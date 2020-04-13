FROM mcr.microsoft.com/dotnet/core/sdk:3.1.101 AS builder
WORKDIR /source
COPY NBXplorer/NBXplorer.csproj NBXplorer/NBXplorer.csproj
COPY NBXplorer.Client/NBXplorer.Client.csproj NBXplorer.Client/NBXplorer.Client.csproj
# Cache some dependencies
RUN cd NBXplorer && dotnet restore && cd ..
COPY . .
RUN cd NBXplorer && dotnet publish -o /app/ -c Release

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1.1-buster-slim
WORKDIR /NBXplorer
RUN mkdir /NBXplorer/data
ENV NBXPLORER_DATADIR=/NBXplorer/data
COPY --from=builder "/app" .
EXPOSE 24444