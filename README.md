# template-net-core
Template de un proyecto de .NET Core

# Tecnologías
- .NET Core 3.1 (versión soportada por Google Cloud)
- Web API y Web App
- Swagger activado
- DB en memoria

# Integración con Google Cloud

## Instalación

- Instalar un python 3.5 a 3.8, y 2.7.9 o superior.
- Bajar el Google Cloud SDK:
curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-317.0.0-linux-x86_64.tar.gz
- Instalar el SDK:
./google-cloud-sdk/install.sh
- Incializar el SDK:
./google-cloud-sdk/bin/gcloud init

## Crear una aplicación

- Actualizar el SDK:
```
./google-cloud-sdk/bin/gcloud components update
```
- Crear el proyecto "figure-factory"
```
./google-cloud-sdk/bin/gcloud projects create figure-factory --set-as-default
```
- Comprobar que se creó el proyecto "figure-factory":
```
./google-cloud-sdk/bin/gcloud projects describe figure-factory
```
- Inicializar la app de App Engine con el proyecto
```
./google-cloud-sdk/bin/gcloud app create --project=figure-factory
```

## Deploy

- Agregar estas líneas al archivo de config del proyecto Web (*.csproj):
```
  <ItemGroup>
    <None Update="app.yaml">
      <CopyToPublishDirectory>PreserveNewest</CopyToPublishDirectory>
    </None>
  </ItemGroup>
```
- Armar el bundle:
```
dotnet publish -c Release
```
- Deploy:
```
gcloud app deploy ./src/AspnetRun.Web/bin/Release/netcoreapp3.1/publish/app.yaml
```

# Endpoints
https://localhost:5001/WeatherForecast -- API

https://localhost:5001/swagger/index.html -- Test APIs

https://localhost:5001/Product -- Web

https://figure-fact.rj.r.appspot.com/ -- App en Google Cloud
