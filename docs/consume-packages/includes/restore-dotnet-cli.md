---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825152"
---
Usare il comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) che ripristina i pacchetti elencati nel file di progetto (vedere [PackageReference](../../consume-packages/package-references-in-project-files.md)). Con .NET Core 2.0 e versioni successive, il ripristino viene eseguito automaticamente con `dotnet build` e `dotnet run`. A partire da NuGet 4.0, esegue lo stesso codice di `nuget restore`.

Come per gli altri comandi dell'interfaccia della riga di comando `dotnet`, aprire prima di tutto una riga di comando e passare alla directory che contiene il file di progetto.

Per ripristinare un pacchetto tramite `dotnet restore`:

```dotnetcli
dotnet restore 
```