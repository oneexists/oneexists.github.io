---
layout: post
title: "Adding a PostgreSQL Database to a Spring Project"
author: skylar_lynner
categories: [ java ]
---

Building a Maven project with a Spring back-end, PostgreSQL
database, and React front-end.

### Add dependencies to pom.xml for PostgreSQL and JPA
```
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
  </dependency>
  <dependency>
      <groupId>org.postgresql</groupId>
      <artifactId>postgresql</artifactId>
  </dependency>
</dependencies>
```

### Update application.properties
In this example, the name of the database created in
PostgreSQL is *notebookdb*. The username and password
values will be need to be added, but these values should
not be shared.

```
# PostgreSQL
spring.datasource.username=
spring.datasource.password=
spring.datasource.url=jdbc:postgresql://localhost:5432/notebookdb
spring.datasource.driver-class-name=org.postgresql.Driver
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQLDialect
spring.jpa.properties.hibernate.show_sql=true
spring.jpa.generate-ddl=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

### Encrypted Properties
A guide to encrypting properties can be found [here](https://access.redhat.com/documentation/zh-cn/red_hat_fuse/7.9/html/deploying_into_spring_boot/how-to-use-encrypted-property-placeholders-sping-boot).

The updates to the pom.xml file can be summarized here:
```
<dependencies>
  <dependency>
      <groupId>com.github.ulisesbocchio</groupId>
      <artifactId>jasypt-spring-boot-starter</artifactId>
      <version>3.0.3</version>
  </dependency>
</dependencies>

<repositories>
  <repository>
    <id>jasypt-basic</id>
    <name>Jasypt Repository</name>
    <url>https://repo1.maven.org/maven2/</url>
  </repository>
</repositories>

<pluginRepositories>
  <pluginRepository>
     <id>jasypt-basic</id>
     <name>Jasypt Repository</name>
     <url>https://repo1.maven.org/maven2/</url>
  </pluginRepository>
</pluginRepositories>

<build>
  <plugins>
    <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
    </plugin>
    <plugin>
       <groupId>com.github.ulisesbocchio</groupId>
       <artifactId>jasypt-maven-plugin</artifactId>
       <version>3.0.3</version>
    </plugin>
  </plugins>
</build>
```

### Add an AppUser entity model class
Create a package for entities to model data from the database.

To create a write-only password, add the following dependency
to the pom.xml file (updated versions can be found [here](https://mvnrepository.com/artifact/io.jsonwebtoken/jjwt-jackson) by selecting the desired version):
```
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
```

The ApplicationUserRole field is an enum that will be created
for supporting Spring Security. It can be temporarily modeled
as a simple enum and expanded with building the Security
package.
```
public enum ApplicationUserRole {
	USER,
	MANAGER,
	ADMIN;
}
```

At this point the AppUser can be created. It will contain
fields for id, username, password, role, isAccountNonExpired,
isAccountNonLocked, isCredentialsNonExpired, and isEnabled.
The id field will use PostgreSQL to assign an id value, the
password will be write-only to restrict its access, and the
addition of the ApplicationUserRole and boolean fields assist
in meeting the UserDetails contract that will be used in
supporting user authentication and authorization.

```
import com.fasterxml.jackson.annotation.JsonProperty;
import com.notebook.security.ApplicationUserRole;

@Entity
@Table(name = "app_user")
public class AppUser implements Serializable {
	private static final long serialVersionUID = 202207001L;
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long appUserId;
	private String username;
	@JsonProperty(access = JsonProperty.Access.WRITE_ONLY)
	private String password;
	private ApplicationUserRole applicationUserRole;
	private boolean isAccountNonExpired;
	private boolean isAccountNonLocked;
	private boolean isCredentialsNonExpired;
	private boolean isEnabled;

	public AppUser() {
    // no-arg constructor, required for database entities
	}

	public AppUser(String username, String password, ApplicationUserRole applicationUserRole,
			boolean isAccountNonExpired, boolean isAccountNonLocked, boolean isCredentialsNonExpired,
			boolean isEnabled) {
		this.username = username;
		this.password = password;
		this.applicationUserRole = applicationUserRole;
		this.isAccountNonExpired = isAccountNonExpired;
		this.isAccountNonLocked = isAccountNonLocked;
		this.isCredentialsNonExpired = isCredentialsNonExpired;
		this.isEnabled = isEnabled;
	}

  // getters, setters, toString

}
```

### Add Repository Layer
This layer will support the finding a user by their username,
which will be used to implement the UserDetailsService when
adding Spring Security.
```
public interface AppUserRepository extends JpaRepository<AppUser, Long> {
	Optional<AppUser> findByUsername(String username);
	boolean existsByUsername(String usernamme);
}
```
