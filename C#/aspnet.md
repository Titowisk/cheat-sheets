# ASP.NET
O ASP.NET é um framework web grátis para a criação de ótimos sites e aplicativos web usando HTML, CSS e
JavaScript. Você também pode criar APIs da Web e usar tecnologias em tempo real como Web Sockets.

## Personalizing the IDE
You can customize the window layout to fit your development style. 
You can dock, float or hide any window at any time, and you also can run the editor in full-screen mode. 
You can create and save multiple custom window layouts that show only the windows you need for specific contexts.
For example, you can create a full-screen layout so that all you see is the code editor. And you can create different 
layouts for debugging and for team operations. For more information, see Customizing window layouts.
You can customize Visual Studio in many other ways, and roam your settings if you work on multiple machines.
For more information, see Personalizing the IDE.
There are keyboard shortcuts for almost everything, and you can customize them as well. 
To create new shortcuts, type "Keyboard" in Quick Launch to open the Keyboard dialog box.
From there, you can press F1 to go to the MSDN help page if you need more information about the options. 
For more information, see Default Keyboard Shortcuts in Visual Studio.

## Connecting to Visual Studio Team Services and Team Foundation Server
Visual Studio Team Services (VSTS) is a cloud-based service for hosting software projects and enabling collaboration 
in teams. VSTS supports both Git and Team Foundation Source Control systems, as well as Scrum, CMMI and Agile development methodologies.

## ASP Pages
https://docs.microsoft.com/en-us/previous-versions/aspnet/k33801s3(v=vs.100)

## Web Server Controls:
https://docs.microsoft.com/en-us/previous-versions/aspnet/zsyt68f1%28v%3dvs.100%29 (Overview)

Indice de Web Server Controls:
https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-3.0/fxh7k08z(v=vs.85)

## Themas e Estilo (CSS):
https://docs.microsoft.com/en-us/previous-versions/aspnet/wcyt4fxb%28v%3dvs.100%29

## WebForms

Em WebForms eu tenho que definir como serão os modelos em uma pasta ```models```, como os modelos se comunicam
com o banco de dados em uma pasta ```DAO```, as configurações de conexão em ```Web.config``` e também definir
as páginas do projeto com tags ```<asp:WebControlName Prop1="Value1" ... />```.

O estilo e a arrumação é veita nessas páginas do WebForms, eu tenho que definir os nomes dos métodos que vão
acionar as ações do CRUD (create, read, update e delete). Nessas páginas eu misturo código ```html``` e
tags ```<asp>```.

# LifeCycle
Começa invocando o HTTP'Handler que instancia a hierarquia de controles (control hierarchy) e após isso vem as fases de
```Initialization```, ```LoadViewState```, ```LoadPostBackData```, ```Load```, ```RaisePostBackEvent```, 
```SaveViewState```, ```Render``` e retorna ao HTTP handler para enviar para o cliente.



### ViewState:
https://docs.microsoft.com/en-us/previous-versions/dotnet/articles/ms972976(v=msdn.10)#the-role-of-view-state
Serve para armazenar informações que precisam ser persistidas ao longo do ciclo de vida do projeto.
**Importante lembrar** que informações de ```Web Controls``` são salvas através de PostBacks na por causa que
suas classes implementa o ```IPostBackDataHandler``` que exige o método ```loadPostData()``` que salva
informações inseridas pelos usuários em ```Web Controls```




**Obs: Erro 403 ao compilar**: acontece porque eu não setei qual a página que irá servir de StartUp page e também
qual projeto irá servir de StartUp Project (nas configurações do Visual Studio).

**Obs:** ```<% %>``` é um code render:

https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-4.0/k6xeyd4z(v=vs.100)

## Visual Studio 2015
https://docs.microsoft.com/pt-br/visualstudio/ide/visual-studio-ide?view=vs-2015
