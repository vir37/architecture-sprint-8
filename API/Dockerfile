# syntax=docker/dockerfile:1-labs

# Установить базовый образ .NET SDK для сборки
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /build

COPY Backend/Program.cs .
COPY Backend/Backend.csproj .
COPY Backend/AuthorizationResultTransformer.cs .
COPY Backend/appsettings.json .

RUN dotnet publish Backend.csproj -c Release -r linux-x64 -p:PublishSingleFile=true --self-contained false -o /out

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /out .
RUN chmod 766 ./Backend

# Expose port
EXPOSE 3000

CMD ["./Backend"]