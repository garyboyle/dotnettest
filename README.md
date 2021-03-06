# .Net Test Project

A sample C# project to work out the development environment.

This project was created using the `dotnet new webapi` [.NET CLI command](https://docs.microsoft.com/en-us/dotnet/core/tools/) with the .NET Core 3.1 SDK.

Use the `dotnet run` command to run the project.  To watch for changes run `dotnet watch run`.

The `global.json` file determines what .NET SDK should be used.  This is similar in behaviour to a `.nvmrc` file.  More information here: https://docs.microsoft.com/en-us/dotnet/core/versions/selection#the-sdk-uses-the-latest-installed-version

## Useful links
- [VS Code: Working with C#](https://code.visualstudio.com/docs/languages/csharp)
- [VS Code: Using .NET Core in Visual Studio Code](https://code.visualstudio.com/docs/languages/dotnet)
- [VS Code: Create a .NET console application using Visual Studio Code](https://docs.microsoft.com/en-us/dotnet/core/tutorials/with-visual-studio-code#debug)
- [VS Code: Debug a .NET console application using Visual Studio Code](https://docs.microsoft.com/en-us/dotnet/core/tutorials/debugging-with-visual-studio-code)
- [Get started with VS Code using C# and .NET Core on Windows](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows)
- [Containerize a .NET Core app](https://docs.microsoft.com/en-us/dotnet/core/docker/build-container?tabs=windows)
- [Deploying to a Digital Ocean Droplet](https://stackabuse.com/deploying-a-node-js-app-to-a-digitalocean-droplet-with-docker/)

# Docker

The project can be started as a container.  The `Dockerfile` is based heavily on the  [Dockerize an ASP.NET Core application](https://docs.docker.com/engine/examples/dotnetcore/) article from Docker docs.

To create an image run `docker build -t dotnet-test .`
To run the image run `docker run -d -p 8080:80 --name myapp dotnet-test`

Or, with docker compose, run `docker-compose up`

# Scripting

Install: `dotnet tool install --global dotnet-script`

Create a script: `dotnet script init hello`

Runn the script: `dotnet script hello.csx`

[C# scripts using dotnet-script](https://galdin.dev/blog/csharp-scripts-using-dotnet-script/)

# Node commands/file equivalents in .NET

|node.js                         |.NET                                            |
|--------------------------------|------------------------------------------------|
|`nodemon`                       |`dotnet watch run`                              |
|`npm start`                     |`dotnet run`                                    |
|`npm build --production`        |`dotnet publish -c Release`                     |
|`.nvmrc`                        |`global.json`                                   |
|`npm i <package-name>`          |`dotnet add package <package-name>`             |
|`npm i <package-name>@<version>`|`dotnet add package <package-name> -v <version>`|
|`npm i`                         |`dotnet restore`                                |
|`nvm ls`                        |`dotnet --list-sdks`                            |
|`node test.js`                  |`dotnet dotnettest.dll`                         |

# Continuous Integration & Continuous Deployment
The app is configured to use [Travis CI](https://www.travis-ci.com/github/garyboyle/dotnettest).

On a commit to main Travis will:
1. build the latest image
2. push this image to [docker hub](https://hub.docker.com/r/shayoo/dotnettest)
3. deploy this to image to AWS Elastic Beanstalk
