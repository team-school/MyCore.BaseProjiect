FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/MyCore.BaseProject.Web.Host/MyCore.BaseProject.Web.Host.csproj", "src/MyCore.BaseProject.Web.Host/"]
COPY ["src/MyCore.BaseProject.Web.Core/MyCore.BaseProject.Web.Core.csproj", "src/MyCore.BaseProject.Web.Core/"]
COPY ["src/MyCore.BaseProject.Application/MyCore.BaseProject.Application.csproj", "src/MyCore.BaseProject.Application/"]
COPY ["src/MyCore.BaseProject.Core/MyCore.BaseProject.Core.csproj", "src/MyCore.BaseProject.Core/"]
COPY ["src/MyCore.BaseProject.EntityFrameworkCore/MyCore.BaseProject.EntityFrameworkCore.csproj", "src/MyCore.BaseProject.EntityFrameworkCore/"]
RUN dotnet restore "src/MyCore.BaseProject.Web.Host/MyCore.BaseProject.Web.Host.csproj"
COPY . .
WORKDIR "/src/src/MyCore.BaseProject.Web.Host"
RUN dotnet build "MyCore.BaseProject.Web.Host.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MyCore.BaseProject.Web.Host.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MyCore.BaseProject.Web.Host.dll"]