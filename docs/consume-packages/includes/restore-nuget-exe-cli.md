---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
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