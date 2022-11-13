pip install django psycopg2 python-decouple djangorestframework
django admin startproject test_rest .
python manage.py runserver (8080 --> change the default port)
python manage.py startapp myapp
python manage.py makemigrations
python manage.py migrate

templates --> index.html
app --> views.py

def myview(request):
    return render(request, "index.html")

app --> urls.py

from django.urls import path
from . import views

urlpatterns = [
    path('myview/', views.myview)
]

# Configurar PostgreSQL

project --> settings.py --> DATABASES --> 'default':
'ENGINE': 'django.db.backends.postgresql',
'NAME': '',
'USER': '',
'PASSWORD': '',
'HOST': '',
'PORT': ''

# Configurar RestAPI

em settings.py colocar 'rest_framework' dentro de INSTALLED_APPS

criar pasta api, criar arquivo __init__.py
criar arquivo views.py e colocar o seguinte conteúdo:
######
from rest_framework.response import Response
from rest_framework.decorators import api_view

@api_view(['GET'])
def getData(request):
    person = {'name': 'Thiago', 'age': 20}
    return Response(person)
######
criar arquivo urls.py e colocar o seguinte conteúdo:
######

######
dentro do arquivo urls.py do projeto importar a função include do django.urls e adicionar as urls da api dentro dos urlpatterns:
path('', include('api.urls')),