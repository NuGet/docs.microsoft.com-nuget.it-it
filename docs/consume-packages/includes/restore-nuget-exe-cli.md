---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860565"
---
<span data-ttu-id="d6c56-101">Usare il comando [restore](../../reference/cli-reference/cli-ref-restore.md) che scarica e installa tutti i pacchetti mancanti dalla cartella *packages*.</span><span class="sxs-lookup"><span data-stu-id="d6c56-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="d6c56-102">Per i progetti migrati in PackageReference, usare invece [msbuild -t:restore](../package-restore.md#restore-using-msbuild) per ripristinare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d6c56-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="d6c56-103">Il comando `restore` aggiunge soltanto pacchetti su disco, ma non modifica le dipendenze di un progetto.</span><span class="sxs-lookup"><span data-stu-id="d6c56-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="d6c56-104">Per ripristinare le dipendenze del progetto, modificare `packages.config`, quindi usare il comando `restore`.</span><span class="sxs-lookup"><span data-stu-id="d6c56-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="d6c56-105">Come per gli altri comandi dell'interfaccia della riga di comando `nuget.exe`, aprire prima di tutto una riga di comando e passare alla directory che contiene il file di progetto.</span><span class="sxs-lookup"><span data-stu-id="d6c56-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="d6c56-106">Per ripristinare un pacchetto tramite `restore`:</span><span class="sxs-lookup"><span data-stu-id="d6c56-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```