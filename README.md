# Blazor
# Criar um aplicativo de lista de tarefas com blazor
## Pré-requisitos

[.NET Core 3.1 SDK ou posterior](https://dotnet.microsoft.com/download/dotnet-core/3.1)

[VS CODE](https://code.visualstudio.com/Download)

1 - Crie um novo aplicativo Blazor chamado Todos:

```C#
dotnet new blazorserver -o Todos
```
1.1 Com o projeto criado navegue até a pasta do projeto:
```
cd Todos
``` 

2 - Crie um novo componente

```C#
dotnet new razorcomponent -n Todo -o Pages
```
3 - Criar modelo TodoItem.cs na raiz do projeto
```
public class TodoItem
{
    public string Title { get; set; }
    public bool IsDone { get; set; }
}
```

4 - Adicione o componente Todo à barra de navegação (Shared/NavMenu.razor).

```
<li class="nav-item px-3">
    <NavLink class="nav-link" href="todo">
        <span class="oi oi-list-rich" aria-hidden="true"></span> Todo
    </NavLink>
</li>
```

5 - Abra o componente todo Pages/Todo.razor:

```html
@page "/todos"

<h3>Todo (@todos.Count(todo => !todo.IsDone))</h3>

<ul>
    @foreach (var todo in todos)
    {
        <li>
            <input type="checkbox" @bind="todo.IsDone" />
            <input @bind="todo.Title" />
        </li>
    }
</ul>

<input placeholder="Something todo" @bind="newTodo" />
<button @onclick="AddTodo">Add todo</button>

@code {
    private IList<TodoItem> todos = new List<TodoItem>();
    private string newTodo;

    private void AddTodo()
    {
        if (!string.IsNullOrWhiteSpace(newTodo))
        {
            todos.Add(new TodoItem { Title = newTodo });
            newTodo = string.Empty;
        }
    }
}

```
6 - Execute o projeto:

```C#
dotnet run
```


