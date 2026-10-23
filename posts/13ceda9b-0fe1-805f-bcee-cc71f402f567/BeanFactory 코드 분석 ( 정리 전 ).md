---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 13ceda9b-0fe1-805f-bcee-cc71f402f567
title: BeanFactory 코드 분석 ( 정리 전 )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 13ceda9b-0fe1-8067-9531-e4fdae3568a2
    title: "[sparta] 스프링 숙련"
  - id: 13ceda9b-0fe1-8053-affd-fe8c876b9815
    title: Spring 핵심 개념
  - id: 13ceda9b-0fe1-805f-bcee-cc71f402f567
    title: BeanFactory 코드 분석 ( 정리 전 )
excerpt: "[ 코드 ] java public class BeanFactory implements ObjectFactory { private static final StringManager sm = StringManager.getManager(BeanFactory.class); private final Log log = LogFact"
cover: null
icon: 🧐
notionProperties: {}
schema_version: 1
parent_id: 13ceda9b-0fe1-8053-affd-fe8c876b9815
created: 2024-11-12T05:56:39.112Z
updated: 2024-11-12T05:59:55.667Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/[sparta] 스프링 숙련-e4fdae3568a2/Spring 핵심 개념-fe8c876b9815/BeanFactory 코드 분석 ( 정리 전 )-cc71f402f567/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/13ceda9b0fe1805fbceecc71f402f567
---
<details>
<summary>&#91; 코드 &#93;</summary>

<a id="13ceda9b0fe18031a99bcd9b433b8a08"></a>

```java
public class BeanFactory implements ObjectFactory {

    private static final StringManager sm = StringManager.getManager(BeanFactory.class);

    private final Log log = LogFactory.getLog(BeanFactory.class); // Not static

    @Override
    public Object getObjectInstance(Object obj, Name name, Context nameCtx, Hashtable<?,?> environment)
            throws NamingException {

        if (obj instanceof ResourceRef) {

            try {
                Reference ref = (Reference) obj;
                String beanClassName = ref.getClassName();
                Class<?> beanClass = null;
                ClassLoader tcl = Thread.currentThread().getContextClassLoader();
                try {
                    if (tcl != null) {
                        beanClass = tcl.loadClass(beanClassName);
                    } else {
                        beanClass = Class.forName(beanClassName);
                    }
                } catch(ClassNotFoundException cnfe) {
                    NamingException ne = new NamingException(sm.getString("beanFactory.classNotFound", beanClassName));
                    ne.initCause(cnfe);
                    throw ne;
                }

                BeanInfo bi = Introspector.getBeanInfo(beanClass);
                PropertyDescriptor[] pda = bi.getPropertyDescriptors();

                Object bean = beanClass.getConstructor().newInstance();

                // Look for the removed forceString option
                RefAddr ra = ref.get("forceString");
                if (ra != null) {
                    log.warn(sm.getString("beanFactory.noForceString"));
                }

                Enumeration<RefAddr> e = ref.getAll();
                String value;

                while (e.hasMoreElements()) {

                    ra = e.nextElement();
                    String propName = ra.getType();

                    if (propName.equals(Constants.FACTORY) ||
                        propName.equals("scope") || propName.equals("auth") ||
                        propName.equals("forceString") ||
                        propName.equals("singleton")) {
                        continue;
                    }

                    value = (String)ra.getContent();

                    Object[] valueArray = new Object[1];

                    int i = 0;
                    for (i = 0; i < pda.length; i++) {

                        if (pda[i].getName().equals(propName)) {

                            Class<?> propType = pda[i].getPropertyType();
                            Method setProp = pda[i].getWriteMethod();

                            if (propType.equals(String.class)) {
                                valueArray[0] = value;
                            } else if (propType.equals(Character.class) || propType.equals(char.class)) {
                                valueArray[0] = Character.valueOf(value.charAt(0));
                            } else if (propType.equals(Byte.class) || propType.equals(byte.class)) {
                                valueArray[0] = Byte.valueOf(value);
                            } else if (propType.equals(Short.class) || propType.equals(short.class)) {
                                valueArray[0] = Short.valueOf(value);
                            } else if (propType.equals(Integer.class) || propType.equals(int.class)) {
                                valueArray[0] = Integer.valueOf(value);
                            } else if (propType.equals(Long.class) || propType.equals(long.class)) {
                                valueArray[0] = Long.valueOf(value);
                            } else if (propType.equals(Float.class) || propType.equals(float.class)) {
                                valueArray[0] = Float.valueOf(value);
                            } else if (propType.equals(Double.class) || propType.equals(double.class)) {
                                valueArray[0] = Double.valueOf(value);
                            } else if (propType.equals(Boolean.class) || propType.equals(boolean.class)) {
                                valueArray[0] = Boolean.valueOf(value);
                            } else if (setProp != null) {
                                // This is a Tomcat specific extension and is not part of the
                                // Java Bean specification.
                                String setterName = setProp.getName();
                                try {
                                    setProp = bean.getClass().getMethod(setterName, String.class);
                                    valueArray[0] = value;
                                } catch (NoSuchMethodException nsme) {
                                    throw new NamingException(sm.getString(
                                            "beanFactory.noStringConversion", propName, propType.getName()));
                                }
                            } else {
                                throw new NamingException(sm.getString(
                                        "beanFactory.noStringConversion", propName, propType.getName()));
                            }

                            if (setProp != null) {
                                setProp.invoke(bean, valueArray);
                            } else {
                                throw new NamingException(sm.getString("beanFactory.readOnlyProperty", propName));
                            }

                            break;
                        }
                    }

                    if (i == pda.length) {
                        throw new NamingException(sm.getString("beanFactory.noSetMethod", propName));
                    }
                }

                return bean;

            } catch (java.beans.IntrospectionException ie) {
                NamingException ne = new NamingException(ie.getMessage());
                ne.setRootCause(ie);
                throw ne;
            } catch (ReflectiveOperationException e) {
                Throwable cause = e.getCause();
                if (cause instanceof ThreadDeath) {
                    throw (ThreadDeath) cause;
                }
                if (cause instanceof VirtualMachineError) {
                    throw (VirtualMachineError) cause;
                }
                NamingException ne = new NamingException(e.getMessage());
                ne.setRootCause(e);
                throw ne;
            }

        } else {
            return null;
        }
    }
}
```

</details>
