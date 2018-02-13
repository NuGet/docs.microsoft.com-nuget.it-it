1. Passare alla cartella contenente il file `.nupkg`.

1. Eseguire il comando seguente, specificando il nome del pacchetto e sostituendo il valore di chiave con la chiave API:

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. dotnet visualizza i risultati del processo di pubblicazione:

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

Vedere [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).