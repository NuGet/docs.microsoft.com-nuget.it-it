---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860565"
---
Usare il comando [restore](../../reference/cli-reference/cli-ref-restore.md) che scarica e installa tutti i pacchetti mancanti dalla cartella *packages*.

Per i progetti migrati in PackageReference, usare invece [msbuild -t:restore](../package-restore.md#restore-using-msbuild) per ripristinare i pacchetti.

Il comando `restore` aggiunge soltanto pacchetti su disco, ma non modifica le dipendenze di un progetto. Per ripristinare le dipendenze del progetto, modificare `packages.config`, quindi usare il comando `restore`.

Come per gli altri comandi dell'interfaccia della riga di comando `nuget.exe`, aprire prima di tutto una riga di comando e passare alla directory che contiene il file di progetto.

Per ripristinare un pacchetto tramite `restore`:

```cli
nuget restore MySolution.sln
```