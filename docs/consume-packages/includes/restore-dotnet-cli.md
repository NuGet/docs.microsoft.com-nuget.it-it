---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825152"
---
Usare il comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) che ripristina i pacchetti elencati nel file di progetto (vedere [PackageReference](../../consume-packages/package-references-in-project-files.md)). Con .NET Core 2.0 e versioni successive, il ripristino viene eseguito automaticamente con `dotnet build` e `dotnet run`. A partire da NuGet 4.0, esegue lo stesso codice di `nuget restore`.

Come per gli altri comandi dell'interfaccia della riga di comando `dotnet`, aprire prima di tutto una riga di comando e passare alla directory che contiene il file di progetto.

Per ripristinare un pacchetto tramite `dotnet restore`:

```dotnetcli
dotnet restore 
```