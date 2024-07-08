# Django-Boilerplate-for-Rest-Api

## Install Djoser and Required Packages
```bash
pip install django djangorestframework djoser djangorestframework_simplejwt
```
## Add Djoser to Installed Apps

Edit settings.py:
```python
INSTALLED_APPS = [
    ...
    'django.contrib.sites',
    'rest_framework',
    'djoser',
    'rest_framework_simplejwt',
    ...
]
```

## Configure Djoser

Edit settings.py:
```python
# Djoser settings
DJOSER = {
    'SERIALIZERS': {},
}
```

## Configure URLs

Edit urls.py:
```python
from django.urls import path,include,re_path

urlpatterns = [
    re_path(r'^auth/', include('djoser.urls')),
    re_path(r'^auth/', include('djoser.urls.jwt')),
]
```


## Configure Authentication Classes

Edit settings.py
```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ],
}
```

**Authentication Endpoints:**

- **User Registration:**
  - URL: `POST /auth/users/`
  - Description: Register a new user.
  - Body: JSON containing user data.
    ```json
    {
      "username": "example_user",
      "email": "example@example.com",
      "password": "example_password"
    }
    ```
  - Response:
    - Status: 201 Created
    - Body: JSON representing the created user.
      ```json
      {
        "email": "example@example.com",
        "username": "example_user"
      }
      ```

- **User Details:**
  - URL: `GET /auth/users/`
  - Description: Retrieve user details.
  - Headers:
    - Authorization: JWT token (Bearer token)
  - Response:
    - Status: 200 OK
    - Body: JSON representing the user details.

- **User Update:**
  - URL: `PUT /auth/users/`
  - Description: Update user details.
  - Headers:
    - Authorization: JWT token (Bearer token)
  - Body: JSON containing updated user data.
    ```json
    {
      "username": "new_username",
      "email": "new_email@example.com"
    }
    ```
  - Response:
    - Status: 200 OK
    - Body: JSON representing the updated user details.

- **User Confirmation:**
  - URL: `POST /auth/users/confirm/`
  - Description: Confirm user account registration.
  - Body: JSON containing confirmation data.
    ```json
    {
      "uid": "your_user_id",
      "token": "your_token_here"
    }
    ```
  - Response:
    - Status: 204 No Content

- **Resend Activation Email:**
  - URL: `POST /auth/users/resend_activation/`
  - Description: Resend activation email.
  - Body: JSON containing email address.
    ```json
    {
      "email": "example@example.com"
    }
    ```
  - Response:
    - Status: 204 No Content

- **Set Password:**
  - URL: `POST /auth/users/set_password/`
  - Description: Set user password.
  - Body: JSON containing new password.
    ```json
    {
      "new_password": "new_example_password"
    }
    ```
  - Response:
    - Status: 204 No Content

- **Password Reset Request:**
  - URL: `POST /auth/users/reset_password/`
  - Description: Request a password reset by providing the email address.
  - Body: JSON containing the email address.
    ```json
    {
      "email": "example@example.com"
    }
    ```
  - Response:
    - Status: 204 No Content

- **Password Reset Confirmation:**
  - URL: `POST /auth/users/reset_password_confirm/`
  - Description: Confirm a password reset by providing the token and new password.
  - Body: JSON containing the token and new password.
    ```json
    {
      "uid": "your_user_id",
      "token": "your_token_here",
      "new_password": "new_example_password"
    }
    ```
  - Response:
    - Status: 204 No Content

- **Set Username:**
  - URL: `POST /auth/users/set_username/`
  - Description: Set user username.
  - Body: JSON containing new username.
    ```json
    {
      "new_username": "new_username"
    }
    ```
  - Response:
    - Status: 204 No Content

- **Username Reset Request:**
  - URL: `POST /auth/users/reset_username/`
  - Description: Request a username reset by providing the email address.
  - Body: JSON containing the email address.
    ```json
    {
      "email": "example@example.com"
    }
    ```
  - Response:
    - Status: 204 No Content

- **Username Reset Confirmation:**
  - URL: `POST /auth/users/reset_username_confirm/`
  - Description: Confirm a username reset by providing the token and new username.
  - Body: JSON containing the token and new username.
    ```json
    {
      "uid": "your_user_id",
      "token": "your_token_here",
      "new_username": "new_username"
    }
    ```
  - Response:
    - Status: 204 No Content

- **Token Login (Token Based Authentication):**
  - URL: `POST /auth/token/login/`
  - Description: Obtain an authentication token by providing valid credentials.
  - Body: JSON containing login credentials.
    ```json
    {
      "username": "example_user",
      "password": "example_password"
    }
    ```
  - Response:
    - Status: 200 OK
    - Body: JSON containing authentication token.
      ```json
      {
        "auth_token": "your_generated_token_here"
      }
      ```

- **Token Logout (Token Based Authentication):**
  - URL: `POST /auth/token/logout/`
  - Description: Logout and invalidate the current authentication token.
  - Headers:
    - Authorization: JWT token (Bearer token)
  - Response:
    - Status: 204 No Content

- **JWT Token Create (JSON Web Token Authentication):**
  - URL: `POST /auth/jwt/create/`
  - Description: Obtain an authentication token (JWT) by providing valid credentials.
  - Body: JSON containing login credentials.
    ```json
    {
      "username": "example_user",
      "password": "example_password"
    }
    ```
  - Response:
    - Status: 200 OK
    - Body: JSON containing authentication token.
      ```json
      {
        "access": "your_generated_access_token_here",
        "refresh": "your_generated_refresh_token_here"
      }
      ```

- **JWT Token Refresh (JSON Web Token Authentication):**
  - URL: `POST /auth/jwt/refresh/`
  - Description: Refresh an authentication token (JWT).
  - Body: JSON containing refresh token.
    ```json
    {
      "refresh": "your_refresh_token_here"
    }
    ```
  - Response:
    - Status: 200 OK
    - Body: JSON containing new access token.
      ```json
      {
        "access": "your_new_access_token_here"
      }
      ```

- **JWT Token Verify (JSON Web Token Authentication):**
  - URL: `POST /auth/jwt/verify/`
  - Description: Verify the validity of an authentication token (JWT).
  - Body: JSON containing access token.
    ```json
    {
      "token": "your_access_token_here"
    }
    ```
  - Response:
    - Status: 200 OK
    - Body: JSON indicating token validity.
      ```json
      {
        "token_status": "valid"
      }
      ```