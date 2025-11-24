# Postman API Testing – Test FFC Application

This folder contains my Postman-based API testing for the **Test Field Force** (Test FFC) web application.

## 1. Scope

I automated API tests for:

1. **Login API (Valid credentials)**  
2. **Login API (Invalid credentials)**  
3. **Add Lead / Add Customer API**  

These tests verify authentication and basic customer creation functionality that is used in the UI.

---

## 2. Files

- `TestFFC_API_Collection.json`  
  Postman collection containing all API requests and tests:
  - `Login - valid`
  - `Login - invalid`
  - `AddLead - Add Customer`

- `TestFFC_Environment.json`  
  Postman environment with variables like:
  - `baseUrl` – `https://testffc.nimapinfotech.com/api`
  - `username` – login mobile number
  - `password` – login password
  - `basicAuth` – Base64 encoded `username:password` (for Basic Auth)

---

## 3. How to Import & Run

### Step 1 – Import Environment
1. Open Postman.
2. Go to **Environments → Import**.
3. Select `TestFFC_Environment.json`.
4. Choose **Test FFC Environment** in the top-right environment dropdown.

### Step 2 – Import Collection
1. In Postman → **Collections → Import**.
2. Select `TestFFC_API_Collection.json`.
3. The collection **“Test FFC API Testing”** will appear.

### Step 3 – Run individual requests

1. Open **Login - valid**  
   - Method: `POST {{baseUrl}}/account/authenticate`  
   - Body uses `{{username}}` and `{{password}}` from the environment.  
   - Tests:
     - Status code is 200  
     - `success = true`  
     - `userId` exists  

2. Open **Login - invalid**  
   - Uses a wrong password.  
   - Tests:
     - Status is 200 or 4xx  
     - `success = false` or appropriate error message.

3. Open **AddLead - Add Customer**  
   - Method: `POST {{baseUrl}}/CRM/AddLead`  
   - Uses **Basic Auth** (`Authorization: Basic {{basicAuth}}`) built from username + password.  
   - Body contains the sample Lead / Customer JSON.  
   - Tests:
     - Status code is 200  
     - Response has `success` / `Message`  
     - Saves `LeadId` into environment when success.

### Step 4 – Run via Collection Runner

1. Click the collection **“Test FFC API Testing”** → **Run**.
2. Select environment **Test FFC Environment**.
3. Click **Start Run**.
4. View pass/fail results for all three APIs.

---

## 4. Key Checks Implemented

- **Login (valid):**
  - Status = 200  
  - `success = true`  
  - `userId` is present  

- **Login (invalid):**
  - Status = 200 or appropriate 4xx  
  - `success = false` or error message  

- **Add Lead / Add Customer:**
  - Status = 200  
  - API returns success/message  
  - When successful, a `LeadId` is returned and stored as `newLeadId`.

---

## 5. Tools Used

- **Postman** for API request creation, test scripts and execution  
- **JavaScript test scripts** in Postman (using `pm.*` APIs)  
- **Environment variables** to avoid hard-coding URLs and credentials.

---

