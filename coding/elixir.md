# String

concat
```exs
"Hello" <> " World" # Hello World
```

# Capture

&
```exs
defmodule Foo do
	def bar(x) do
		x - 1
	end
end

[1, 2] |> Enum.map(&Foo.bar/1) # Enum.map(fn x -> Foo.bar(x) end) # [0, 1]
```

# Mix
>[!info] build system

commands
```bash
# create new project
mix new <name> --module <name>
# run once
mix run
# run tests
mix test
# compile
mix compile
# release
mix release
```

# Agent
>[!info] state storage

lookup/2

# GenServer
>[!info] client-server communication

call/3

cast/2

# Supervisor
>[!info] process manager

spawn/2
spawn_link/2

# Tasks

# Node

commands
```bash
iex -sname foo
# start with custom cookie
iex -sname foo --cookie bar
```

iex
```exs
# get cookie
cookie = Node.get_cookie
# set cookie
Node.set_cookie cookie
# ping node
:net_adm.ping(:node@noname)
```