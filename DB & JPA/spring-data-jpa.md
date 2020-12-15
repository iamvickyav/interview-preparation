# Spring Data JPA - Learnings

## Key Learnings List

* @Modifying is meaningless without @Query annotation
* @Modifying needs @Transactional. Otherwise will result in TransactionRequiredException
* @Transactional only rollback on RuntimeException
* @Transactional(readOnly = true) can be avoided as readOnly adds few performance overheads unncessarily
* Inside @Transactional, if you get a fetch a Entity & update the Entity, you don't need to explicitly save the Entity

## Interesting facts

* All fields in @Entity class are default persistable

<hr>

## @Query Annotation

### 1. How to use the method args in @Query

```java
// Access params using param's position
@Query("select u from User u where u.emailAddress = ?1")
User findByEmailAddress(String emailAddress);

// Access params using param's name
@Query("select u from User u where u.firstname = :firstname or u.lastname = :lastname")
User findByLastnameOrFirstname(@Param("lastname") String lastname, @Param("firstname") String firstname);
```

### 2. How to write a update/delete query

```java
@Modifying
@Query("update User u set u.firstname = ?1 where u.lastname = ?2")
int setFixedFirstnameFor(String firstname, String lastname);
```

### 3. Query from Method name is slow for Modifying queries

Consider the following delete methods

```java
public interface EmployeeRepo extends JpaRepository<Employee, Integer>{

    void deleteById(Integer id);

    @Modifying
    @Query("delete from Employee e where e.id = ?1")
    void deleteByGivenId(Integer id);
}
```

```java
// Queries generated 

void deleteById(Integer id);

Hibernate: 
    select
        employee0_.id as id1_0_0_,
        employee0_.name as name2_0_0_ 
    from
        employee employee0_ 
    where
        employee0_.id=?
Hibernate: 
    delete 
    from
        employee 
    where
        id=?

---

@Modifying
@Query("delete from Employee e where e.id = ?1")
void deleteByGivenId(Integer id);
    
Hibernate: 
    delete 
    from
        employee 
    where
        id=?
```

### One to One Ownership

In below example, customer is the owner of the address

```
@Entity
class Customer {

    @OneToOne
    Address address;
}

@Entity
class Address {

    @OneToOne(mappedBy="address");
    Customer customer;
}
```
