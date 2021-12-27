# TODO

# We use .NET SDK version 6.0 for the build.
FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine  AS builder
# Run the build scripts:
#  - src/web/restore.sh
#  - src/web/build.sh
#  you'll need to make the files executable first with chmod +x <filename>.
WORKDIR /dot
COPY src/web/ .
RUN chmod +x restore.sh && ./restore.sh
RUN chmod +x build.sh && ./build.sh
# Build output is in the folder:
#  /out

# The app should run using a .NET ASP.NET 6.0 image, with a minimal OS.
FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine
# We need to set four environment variables - 
# DOTNET_VERSION and APP_VERSION - for ops usage
# Widgetario__ProductsApi__Url set to "http://products-api/products"
# Widgetario__StockApi__Url set to "http://stock-api:8080/stock"
ENV DOTNET_VERSION="6.0"\
    APP_VERSION="1.0.0"\
    Widgetario__ProductsApi__Url="http://products-api/products"\
    Widgetario__StockApi__Url="http://stock-api:8080/stock"
# The startup command needs to run the DLL from the build:
#  dotnet Widgetario.Web.dll

ENTRYPOINT ["dotnet", "/appss/Widgetario.Web.dll"]
WORKDIR /appss
COPY --from=builder /out/ .