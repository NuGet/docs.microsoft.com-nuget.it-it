---
ms.openlocfilehash: 9167b4b5943dd797c5a4cb20e53ee6832f0b3021
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623025"
---
1. <span data-ttu-id="c90c0-101">Passare alla cartella contenente il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="c90c0-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="c90c0-102">Eseguire il comando seguente, specificando il nome del pacchetto (ID pacchetto univoco) e sostituendo il valore di chiave con la chiave API:</span><span class="sxs-lookup"><span data-stu-id="c90c0-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg --api-key qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 --source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="c90c0-103">dotnet visualizza i risultati del processo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="c90c0-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="c90c0-104">Vedere [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span><span class="sxs-lookup"><span data-stu-id="c90c0-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>