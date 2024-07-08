# Django-Boilerplate-for-Rest-Api

## Install Packages
```bash
pip install djangorestframework-simplejwt
```
## Configure Simple JWT in Django Settings
```python
REST_FRAMEWORK = {
    # ...
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ],
}

SIMPLE_JWT = {
    'AUTH_HEADER_NAME': 'HTTP_AUTHORIZATION',
    'TOKEN_TTL': 3600,  # Token expires after 1 hour
    'REFRESH_TOKEN_TTL': 10800,  # Refresh token expires after 3 hours
}
```
## Create Post Serializer
```python
from .models import Post
from rest_framework import serializers

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = ['id', 'title', 'content', 'active']
```

## Login & Logout View With Protected view
```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.auth import authenticate, login, logout
from rest_framework_simplejwt.tokens import RefreshToken

# Login view
class LoginView(APIView):
    def post(self, request):
        username = request.data['username']
        password = request.data['password']

        user = authenticate(username=username, password=password)
        if user is not None:
            login(request, user)
            token = RefreshToken.for_user(user)
            return Response({'token': str(token.access_token)})
        else:
            return Response({'error': 'Invalid credentials'})

# Logout view
class LogoutView(APIView):
    def post(self, request):
        logout(request)
        return Response({'message': 'Successfully logged out'})

# Protected view
class ProtectedView(APIView):
    def get(self, request):
        if request.user.is_authenticated:
            return Response({'message': 'You are authorized to access this view'})
        else:
            return Response({'error': 'You must be logged in to access this view'})
```

## urls.py
```python
from django.urls import path
from .views import LoginView, LogoutView, ProtectedView

urlpatterns = [
    path('login/', LoginView.as_view(), name='login'),
    path('logout/', LogoutView.as_view(), name='logout'),
    path('protected/', ProtectedView.as_view(), name='protected'),
]
```