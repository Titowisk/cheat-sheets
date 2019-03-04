# Django cheat-sheet

## Project x App
```
django-admin startproject <project_name> [/path/to/project]
```

cria o manage.py + pasta central do projeto /project_name/
contem as urls principais do projeto, settings.py, ...
```
django-admin startapp <project_name> [/path/to/project]
```
contém os templates, assets, views, models de cada app criado

## Shell
```
py manage.py shell
```
Permite brincar com os modelos criados em models.py de cada app

## makemigrations x migrate
```
py manage.py makemigrations
```
cria o código para alteração da tabela, baseada no que é encontrado em models.py de cada app
```
py manage.py migrate
```
executa as alterações

## Views
### Class-based-views

## Templates

## Models

## GET x POST

### Upload Files
