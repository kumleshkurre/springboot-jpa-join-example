# springboot-jpa-join-example
---
Spring Boot REST API demonstrating JPQL JOIN between multiple tables (Employee and Staff) using Spring Data JPA, DTO mapping, and PostgreSQL.

## 📂 Project Structure
```
KCAPI
├── src/main/java
│   └── kumlesh
│       ├── KurrecomputersApplication.java
│       ├── Kurre.java
│       ├── Kurrerepo.java
│       └── KurreControler.java
│
├── src/main/resources
│   └── application.properties
└── pom.xml
```

## ⚙️ Project Setup
### 1️⃣ Create Spring Boot Project
- Project Type: Maven
- Group: restapi
- Artifact: KCAPI
- Package: kcrestapi

### 2️⃣ Dependencies Used
- Spring Boot DevTools
- Spring Web
- Spring Data JPA
- PostgreSQL Driver
- Spring Boot Actuator


## 🗄️ Database Configuration
src/main/resources/application.properties
```
spring.application.name=kurrecomputers
spring.datasource.url=jdbc:postgresql://localhost:5432/your_database_name
spring.datasource.username=your_username
spring.datasource.password=YOUR_PASSWORD
spring.datasource.driver-class-name=org.postgresql.Driver

# JPA settings
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
```

## ▶️ Application Entry Point
```

package kumlesh;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class KurrecomputersApplication {

	public static void main(String[] args) {
		SpringApplication.run(KurrecomputersApplication.class, args);
		System.out.println("Success....!");
	}

}

```
Run the project using: Run As → Spring Boot App

## 🧱 Step 1: Create Entity – Employe
```
package kumlesh;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name = "employe")
public class Employe {

	@Id
	private int id;
	private String mobile;
	private String name;

	// Getters & Setters
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getMobile() {
		return mobile;
	}
	public void setMobile(String mobile) {
		this.mobile = mobile;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
}
```
## 🧱 Step 2: Create Entity – Staff
```
package kumlesh;

import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name = "staff")
public class Staff {

	@Id
	private int id;
	private int age;
	private String city;

	// Getters & Setters
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public String getCity() {
		return city;
	}
	public void setCity(String city) {
		this.city = city;
	}
}
```
## 📦 Step 3: Create DTO Class (Join Result)
```
package kumlesh;

public class EmpStaffDTO {

	private int id;
	private String name;
	private String mobile;
	private int age;
	private String city;

	public EmpStaffDTO(int id, String name, String mobile, int age, String city) {
		this.id = id;
		this.name = name;
		this.mobile = mobile;
		this.age = age;
		this.city = city;
	}

	// Getters & Setters
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getMobile() {
		return mobile;
	}
	public void setMobile(String mobile) {
		this.mobile = mobile;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public String getCity() {
		return city;
	}
	public void setCity(String city) {
		this.city = city;
	}
}
```
## 📂 Step 4: Repository Layer (JOIN Query)
```
package kumlesh;

import java.util.List;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;

public interface Kurrerepo extends JpaRepository<Employe, Integer> {

	@Query("SELECT new kumlesh.EmpStaffDTO(e.id, e.name, e.mobile, s.age, s.city) " +
	       "FROM Employe e JOIN Staff s ON e.id = s.id")
	List<EmpStaffDTO> getJoinData();
}
```
📌 JPQL JOIN ka use karke multiple tables ka data ek DTO me return kiya gaya hai.
## 🎮 Step 5: Controller Layer
```
package kumlesh;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class KurreController {

	@Autowired
	private Kurrerepo repo;

	@GetMapping("/join")
	public List<EmpStaffDTO> joinData() {
		return repo.getJoinData();
	}
}
```
## 🔗 API Endpoint
```
| Method | Endpoint | Description                |
| ------ | -------- | -------------------------- |
| GET    | `/join`  | Employee + Staff JOIN data |
```
## ✅ Output
- API successfully performs CRUD operations
- Data automatically stored in PostgreSQL
- REST endpoints tested via Postman

## 🎯 Learning Outcome
- Hands-on experience with Spring Boot
- Real-world REST API development
- Database integration using JPA
- Clean MVC architecture understanding

## 👨‍💻 Author
**Kumlesh Kurre**  
Backend Developer | Spring Boot | PostgreSQL
