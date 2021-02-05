# api_auth2


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
     

