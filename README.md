# api_auth2


settings.py

add installed apps
INSTALLED_APPS = [
    ...
    'rest_framework',
    'djoser',
    'aacounts',
    'social_django', 

    'rest_framework_simplejwt',
    'rest_framework_simplejwt.token_blacklist',
]    
 
 add one piece of middleware
 MIDDLEWARE = [
    'social_django.middleware.SocialAuthExceptionMiddleware'
    ...
 ]
    
