# Go Project with GORM Relationships

This README details the use of GORM functionalities to manage database relationships in a Go project. It includes struct definitions for one-to-many, one-to-one, and many-to-many relationships.

## One-to-Many Relationship

In a one-to-many relationship, one record in a table can be associated with one or more records in another table.

### Example: Users and Posts

```go
// User represents the users table
type User struct {
    ID    string `gorm:"primaryKey"`
    Name  string
    Posts []Post `gorm:"foreignKey:UserId"`
}

// Post represents the posts table
type Post struct {
    ID     string `gorm:"primaryKey"`
    UserId string `gorm:"column:user_id"`
    User   User
}
```

## One-to-One Relationship
```go
// User represents the users table
type User struct {
    ID      string `gorm:"primaryKey"`
    Name    string
    Profile Profile
}

// Profile represents the profiles table
type Profile struct {
    ID     string `gorm:"primaryKey"`
    UserID string `gorm:"unique"`
    User   User
}
```

## Many-to-Many Relationship
```go
// Student represents the students table
type Student struct {
    ID      string `gorm:"primaryKey"`
    Name    string
    Courses []Course `gorm:"many2many:student_courses;"`
}

// Course represents the courses table
type Course struct {
    ID       string `gorm:"primaryKey"`
    Title    string
    Students []Student `gorm:"many2many:student_courses;"`
}

```
