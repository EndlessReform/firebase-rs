# firebase-rs

[![Crates.io](https://img.shields.io/crates/v/firebase-rs.svg)](https://crates.io/crates/firebase-rs) [![docs.rs](https://docs.rs/firebase-rs/badge.svg)](https://docs.rs/firebase-rs) [![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

Rust based Firebase library.
---
![firebase](https://firebase.google.com/downloads/brand-guidelines/SVG/logo-logomark.svg 'Firebase')

# Full Documentation
[Documentation](https://docs.rs/firebase-rs/1.0.3/firebase_rs/)

# How to use

### Load library
````rust
use firebase_rs::*;
````

### Without Auth
````rust
let firebase = Firebase::new("https://myfirebase.firebaseio.com").unwrap();
````

### With Auth
````rust
let firebase = Firebase::auth("https://myfirebase.firebaseio.com", "AUTH_KEY").unwrap();
````
---

### At usage for nested objects
````rust
let firebase = Firebase::new("https://myfirebase.firebaseio.com").unwrap().at("users").at("USER_ID").at(...);
````

---

### Read Data

#### Read data with generic type (All)
````rust
#[derive(Serialize, Deserialize, Debug)]
struct User {
  name: String
}

let firebase = Firebase::new("https://myfirebase.firebaseio.com").unwrap().at("users");
let user = firebase.get::<HashMap<String, User>>().await;
````

#### Read data as string
````rust
let firebase = Firebase::new("https://myfirebase.firebaseio.com").unwrap().at("users");
let users = firebase.get_as_string().await;
````

#### Read data with generic type (Single record)
````rust
#[derive(Serialize, Deserialize, Debug)]
struct User {
  name: String
}

let firebase = Firebase::new("https://myfirebase.firebaseio.com").unwrap().at("users").at("USER_ID");
let user = firebase.get_generic::<User>().await;
````


---

### Set Data
````rust
#[derive(Serialize, Deserialize, Debug)]
struct User {
  name: String
}

let user = User { name: String::default() };
let firebase = Firebase::new("https://myfirebase.firebaseio.com").unwrap().at("users");
let users = firebase.set(&user).await;
````

---

### Update Data
````rust
#[derive(Serialize, Deserialize, Debug)]
struct User {
  name: String
}

let user = User { name: String::default() };
let firebase = Firebase::new("https://myfirebase.firebaseio.com").unwrap().at("users").at("USER_ID");
let users = firebase.update(&user).await;
````
