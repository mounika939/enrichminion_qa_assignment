| **Bug ID** | **Title**       Phone number accepts more than 10 digits                                                        | **Steps to Reproduce**                                                                                                          | **Expected Result**                                                         | **Actual Result**                                 | **Severity** | **Root Cause**         |
| ---------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- | ------------------------------------------------- | ------------ | ---------------------- |
| BUG_EN_02  | Phone number accepts more than 10 digits and API accepts invalid input | 1. Go to Enrichment → Phone Finder <br> 2. Enter phone number with >10 digits <br> 3. Click Submit <br> 4. Observe API response | UI should restrict input to 10 digits; Backend should reject invalid format | Input accepted, API response “Request successful” | High         | **Frontend + Backend** |

**API Response**

{
  "message": "Request successful",
  "error": "",
  "success": true,
  "data": {
    "itemsReceived": 0,
    "curPage": 1,
    "nextPage": null,
    "prevPage": null,
    "perPage": 10,
    "itemsTotal": 0,
    "pageTotal": 0,
    "data": []
  }
}

**Root Cause**: Frontend is not sending input payload to backend API (data: [] observed in response). Backend works correctly when tested directly via API.

<img width="1393" height="782" alt="image" src="https://github.com/user-attachments/assets/4d0ac47f-2846-4846-bea6-880c5675ce8d" />


| **Bug ID**     | **Title**           Sign in with google is failed                                                                 | **Steps to Reproduce**                                                                              | **Expected Result**                                                 | **Actual Result**                                                 | **Severity** | **Root Cause**                            |
| -------------- | ------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- | ----------------------------------------------------------------- | ------------ | ----------------------------------------- |
| **BUG_REG_03** | Sign in with Google fails with error “Unsupported provider: provider is not enabled” | 1. Navigate to Registration page <br> 2. Click **Sign in with Google** <br> 3. Observe API response | User should be authenticated via Google and redirected to dashboard | API returns error `Unsupported provider: provider is not enabled` | **High**     | **Backend** (Google OAuth not configured) |

****Api response**

**{
  "code": 400,
  "error_code": "validation_failed",
  "msg": "Unsupported provider: provider is not enabled"
}****
This response comes from the backend authentication API, not the UI.

Unsupported provider → means that the app tried to authenticate using a provider (Google), but the backend configuration does not recognize or allow it.

provider is not enabled → the Google Sign-In integration is not activated or configured in the backend (e.g., missing OAuth credentials or provider setup in environment variables).
**Root Cause Analysis**
Layer	Responsible Side	Reason
Frontend (UI)	❌ No issue	The UI correctly triggered the Google Sign-In flow.
Backend (Server)	✅ Issue	The backend is not configured to handle Google as an authentication provider (OAuth provider not enabled in backend settings).
<img width="1898" height="1068" alt="image" src="https://github.com/user-attachments/assets/6ca6ff2b-5b18-4041-b02f-be0aeb8ea53b" />

