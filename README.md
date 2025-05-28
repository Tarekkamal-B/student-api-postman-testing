# Student API Testing with Postman

A Postman collection for testing CRUD operations on a Student Management API (mock backend using `json-server`).

## 📌 Repository Name

**`student-api-postman-testing`**

---

## 🚀 Setup Instructions

### 1. Install JSON Server

```bash
npm install -g json-server
````

### 2. Start the Mock API

Place your `students.json` file in a project folder and run:

```bash
json-server --watch students.json
```

**API Base URL:**
`http://localhost:3000/students`

### 3. Import Postman Collection

* Download `Student-API-Postman-Collection.json` from this repo.
* Import into Postman.

---

## 📚 API Endpoints

| Method | Endpoint         | Description              |
| ------ | ---------------- | ------------------------ |
| GET    | `/students`      | Get all students         |
| GET    | `/students/{id}` | Get single student by ID |
| POST   | `/students`      | Add new student          |
| PUT    | `/students/{id}` | Update student by ID     |
| DELETE | `/students/{id}` | Delete student by ID     |

---

## 🔍 Test Assertions

### ✅ Common Checks

* Status codes (`200`, `201`, `204`)
* Header: `Content-Type: application/json`
* Response time (`< 500ms`)

### 📜 JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "id": { "type": "string" },
    "name": { "type": "string" },
    "age": { "type": "integer" },
    "grade": { "type": "string" },
    "subjects": {
      "type": "array",
      "items": { "type": "string" }
    }
  },
  "required": ["id", "name", "age", "grade", "subjects"]
}
```

---

## 🧪 Detailed Test Cases

### 1. GET All Students (`/students`)

**Assertions:**

```javascript
pm.expect(jsonData[0].id).to.be.a("string");
pm.expect(jsonData[0].subjects).to.include("Math");
```

* Response is an array
* Schema validation for all items

### 2. GET Single Student (`/students/1`)

**Assertions:**

```javascript
pm.expect(jsonData.id).to.eql("1");
```

* Subjects array contains expected values

### 3. POST New Student

**Request Body:**

```json
{
  "id": "4",
  "name": "Tarek Kamal",
  "age": 27,
  "grade": "4.8",
  "subjects": ["C++", "Cypress", "API Testing"]
}
```

**Assertions:**

* Status code `201`
* Response matches request body

### 4. PUT Update Student

**Assertions:**

```javascript
pm.expect(jsonData.subjects).to.include("Electronics");
```

* Updated fields persist

### 5. DELETE Student

**Assertions:**

* Status code `204`
* Verify deletion via `GET /students`

---

## 📂 Repository Structure

```
student-api-postman-testing/
├── Student-API-Postman-Collection.json
├── students.json
└── README.md
```

---

## 💡 How to Contribute

1. Fork the repo
2. Add edge-case tests (e.g., invalid inputs)
3. Submit a PR!

---

🎯 **Perfect for QA Engineers** learning:

* API testing with Postman
* Schema validation
* Automated checks

