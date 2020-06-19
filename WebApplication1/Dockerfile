FROM ashish1981/s390x-clefos-mono AS base
WORKDIR /app
EXPOSE 8080
EXPOSE 8443

FROM ashish1981/s390x-clefos-mono AS build
WORKDIR /src
COPY ["WebApplication1/WebApplication1.csproj", "WebApplication1/"]
#RUN mono restore "WebApplication1/WebApplication1.csproj"
COPY . .
WORKDIR "/src/WebApplication1"
RUN mono build "WebApplication1.csproj" -c Release -o /app

FROM build AS publish
RUN mono publish "WebApplication1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["mono", "WebApplication1.dll"]