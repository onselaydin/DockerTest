#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#alttaki 6 satýr ilk publish yapan imajým
#içinde cli,runtime,asp.net core var.
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build 
WORKDIR /app
COPY *.csproj .
#nugettan çekilmemiþ paketleri çeker.
RUN dotnet restore 
#ilk nokta projedeki tüm dosyalar. ikincisi /app klasörüdür.
COPY . . 

RUN dotnet publish CoreMvcDockerTest.csproj -c Release -o out


#altdaki 3 satýr bizim yeni imajýmýz.
FROM mcr.microsoft.com/dotnet/aspnet:6.0
#yeni klasör oluþturduk.
WORKDIR /app
#build kelimesi üstteki sdk image mizin as ile belirtilen ismi.
COPY --from=build /app/out . 

ENV ASPNETCORE_URLS="http://*:4500"
ENV ASPNETCORE_ENVIRONMENT="Development"
ENV MySqlCon="Remote Sql Server"
ENTRYPOINT ["dotnet", "CoreMvcDockerTest.dll"]