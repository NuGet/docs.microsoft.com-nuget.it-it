---
title: Informazioni di riferimento su PowerShell per NuGet
description: Informazioni di riferimento complete per i comandi di PowerShell disponibili nella console Gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 7bc0395a98e75fe006e048b91d84cb5c17220161
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901889"
---
# <a name="powershell-reference"></a>Informazioni di riferimento su PowerShell

La console Gestione pacchetti fornisce un'interfaccia di PowerShell Visual Studio in Windows per interagire con NuGet tramite i comandi specifici elencati di seguito. La console non è attualmente disponibile in Visual Studio per Mac. Per una guida all'uso della console di , vedere [l'argomento Installare](../consume-packages/install-use-packages-powershell.md) e gestire pacchetti Gestione pacchetti console.

> [!Tip]
> Tutti i comandi di PowerShell sono correlati solo all'utilizzo dei pacchetti. Nessun comando di PowerShell riguarda la creazione e la pubblicazione di pacchetti, ad eccezione del fatto che un pacchetto può anche essere un consumer di altri pacchetti.

> [!Important]
> I comandi elencati di seguito sono specifici della console di Gestione pacchetti in Visual Studio e differiscono dai comandi del modulo [Gestione pacchetti](/powershell/module/packagemanagement) disponibili in un ambiente PowerShell generale. In particolare, ogni ambiente dispone di comandi che non sono disponibili nell'altro e i comandi con lo stesso nome possono anche differire nei relativi argomenti specifici. Quando si usa Gestione pacchetti Console in Visual Studio, si applicano i comandi e gli argomenti documentati in questo argomento.

| Comandi comuni | Descrizione | Versione di NuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Installa un pacchetto e le relative dipendenze nel progetto. | Tutti |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Aggiorna un pacchetto e le relative dipendenze o tutti i pacchetti in un progetto. | Tutti |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Esegue la ricerca in un'origine del pacchetto usando un ID pacchetto o parole chiave. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Recupera l'elenco dei pacchetti installati nel repository locale o elenca i pacchetti disponibili da un'origine pacchetto. | Tutti |

| Comandi secondari | Descrizione | Versione di NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Esamina tutti gli assembly all'interno del percorso di output per un progetto e aggiunge reindirizzamenti di associazione a `app.config` o `web.config` , se necessario. | Tutti |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Visualizza informazioni sul progetto predefinito o specificato. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Avvia il browser predefinito con il progetto, la licenza o l'URL di segnalazione di abusi per il pacchetto specificato. | Deprecato nella versione 3.0+ |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Registra un'espansione di tabulazione per i parametri di un comando, consentendo di creare espansioni personalizzate per i valori dei parametri di uso comune. | Tutti |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Ottenere la versione del pacchetto installato dal progetto specificato e sincronizzare la versione con il resto dei progetti nella soluzione. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Rimuove un pacchetto da un progetto, rimuovendo facoltativamente le relative dipendenze. | Tutti |

Per informazioni complete e dettagliate su uno di questi comandi all'interno della console, eseguire quanto segue con il nome del comando in questione:

```ps
Get-Help <command> -full
```

Tutti Gestione pacchetti comandi della console supportano i [parametri comuni di PowerShell seguenti:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)

- Debug
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Dettagliato
- WarningAction
- WarningVariable

Per informazioni dettagliate, [vedere about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) nella documentazione di PowerShell.