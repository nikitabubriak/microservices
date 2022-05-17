#docker build -t dotnetcoreapp -f Dockerfile .
#docker image ls
#docker run -p 8080:80 --name app dotnetcoreapp
#docker ps

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /app

# Copy csproj file and restore
COPY ./*.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . .
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /app/out .
ENTRYPOINT ["dotnet", "micros.dll"]