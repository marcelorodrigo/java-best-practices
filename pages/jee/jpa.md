# JPA

### Use `TypedQuery` instead of `Query`

`TypedQuery` is just faster, and you don't need to cast.

Bad:

```java
Query q = em.createQuery("SELECT t FROM Type t where xyz = :xyz");
q.setParemeter("xyz", xyz);
List<Type> types = (List<Type>) q.getResultList();
```

Better:

```java
TypedQuery<Type> q = em.createQuery("SELECT t FROM Type t where xyz = :xyz", Type.class)
  .setParemeter("xyz", xyz);
List<Type> types = q.getResultList();
```

### Use fluent interface in queries

Good:

```java
TypedQuery<Type> q = em.createQuery(
  "SELECT t FROM Type t where xyz = :xyz and abc = :abc", Type.class);
  q.setParemeter("xyz", xyz);
  q.setParemeter("abc", abc);
  List<Type> types = q.getResultList();
```

Better:

```java
List<Type> types = em.createQuery(
  "SELECT t FROM Type t where xyz = :xyz and abc = :abc", Type.class)
  .setParemeter("xyz", xyz)
  .setParemeter("abc", abc)
  .getResultList();
```
