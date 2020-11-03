---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825152"
---
<span data-ttu-id="d6a8e-101">Usare il comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) che ripristina i pacchetti elencati nel file di progetto (vedere [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="d6a8e-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="d6a8e-102">Con .NET Core 2.0 e versioni successive, il ripristino viene eseguito automaticamente con `dotnet build` e `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="d6a8e-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="d6a8e-103">A partire da NuGet 4.0, esegue lo stesso codice di `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="d6a8e-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="d6a8e-104">Come per gli altri comandi dell'interfaccia della riga di comando `dotnet`, aprire prima di tutto una riga di comando e passare alla directory che contiene il file di progetto.</span><span class="sxs-lookup"><span data-stu-id="d6a8e-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="d6a8e-105">Per ripristinare un pacchetto tramite `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="d6a8e-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```