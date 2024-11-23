### **Issue [#5: Pytest Passing Incorrect Parameters](../../issues/5)**  
**Description:**  
Several tests were failing because `pytest` did not pass the correct parameters. HTTP status code mismatches (`401` vs. `403`) occurred due to missing or incorrect token data.

**Solution:**  
Added the `login_request_data` function in `conftest.py`, which properly injects `admin_token`, `manager_token`, and `user_token` to ensure valid authorization during tests.

**Tests Affected:**  
- `test_create_user_access_denied`  
- `test_retrieve_user_access_denied`  
- `test_update_user_email_access_denied`  
- `test_list_users_unauthorized`  

**Error Logs:**  
```
FAILED tests/test_api/test_users_api.py::test_create_user_access_denied - assert 401 == 403
FAILED tests/test_api/test_users_api.py::test_retrieve_user_access_denied - assert 401 == 403
FAILED tests/test_api/test_users_api.py::test_update_user_email_access_denied - assert 401 == 403
FAILED tests/test_api/test_users_api.py::test_list_users_unauthorized - assert 401 == 403
```

---

### **Issue [#4: Incorrect Test Data Passed to CRUD Operations](../../issues/4)**  
**Description:**  
CRUD-related tests failed due to misaligned test data, resulting in validation errors and other issues.

**Solution:**  
Revised test data to properly sync with expected inputs. Verified connections and fixed discrepancies in database state and route configurations.

**Tests Affected:**  
- `test_update_user_email_access_allowed`  
- `test_delete_user_does_not_exist`  
- Other CRUD-related tests  

**Error Logs:**  
```
ValidationError, KeyError, and other CRUD-related issues.
```

**Root Cause:**  
- Misconfigured test data.  
- Invalid parameters or database state during testing.

---

### **Issue [#3: Access Denied in Test APIs](../../issues/3)**  
**Description:**  
Permission-related tests failed with "Access Denied" errors (`401`). This was caused by missing or invalid authorization tokens during API calls.

**Solution:**  
Enhanced `login_request_data` in `conftest.py` to ensure valid authorization tokens are sent, resolving the permission issues.

**Tests Affected:**  
- `test_create_user_access_denied`  
- `test_retrieve_user_access_denied`  
- `test_update_user_email_access_denied`  

**Error Logs:**  
```
Access Denied (401 - Unauthorized)
```

**Root Cause:**  
- Missing or invalid tokens.  
- Improper role-based access permissions.

---

### **Issue [#2: Validation Errors in User Schemas](../../issues/2)**  
**Description:**  
Tests in `test_user_schemas.py` failed due to validation errors, particularly missing or incorrect `uuid` fields.

**Solution:**  
Updated `test_user_schemas.py` to include the necessary `uuid` field, ensuring compatibility with the expected schema.

**Tests Affected:**  
- `test_user_response_valid`  
- `test_login_request_valid`  

**Error Logs:**  
```
ValidationError
```

**Root Cause:**  
- Missing required fields in the test data.

---

### **Issue [#1: KeyError in User Fields](../../issues/1)**  
**Description:**  
Tests were failing because the pytest setup did not properly reference required resources. Specifically, the `nickname` field was missing from test data or schemas.

**Solution:**  
Corrected the pytest configuration to reference the appropriate resources and added the missing `nickname` field to test data and schemas.

**Tests Affected:**  
- `test_user_base_valid`  
- `test_user_create_valid`  
- `test_user_update_valid`  

**Error Logs:**  
```
KeyError - Missing field "nickname"
```

**Root Cause:**  
- Missing field (`nickname`) in test data or schema.
