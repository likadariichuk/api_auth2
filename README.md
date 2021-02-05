# api_auth2
    pip install django
    pip install djangorestframework

    pip install djoser
    pip install djangorestframework_simplejwt
    pip install social-auth-app-django
 
settings.py

#add installed apps


    INSTALLED_APPS = [
        ...
        'rest_framework',
        'djoser',
        'aacounts',
        'social_django', 

        'rest_framework_simplejwt',
        'rest_framework_simplejwt.token_blacklist',
    ]    
 
    REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],

    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ],
    }
    
 SIMPLE JWT SETTINGS in settings.py:
 
        from datetime import timedelta

        SIMPLE_JWT = {
        'ACCESS_TOKEN_LIFETIME': timedelta(minutes=60),
        'REFRESH_TOKEN_LIFETIME': timedelta(days=1),
        'AUTH_HEADER_TYPES': ('JWT',),
        'AUTH_TOKEN_CLASSES': (
            'rest_framework_simplejwt.tokens.AccessToken',
        ),
    }
    
    
 add one piece of middleware
 
     MIDDLEWARE = [
        'social_django.middleware.SocialAuthExceptionMiddleware',
        ...
     ]
     
 add cotext processors to the templates:
 
    TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                ...
                'social_django.context_processors.backends',
                'social_django.context_processors.login_redirect',
            ],
        },
    },
]

add authentication backends:
    
    AUTHENTICATION_BACKENDS = (
    'social_core.backends.github.GithubOAuth2',
    'social_core.backends.google.GoogleOAuth2',
    'django.contrib.auth.backends.ModelBackend'
    )

DJOSER settings in settings.py:
        
     DJOSER = {
        'LOGIN_FIELD': 'email',
        'USER_CREATE_PASSWORD_RETYPE': True,
        'USERNAME_CHANGED_EMAIL_CONFIRMATION': True,
        'PASSWORD_CHANGED_EMAIL_CONFIRMATION': True,
        'SEND_CONFIRMATION_EMAIL': True,
        'SET_USERNAME_RETYPE': True,
        'SET_PASSWORD_RETYPE': True,
        'PASSWORD_RESET_CONFIRM_URL': 'password/reset/confirm/{uid}/{token}',
        'USERNAME_RESET_CONFIRM_URL': 'email/reset/confirm/{uid}/{token}',
        'ACTIVATION_URL': 'activate/{uid}/{token}',
        'SEND_ACTIVATION_EMAIL': True,
        'SOCIAL_AUTH_TOKEN_STRATEGY': 'djoser.social.token.jwt.TokenStrategy',
        'SOCIAL_AUTH_ALLOWED_REDIRECT_URIS': ['http://localhost:8000/google', 'http://localhost:8000/facebook'],
        'SERIALIZERS': {
            'user_create': 'accounts.serializers.UserCreateSerializer',
            'user': 'accounts.serializers.UserCreateSerializer',
            'current_user': 'accounts.serializers.UserCreateSerializer',
            'user_delete': 'djoser.serializers.UserDeleteSerializer',
    }
}

add social settings to settings.py:

        SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = '[YOUR GOOGLE OAUTH2 API KEY]'
        SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = '[YOUR GOOGLE OAUTH2 API SECRET]'
        SOCIAL_AUTH_GOOGLE_OAUTH2_SCOPE = ['https://www.googleapis.com/auth/userinfo.email', 'https://www.googleapis.com/auth/userinfo.profile', 'openid']
        SOCIAL_AUTH_GOOGLE_OAUTH2_EXTRA_DATA = ['first_name', 'last_name']

        SOCIAL_AUTH_FACEBOOK_KEY = '[YOUR FACEBOOK API KEY]'
        SOCIAL_AUTH_FACEBOOK_SECRET = '[YOUR FACEBOOK API SECRET]'
        SOCIAL_AUTH_FACEBOOK_SCOPE = ['email']
        SOCIAL_AUTH_FACEBOOK_PROFILE_EXTRA_PARAMS = {
            'fields': 'email, first_name, last_name'
        }

        SOCIAL_AUTH_GITHUB_KEY = '[75158c04ba4ff888155f]'
        SOCIAL_AUTH_GITHUB_SECRET = '[d7844e45a9596e6e7e5170c2898144794e2675ed]'
        SOCIAL_AUTH_GITHUB_SCOPE = ['email']
        SOCIAL_AUTH_GITHUB_PROFILE_EXTRA_PARAMS = {
            'fields': 'email, first_name, last_name'
        }

urls.py:

      from django.urls import path, include  
      
      urlpatterns = [
        (...),
        path('auth/', include('djoser.urls')),
    ]
