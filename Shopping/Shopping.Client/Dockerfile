#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["Shopping.Client/Shopping.Client.csproj", "Shopping.Client/"]
RUN dotnet restore "Shopping.Client/Shopping.Client.csproj"
COPY . .
WORKDIR "/src/Shopping.Client"
RUN dotnet build "Shopping.Client.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Shopping.Client.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Shopping.Client.dll"]

# Download and install the Tracer
RUN mkdir -p /opt/datadog

# Enable the tracer
ENV CORECLR_ENABLE_PROFILING=1
ENV CORECLR_PROFILER={846F5F1C-F9AE-4B07-969E-05C26BC060D8}
ENV CORECLR_PROFILER_PATH=/opt/datadog/Datadog.Trace.ClrProfiler.Native.so
ENV DD_DOTNET_TRACER_HOME=/opt/datadog
