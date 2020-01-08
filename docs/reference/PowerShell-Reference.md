---
title: Informazioni di riferimento su NuGet PowerShell
description: Il riferimento completo ai comandi di PowerShell disponibili nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 2a82b1977265a8f8a15247759bc3de80a5efe228
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385343"
---
# <a name="powershell-reference"></a>Informazioni di riferimento su PowerShell

La console di gestione pacchetti fornisce un'interfaccia di PowerShell all'interno di Visual Studio in Windows per interagire con NuGet tramite i comandi specifici elencati di seguito. La console non è attualmente disponibile in Visual Studio per Mac. Per una guida all'uso della console di, vedere l'argomento relativo alla procedura di [installazione e gestione dei pacchetti tramite la console di gestione pacchetti](../consume-packages/install-use-packages-powershell.md) .

> [!Tip]
> Tutti i comandi di PowerShell sono correlati solo al consumo del pacchetto. Nessun comando di PowerShell è correlato alla creazione e alla pubblicazione di pacchetti, tranne nella misura in cui un pacchetto può essere anche un consumer di altri pacchetti.

> [!Important]
> I comandi elencati di seguito sono specifici della console di gestione pacchetti in Visual Studio e si differenziano dai [comandi del modulo Gestione pacchetti](/powershell/module/packagemanagement/?view=powershell-6) disponibili in un ambiente PowerShell generale. In particolare, in ogni ambiente sono presenti comandi che non sono disponibili nell'altra e i comandi con lo stesso nome potrebbero differire anche per gli argomenti specifici. Quando si usa la console di Gestione pacchetti in Visual Studio, vengono applicati i comandi e gli argomenti illustrati in questo argomento.

| Comandi comuni | Descrizione | Versione di NuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Installa un pacchetto e le relative dipendenze nel progetto. | Tutte le |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Aggiorna un pacchetto e le relative dipendenze o tutti i pacchetti in un progetto. | Tutte le |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Cerca un'origine del pacchetto usando un ID o parole chiave del pacchetto. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Recupera l'elenco dei pacchetti installati nel repository locale oppure elenca i pacchetti disponibili da un'origine del pacchetto. | Tutte le |

| Comandi secondari | Descrizione | Versione di NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Esamina tutti gli assembly nel percorso di output di un progetto e aggiunge i reindirizzamenti di binding al `app.config` o `web.config` laddove necessario. | Tutte le |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Visualizza le informazioni relative al progetto predefinito o specificato. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Avvia il browser predefinito con l'URL del progetto, della licenza o dell'abuso del report per il pacchetto specificato. | Deprecato in 3.0 + |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Registra un'espansione di tabulazione per i parametri di un comando, consentendo di creare espansioni personalizzate per i valori di parametro usati comunemente. | Tutte le |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Ottenere la versione del pacchetto installato dal progetto specificato e sincronizzare la versione con il resto dei progetti nella soluzione. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Rimuove un pacchetto da un progetto, rimuovendo facoltativamente le relative dipendenze. | Tutte le |

Per una guida completa e dettagliata su uno di questi comandi all'interno della console di, è sufficiente eseguire il comando seguente con il nome del comando in questione:

```ps
Get-Help <command> -full
```

Tutti i comandi della console di gestione pacchetti supportano i seguenti [parametri comuni di PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216):

- Debug
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Dettagliato
- WarningAction
- WarningVariable

Per informazioni dettagliate, vedere [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216) nella documentazione di PowerShell.
