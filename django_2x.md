# Django cheat-sheet

## Project x App
```
django-admin startproject <project_name> [/path/to/project]
```

cria o manage.py + pasta central do projeto /project_name/
contem as urls principais do projeto, settings.py, ...
### Ao criar um projeto deve-se:
- fazer isso
- fazer aquilo
- ...
```
django-admin startapp <project_name> [/path/to/project]
```
contém os templates, assets, views, models de cada app criado

### Ao criar um app:
- É preciso registra-lo em settings.INSTALLED_APPS
- criar as pastas de templates/ e static/ (caso necessite)
- criar o arquivo urls.py

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

- class FormView(forms.Form):

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

### Ajax GET request
Inspiração: https://www.techiediaries.com/python-django-ajax/

1. Construa uma requisição ajax get com Jquery:
https://api.jquery.com/jQuery.get/
```
$.get(
    `transactions/monthsByYear/${year}`,
    function(data){
        console.log(data.months)

        // erase .options__months childs
        $('.options__months').empty()

        // takes a json data and fill up the .options__months element
        data.months.forEach(month => {
        // build a li element with class, attribute and text
            let $li = $('<li></li>').addClass('month__item').attr("data-id", month.id).text(`${month.name}`)
            // append to the final of the .options_months element
           $('.options__months').append($li)
        });
    }
```

3. Construa uma URL com captura de argumentos:
```
path('transactions/monthsByYear/<year>', views.MonthsByYearList.as_view(), name='months_by_year'),
```

4. Construa uma view em Django/python para receber a requisição GET

**Obs: É necessário retornar uma resposta JSON.**
```
class MonthsByYearList(ListView):
    """
    receiveis a GET request and returns months json data
    according to the year choosed.
    """
    def get(self, request, *args, **kwargs):
        print(kwargs['year'])
        months = Year.objects.get(name=kwargs['year']).months.all()
        months_display = list()
        for month in months:
            # {'id': 1,'name': Janeiro}, {'id': 2, 'name': Fevereiro}...
            months_display.append(dict(id=month.id, name=month.get_month_number_display()))
        data = dict()
        data['months'] = months_display
        return JsonResponse(data)
```
Da forma que foi construida a URL, quando uma requisição GET chamar a URL com aquele padrão,
o Django ele vai capturar o elemento da URL com a keyword especificada

Por exemplo: ```[05/May/2019 17:08:30] "GET /budget_viewer/transactions/monthsByYear/18 HTTP/1.1" 200 14```

DJango vai pegar o ```18``` e guardar em um dicionário ```kwargs['year'] = 18```. Existem várias formas de acessar esse
dicionário em uma view. Uma delas está feita acima.

5. Agora é só utilizar os dados.
```
function(data){
        console.log(data.months)

        // erase .options__months childs
        $('.options__months').empty()

        // takes a json data and fill up the .options__months element
        data.months.forEach(month => {
            // build a li element with class, attribute and text
            let $li = $('<li></li>').addClass('month__item').attr("data-id", month.id).text(`${month.name}`)
            // append to the final of the .options_months element
           $('.options__months').append($li)
        });
    }
```

# Exceptions
É possível lidar com exceções criadas pelo Django importando elas de django.core.exceptions.
https://docs.djangoproject.com/en/2.1/ref/exceptions/
