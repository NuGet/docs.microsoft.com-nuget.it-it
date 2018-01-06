---
title: Riferimento di PowerShell di NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: Il riferimento completo di comandi di PowerShell disponibili nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: NuGet package manager console comandi Powershell di NuGet, riferimento NuGet Powershell
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 64450a8bcca7f6028d4ce389d51ac35e9209cfae
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="powershell-reference"></a>Riferimento di PowerShell

La Console di gestione pacchetti fornisce un'interfaccia di PowerShell all'interno di Visual Studio in Windows per l'interazione con NuGet tramite i comandi specifici elencati di seguito. (La console non è attualmente disponibile in Visual Studio per Mac.) Per una Guida per l'utilizzo della console, vedere il [Package Manager Console](../tools/package-manager-console.md) argomento.

> [!Tip]
> Tutti i comandi PowerShell riguardano solo il consumo di pacchetto. Nessun comando di PowerShell si riferiscono alla creazione e pubblicazione di pacchetti tranne nella misura in cui un pacchetto può anche essere un utente di altri pacchetti.

> [!Important]
> I comandi elencati di seguito sono specifici per la Console di gestione dei pacchetti in Visual Studio e diversi dal [i comandi di moduli di gestione dei pacchetti](/powershell/module/packagemanagement/?view=powershell-6) che sono disponibili in un ambiente di PowerShell generale. In particolare, ogni ambiente è comandi che non sono disponibili negli altri e comandi con lo stesso nome possono anche differire nei relativi argomenti specifici. Quando si utilizza la Console di gestione di pacchetti in Visual Studio, si applicano i comandi e argomenti illustrati in questo argomento presentano.

| Comandi comuni | Descrizione | Versione di NuGet |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Installa un pacchetto e le relative dipendenze nel progetto. | Tutti |
| [Update-Package](ps-ref-update-package.md) | Aggiorna un pacchetto e le relative dipendenze o tutti i pacchetti in un progetto. | Tutti |
| [Find-Package](ps-ref-find-package.md) | Cerca un'origine del pacchetto usando un ID di pacchetto o parole chiave. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Recupera l'elenco di pacchetti installati nell'archivio locale o elenca i pacchetti disponibili dall'origine pacchetto. | Tutti |

| Comandi secondari | Descrizione | Versione di NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Esamina tutti gli assembly nel percorso di output per un progetto e aggiunge reindirizzamenti di binding di `app.config` o `web.config` in caso di necessità. | Tutti |
| [Get-Project](ps-ref-get-project.md) | Visualizza informazioni sul valore predefinito o il progetto specificato. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Avvia il browser predefinito con il progetto, licenza o report abuso URL per il pacchetto specificato. | Deprecato in 3.0 + |
| [Registro TabExpansion](ps-ref-register-tabexpansion.md) | Registra l'espansione tramite tab per i parametri di un comando, che consente di creare espansioni personalizzate per i valori dei parametri di uso comune. | Tutti |
| [Sync-Package](ps-ref-sync-package.md) | Get installata la versione del pacchetto dal progetto specificato e sincronizza la versione ai restanti progetti nella soluzione. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Rimuove un pacchetto da un progetto, rimuovere facoltativamente le relative dipendenze. | Tutti |

Per informazioni complete e dettagliate su uno di questi comandi all'interno della console, è sufficiente eseguire le operazioni seguenti con il nome del comando in questione:

```ps
Get-Help <command> -full
```

Tutti i comandi della Console di gestione pacchetti supportano i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216):

- Debug
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Dettagliato
- WarningAction
- WarningVariable

Per informazioni dettagliate, vedere [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) nella documentazione di PowerShell.
