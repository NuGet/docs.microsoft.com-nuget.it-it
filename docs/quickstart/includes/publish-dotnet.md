---
ms.openlocfilehash: bb39e1056ea97ecf1ac70d7fd8e79e65dc04655c
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842151"
---
1. <span data-ttu-id="2735d-101">Passare alla cartella contenente il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="2735d-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="2735d-102">Eseguire il comando seguente, specificando il nome del pacchetto (ID pacchetto univoco) e sostituendo il valore di chiave con la chiave API:</span><span class="sxs-lookup"><span data-stu-id="2735d-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="2735d-103">dotnet visualizza i risultati del processo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="2735d-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="2735d-104">Vedere [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span><span class="sxs-lookup"><span data-stu-id="2735d-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>