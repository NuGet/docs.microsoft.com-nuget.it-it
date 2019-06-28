---
title: Riferimento di PowerShell di NuGet
description: Informazioni di riferimento complete per i comandi di PowerShell disponibili nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 977e06d36962366abd69f1c7f21ef33eca4e5029
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426129"
---
# <a name="powershell-reference"></a>Informazioni di riferimento su PowerShell

La Console di gestione pacchetti fornisce un'interfaccia di PowerShell all'interno di Visual Studio in Windows per interagire con NuGet tramite i comandi specifici elencati di seguito. (La console non è attualmente disponibile in Visual Studio per Mac.) Per una Guida all'utilizzo della console, vedere [installare e gestire i pacchetti con PowerShell](../tools/package-manager-console.md) argomento.

> [!Tip]
> Tutti i comandi di PowerShell sono correlate solo all'utilizzo di un pacchetto. I comandi di PowerShell non sono correlati alla creazione e pubblicazione di pacchetti tranne nella misura in cui un pacchetto può anche essere un consumer di altri pacchetti.

> [!Important]
> I comandi elencati di seguito sono specifici per la Console di gestione pacchetti in Visual Studio e differiscono dalle [comandi modulo Packagemanagement](/powershell/module/packagemanagement/?view=powershell-6) che sono disponibili in un ambiente di PowerShell generale. In particolare, ogni ambiente ha comandi che non sono disponibili in altro, e i comandi con lo stesso nome anche alcune possibili differenze nei relativi argomenti specifici. Quando si usa la Console di gestione pacchetti in Visual Studio, si applicano i comandi e gli argomenti illustrati in questo argomento presentano.

| Comandi comuni | Descrizione | Versione di NuGet |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Installa un pacchetto e le relative dipendenze nel progetto. | Tutti |
| [Update-Package](ps-ref-update-package.md) | Aggiorna un pacchetto e le relative dipendenze o tutti i pacchetti in un progetto. | Tutti |
| [Find-Package](ps-ref-find-package.md) | Cerca un'origine pacchetto usando un ID di pacchetto o le parole chiave. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Recupera l'elenco dei pacchetti installati nel repository locale, o elenca i pacchetti disponibili da un'origine del pacchetto. | Tutti |

| Comandi secondari | Descrizione | Versione di NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Esamina tutti gli assembly all'interno del percorso di output per un progetto e aggiunge reindirizzamenti di binding per il `app.config` o `web.config` laddove necessario. | Tutti |
| [Get-Project](ps-ref-get-project.md) | Visualizza informazioni sull'impostazione predefinita o progetto specificato. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Avvia il browser predefinito con il progetto, licenza o URL per segnalare abusi per il pacchetto specificato. | Deprecato in 3.0 e versioni successive |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | Registra un'espansione tramite tab per i parametri di un comando, consentendo la creazione di espansioni personalizzate per i valori dei parametri di uso comune. | Tutti |
| [Sync-Package](ps-ref-sync-package.md) | Get installata la versione del pacchetto dal progetto specificato e sincronizza la versione per il resto dei progetti nella soluzione. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Rimuove un pacchetto da un progetto, se lo si desidera rimuovere le relative dipendenze. | Tutti |

Per informazioni complete e dettagliate su uno di questi comandi all'interno della console, è sufficiente eseguire quanto segue con il nome del comando in questione:

```ps
Get-Help <command> -full
```

Tutti i comandi della Console di gestione pacchetti supportano le operazioni seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216):

- Debug
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Dettagliato
- WarningAction
- WarningVariable

Per informazioni dettagliate, consultare [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) nella documentazione di PowerShell.
