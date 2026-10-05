# Practical 7 – Mobile Application Development

## Contact Application using JSON API

**Submitted By:** Reyan Prajapati
**Enrollment Number:** 24012011155
**Department:** Computer Engineering / Information Technology

---

## 📌 Practical Objective

Create an Android application that retrieves contact information in **JSON format** from a web URL and displays the contacts using a **RecyclerView**.

Each contact contains information such as:

* ID
* Name
* Phone Number
* Email ID
* Address

The application also provides a delete option for individual contacts and stores the retrieved data locally using SQLite.

---

## 🎯 Requirements

The practical requires the following:

1. Create the MainActivity according to the given UI design.
2. Use a generated JSON URL for retrieving contact data.
3. Create a `Person` class containing contact information.
4. Generate and parse JSON data.
5. Display contacts using `RecyclerView` and an Adapter.
6. Add Internet permission in `AndroidManifest.xml`.
7. Create an `HttpRequest` class for communicating with the JSON web URL.

---

## 🛠️ Technologies Used

* **Language:** Kotlin
* **Platform:** Android
* **IDE:** Android Studio
* **UI:** XML
* **JSON:** JSON Generator API
* **Database:** SQLite
* **Networking:** `HttpURLConnection`
* **List:** RecyclerView
* **Asynchronous Processing:** Kotlin Coroutines
* **View Binding:** Android View Binding

---

## 📂 Project Structure

```text
app/
└── src/
    └── main/
        ├── java/
        │   └── com.example.a24012011155_practical_7/
        │       ├── MainActivity.kt
        │       ├── Person.kt
        │       ├── PersonAdapter.kt
        │       ├── DatabaseHelper.kt
        │       ├── PersonDbTableData.kt
        │       └── HttpRequest.kt
        │
        ├── res/
        │   ├── layout/
        │   │   ├── activity_main.xml
        │   │   ├── item_person.xml
        │   │   └── single_item.xml
        │   └── values/
        │       └── styles.xml
        │
        └── AndroidManifest.xml
```

---

## 📱 Application Features

### 1. Fetch Contact Data

The application retrieves JSON contact data from a web API using an HTTP GET request.

The JSON API used in the project is:

```text
https://api.json-generator.com/templates/5rDXHcbgpo93/data
```

The application sends an authorization token with the request.

---

### 2. JSON Parsing

The received JSON response is converted into Kotlin `Person` objects.

The application extracts:

```text
id
name
email
phone
address
```

The `profile` object inside the JSON contains the name and address.

---

### 3. RecyclerView

The contacts are displayed using a `RecyclerView`.

Each contact card displays:

* Person name
* Phone number
* Email address
* Address
* Person icon
* Delete button

The provided UI uses Material CardView and ConstraintLayout for the contact item design.

---

### 4. Delete Contact

Each contact has a delete button.

When the delete button is clicked:

1. The selected contact is removed from the SQLite database.
2. The contact is removed from the RecyclerView.
3. The RecyclerView is updated using `notifyItemRemoved()`.

---

### 5. Local SQLite Database

The application stores downloaded contact information in a local SQLite database named:

```text
persons_db
```

The database contains a table named:

```text
persons
```

The table contains:

| Column  | Type             |
| ------- | ---------------- |
| id      | TEXT PRIMARY KEY |
| name    | TEXT             |
| email   | TEXT             |
| phone   | TEXT             |
| address | TEXT             |

The database structure is defined in `PersonDbTableData.kt`.

---

## 🔐 Internet Permission

Internet permission is added to `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

This permission allows the application to communicate with the JSON web API.

---

## 👤 Person Class

The `Person` class represents a contact:

```kotlin
class Person(
    var id: String,
    var name: String,
    var emailId: String,
    var phoneNo: String,
    var address: String
) : Serializable
```

The class implements `Serializable` so that Person objects can be serialized when required.

---

## 🌐 HTTP Request

The `HttpRequest` class is responsible for communicating with the JSON URL.

It uses:

```kotlin
HttpURLConnection
```

The request method is:

```text
GET
```

An authorization token is sent using the HTTP `Authorization` header.

---

## 🔄 Application Flow

```text
Start Application
       ↓
Check Local SQLite Database
       ↓
Is Database Empty?
   ↙           ↘
 Yes            No
 ↓               ↓
Fetch JSON       Load Local Data
 from API            ↓
 ↓              Display Contacts
Parse JSON
 ↓
Store in SQLite
 ↓
Display Contacts
 ↓
RecyclerView
 ↓
Delete / Refresh
```

---

## 🔄 Data Fetching Process

The application uses Kotlin Coroutines to perform the network operation in the background.

Th
