1. <span data-ttu-id="f83a1-101">Passare alla cartella contenente il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="f83a1-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="f83a1-102">Eseguire il comando seguente, specificando il nome del pacchetto e sostituendo il valore di chiave con la chiave API:</span><span class="sxs-lookup"><span data-stu-id="f83a1-102">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="f83a1-103">dotnet visualizza i risultati del processo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="f83a1-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="f83a1-104">Vedere [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span><span class="sxs-lookup"><span data-stu-id="f83a1-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>