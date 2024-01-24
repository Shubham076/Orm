
###  One-to-One Relationship

#### Example: `User` and `Profile`

**User.java:**


```java
import javax.persistence.*;

@Entity
public class User {
    @Id
    private String id;
    private String name;

    @OneToOne(mappedBy = "user", cascade = CascadeType.ALL)
    private Profile profile;

    // Getters and setters...
} 


@Entity
public class Profile {
    @Id
    private String id;
    private String bio;

    @OneToOne
    @JoinColumn(name = "user_id", referencedColumnName = "id")
    private User user;

    // Getters and setters...
}
``` 

### 2. One-to-Many Relationship

#### Example: `User` and `Post`



```java
import javax.persistence.*;
import java.util.Set;

@Entity
public class User {
    @Id
    private String id;
    private String name;

    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private Set<Post> posts;

    // Getters and setters...
}` 


@Entity
public class Post {
    @Id
    private String id;
    private String content;

    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;

    // Getters and setters...
}
``` 

### 3. Many-to-Many Relationship

#### Example: `Student` and `Course`


```java
import javax.persistence.*;
import java.util.Set;

@Entity
public class Student {
    @Id
    private String id;
    private String name;

    @ManyToMany(cascade = { CascadeType.ALL })
    @JoinTable(
        name = "Student_Course", 
        joinColumns = { @JoinColumn(name = "student_id") }, 
        inverseJoinColumns = { @JoinColumn(name = "course_id") }
    )
    private Set<Course> courses;

    // Getters and setters...
}


@Entity
public class Course {
    @Id
    private String id;
    private String title;

    @ManyToMany(mappedBy = "courses")
    private Set<Student> students;

    // Getters and setters...
}
```
