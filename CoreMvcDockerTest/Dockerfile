#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#alttaki 6 sat?r ilk publish yapan imaj?m
#i?inde cli,runtime,asp.net core var.
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build 
WORKDIR /app
COPY *.csproj .
#nugettan ?ekilmemi? paketleri ?eker.
RUN dotnet restore 
#ilk nokta projedeki t?m dosyalar. ikincisi /app klas?r?d?r.
COPY . . 

RUN dotnet publish CoreMvcDockerTest.csproj -c Release -o out


#altdaki 3 sat?r bizim yeni imaj?m?z.
FROM mcr.microsoft.com/dotnet/aspnet:6.0
#yeni klas?r olu?turduk.
WORKDIR /app
#build kelimesi ?stteki sdk image mizin as ile belirtilen ismi.
COPY --from=build /app/out . 

ENV ASPNETCORE_URLS="http://*:4500"
ENV ASPNETCORE_ENVIRONMENT="Development"
ENV MySqlCon="Remote Sql Server"
ENTRYPOINT ["dotnet", "CoreMvcDockerTest.dll"]