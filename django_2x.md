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
https://ccbv.co.uk/ um site que facilita ver toda a árvore de classes com seus atributos e métodos

class FormView(forms.Form):

Cada field do forms.Form possuem widgets (código HTML) de formulários web.

## Templates
É necessário criar a pasta /templates/ dentro da pasta do app
O django recomenda dessa forma:

```app_name/templates/app_name/```

E quando for utilizar o template colocar:

```"app_name/template.html"```

## Models

## GET x POST


### Upload Files
Para trabalhar com importação de arquivos é preciso utilizar formulários.

1 - criar forms.py:
funciona como um models.py, só que para classes que herdam de forms.Form ao invés de models.Model

2 - criar uma view para lidar com a página que contém o forumlário e com a requisição de POST que será enviada:
```
class ReadFilesView(FormView):
    template_name = "bank_statements_reader/csv_reader.html"
    success_url = "sample_statement_table"
    form_class = UploadFileForm


    def post(self, request, *args, **kwargs):
        """
        Handle POST requests: instantiate a form instance with the passed
        POST variables and then check if it's valid.
        """
        form_class = self.get_form_class()
        form = self.get_form(form_class)
        file = request.FILES['file']
        if form.is_valid():
            transactions = read_csv_file(file)
            for t_dict in transactions:
                create_transaction(t_dict)

            return self.form_valid(form)
        else:
            return self.form_invalid(form)
```
Informações enviadas por POST ficam em request.POST (um dicionário).
No caso de arquivos é request.FILES.
!!!
Quando a página é acessada, ele cai no caso do ```.form_invalid(form)```
```
def form_invalid(self, form):
    """If the form is invalid, render the invalid form."""
    return self.render_to_response(self.get_context_data(form=form))
```
que pega o código HTML gerado pelo ```UploadFileForm``` para criar o 
formulário-ligado na página em questão.
!!!
