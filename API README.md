
---

##  **EnrichMinion API Automation Tests (Postman)**

| **#** | **Test Name**                         | **Endpoint**               | **Method** | **Request Body / Params**                                                            | **Expected Response**                                                         | **Postman Test Script**                                                                                                                                        |
| ----- | ------------------------------------- | -------------------------- | ---------- | ------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1     | **User Registration - Valid**         | `/auth/v1/signup`          | POST       | `{ "email": "testuser@gmail.com", "password": "Test@123", "fullName": "Test User" }` | `status: 200`, `"success": true`, `"message": "User registered successfully"` | `js pm.test("Status code is 200", () => pm.response.to.have.status(200)); pm.test("Success true", () => pm.expect(pm.response.json().success).to.eql(true)); ` |
| 2     | **User Registration - Invalid Email** | `/auth/v1/signup`          | POST       | `{ "email": "invalid", "password": "Test@123", "fullName": "Test User" }`            | `status: 400`, `"error": "Invalid email format"`                              | `js pm.test("Invalid email returns 400", () => pm.response.to.have.status(400)); `                                                                             |
| 3     | **Login - Valid User**                | `/auth/v1/token`           | POST       | `{ "email": "testuser@gmail.com", "password": "Test@123" }`                          | `status: 200`, `"success": true`, `"token"` exists                            | `js const json = pm.response.json(); pm.test("Login successful", () => pm.expect(json.success).to.eql(true)); pm.environment.set("token", json.token); `       |
| 4     | **Login - Invalid Password**          | `/auth/v1/token`           | POST       | `{ "email": "testuser@gmail.com", "password": "wrongpass" }`                         | `status: 401`, `"error": "Invalid credentials"`                               | `js pm.test("Invalid password returns 401", () => pm.response.to.have.status(401)); `                                                                          |
| 5     | **Forgot Password**                   | `/auth/v1/forgot-password` | POST       | `{ "email": "testuser@gmail.com" }`                                                  | `status: 200`, `"message": "Password reset email sent"`                       | `js pm.test("Reset email sent", () => pm.expect(pm.response.json().success).to.eql(true)); `                                                                   |
| 6     | **Get User Profile**                  | `/auth/v1/user`            | GET        | Header: `Authorization: Bearer {{token}}`                                            | `status: 200`, contains `"email"`, `"fullName"`                               | `js pm.test("Profile fetched successfully", () => pm.response.to.have.status(200)); `                                                                          |
| 7     | **Enrichment - Valid Input**          | `/enrichment`              | POST       | `{ "email": "elonmusk@tesla.com" }`                                                  | `status: 200`, `"data"` not empty                                             | `js pm.test("Enrichment success", () => pm.expect(pm.response.json().data).to.exist); `                                                                        |
| 8     | **Enrichment - Invalid Email**        | `/enrichment`              | POST       | `{ "email": "invalidemail" }`                                                        | `status: 400`, `"error": "Invalid email"`                                     | `js pm.test("Invalid email fails", () => pm.response.to.have.status(400)); `                                                                                   |
| 9     | **Verification - Email Check**        | `/verification`            | POST       | `{ "email": "testuser@gmail.com" }`                                                  | `status: 200`, `"verified": true/false`                                       | `js pm.test("Verification check runs", () => pm.response.to.have.status(200)); `                                                                               |
| 10    | **Logout**                            | `/auth/v1/logout`          | POST       | Header: `Authorization: Bearer {{token}}`                                            | `status: 200`, `"message": "Logged out successfully"`                         | `js pm.test("Logout success", () => pm.response.to.have.status(200)); `                                                                                        |

---

###  Environment Setup (Postman)

1. Create an environment variable `base_url` →
   `https://enrichminion.vercel.app/api`
2. Use endpoints like:
   `{{base_url}}/auth/v1/signup`
3. Add environment variable `token` (auto-set during login test #3).

---

###  Collection Export

After creating all 10 tests:

1. Save them in one collection → `EnrichMinion_API_Automation`.
2. Export → *Collection (v2.1)* → Save as
   `automation/api/enrichminion_api_collection.json`

---

