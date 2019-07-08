## Ecto Friends

##### A simple Elixir application based on the [Ecto Getting Started](https://hexdocs.pm/ecto/getting-started.html) guide.

#### What is Ecto?
Ecto is a database wrapper and query generator for Elixir.  It allows an Elixir application to interact with a SQL database such as Postgres (default) or MySQL.
You can use it for all CRUD type operations such as creating, reading, updating or destroying a database record.  

### Notes:
- ensure your app has a supervision tree when you run the mix generator....
```
  mix new <YOUR_APP> --sup
```
- add Ecto and Postgrex driver as dependencies insode your mix.exs file and then run `mix deps.get`
```
  defp deps do
    [
      {:ecto_sql, "~> 3.0"},
      {:postgrex, ">= 0.0.0"}
    ]
  end
```
- Configure the database by running `mix ecto.gen.repo -r <YOUR_APP>.Repo`

- Setup the repo as a supervisor in the app's supervisor tree by adding the following to your `application.ex`
```
def start(_type, _args) do
    # List all child processes to be supervised
    children = [
      # Starts a worker by calling: <YOUR_APP>.Worker.start_link(arg)
      # {<YOUR_APP>.Worker, arg}

      # Setup <YOUR_APP>.Repo as a supervisor within the apps supervision tree
      <YOUR_APP>.Repo
    ]

    opts = [strategy: :one_for_one, name: <YOUR_APP>.Supervisor]
    Supervisor.start_link(children, opts)
  end
```
- next create the database by running `mix ecto.create`
- ...and run a migration `mix ecto.gen.migration create_<TABLE_NAME>`
- NOTE:  The convention is to name the table plural and the records singular i.e. name the table people and each record is a person.




