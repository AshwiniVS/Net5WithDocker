# Get the base image
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build-env

WORKDIR /app

# Copy the csproj and restore all of the nugets
COPY /WebAPI/*.csproj ./
RUN dotnet restore 

# Copy everything else and build
COPY . ./
RUN dotnet publish WebAPI -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/sdk:5.0 As base
WORKDIR /app
COPY --from=build-env /app/out .
ENV ASPNETCORE_URLS=http://+80
EXPOSE 80
ENTRYPOINT ["dotnet", "WebAPI.dll"]