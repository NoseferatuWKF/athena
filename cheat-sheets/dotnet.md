[dev-cert](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-dev-certs)
```bash
# remove existing certs
dotnet dev-certs https --clean
# create new cert for localhost
dotnet dev-certs https --trust
# import existing cert for localhost
dotnet dev-certs https --clean -i /path/to/file.pfx -p password
```

start server
```bash
dotnet run --project /path/to/project.csproj
# with HMR
dotnet watch -lp <profile>
# start server with url, ie; http://0.0.0.0
dotnet run --urls <ip> # can also use with dll
```

reference
```bash
dotnet add <project> reference <another-project>
```

package
```bash
dotnet add package <package>
dotnet remove package <package>
dotnet list package
```

build
```bash
dotnet build -ts # list all target
dotnet build -t:<target> # execute target tasks
dotnet build -preprocess # dump source without building
```