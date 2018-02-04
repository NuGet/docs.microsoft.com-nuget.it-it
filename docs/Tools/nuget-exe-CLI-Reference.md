---
title: Riferimento di interfaccia della riga di comando (CLI) NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Indice di riferimento della riga di comando per l'interfaccia CLI di nuget.exe
keywords: indice di riferimento di NuGet.exe, interfaccia della riga di comando di nuget.exe, nuget.exe CLI, il comando di nuget
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8b1ee17702f5a54a77dc2cd663e13729a9b4a39f
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-cli-reference"></a>Riferimento a CLI NuGet

NuGet interfaccia della riga di comando (CLI), `nuget.exe`, fornisce l'entità completa di funzionalità di NuGet per installare, creare, pubblicare e gestire i pacchetti senza apportare alcuna modifica ai file di progetto.

Per utilizzare qualsiasi comando, aprire una finestra di comando o della shell bash, quindi eseguire `nuget` aggiungendo il comando e le opzioni appropriate, ad esempio `nuget help pack` (per visualizzare la Guida sul comando pack).

Questa documentazione riflette la versione più recente di NuGet CLI. Per i dettagli esatti per qualsiasi versione specificata in uso, eseguire `nuget help` per il comando desiderato.

## <a name="installing-nugetexe"></a>L'installazione di nuget.exe

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Tip]
> Per rendere disponibile all'interno della Console di gestione pacchetti NuGet CLI in Visual Studio, vedere [utilizzando nuget.exe CLI nella console di](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilità

Vedere [la disponibilità di funzionalità](../install-nuget-client-tools.md#feature-availability) per i dettagli esatti.

- Tutti i comandi sono disponibili in Windows.
- Tutti i comandi funzionano con in esecuzione in Mono tranne dove indicato per nuget.exe `pack`, `restore`, e `update`.
- Il `pack`, `restore`, `delete`, `locals`, e `push` comandi sono anche disponibili in Mac e Linux tramite dotnet CLI.

## <a name="commands-and-applicability"></a>Comandi e applicabilità

I comandi disponibili e applicabilità alla creazione del pacchetto, il consumo di pacchetto e/o la pubblicazione di un pacchetto in un host:

| Comandi comuni | Ruoli applicabili | Versione di NuGet | Descrizione |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Creazione | 2.7+ | Crea un pacchetto NuGet da un `.nuspec` o file di progetto. Quando in esecuzione in Mono, crea un pacchetto da un file di progetto non è supportato. |
| [push](cli-ref-push.md) | Pubblicazione | Tutti | Pubblica un pacchetto a un'origine pacchetto. |
| [config](cli-ref-config.md) | Tutti | Tutti | Ottiene o imposta i valori di configurazione NuGet. |
| [help o ?](cli-ref-help.md) | Tutti | Tutti | Visualizza la Guida informazioni o per un comando. |
| [locals](cli-ref-locals.md) | Utilizzo | 3.3+ | Cancella o elenca i pacchetti nella cache diverse oppure nella cartella pacchetti globale identifica le cartelle. |
| [restore](cli-ref-restore.md) | Utilizzo | 2.7+ | Ripristina tutti i pacchetti a cui fa riferimento il formato del riferimento pacchetto in uso. Quando in esecuzione in Mono, ripristino dei pacchetti utilizzando il formato PackageReference non è supportato. |
| [setapikey](cli-ref-setapikey.md) | Pubblicazione, al consumo | Tutti | Salva una chiave API per un'origine del pacchetto specificato quando l'origine del pacchetto richiede una chiave per l'accesso. |
| [spec](cli-ref-spec.md) | Creazione | Tutti | Genera un `.nuspec` file, utilizzando token se il file generato da un progetto di Visual Studio. |

| Comandi secondari | Ruoli applicabili | Versione di NuGet | Descrizione |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Pubblicazione | 3.3+ | Aggiunge un pacchetto a un'origine del pacchetto non HTTP con layout organizzato gerarchicamente. Per le origini HTTP, utilizzare *push*. |
| [delete](cli-ref-delete.md) | Pubblicazione | Tutti | Rimuove o unlists un pacchetto da un'origine del pacchetto. |
| [init](cli-ref-init.md) | Creazione | 3.3+ | Aggiunge i pacchetti da una cartella a un'origine del pacchetto con layout organizzato gerarchicamente. |
| [install](cli-ref-install.md) | Utilizzo | Tutti | Installa un pacchetto in corrente in un progetto, ma non modificare i progetti o fare riferimento ai file. |
| [list](cli-ref-list.md) | Consumo, ad esempio la pubblicazione | Tutti | Visualizza i pacchetti da un'origine specificata. |
| [mirror](cli-ref-mirror.md) | Pubblicazione | 3.2 + deprecato in | Riflette un pacchetto e le relative dipendenze da un'origine a un repository di destinazione. |
| [sources](cli-ref-sources.md) | Il consumo, pubblicazione | Tutti | Gestisce l'origine del pacchetto nel file di configurazione. |
| [update](cli-ref-update.md) | Utilizzo | Tutti | Aggiorna pacchetti di un progetto per le versioni più recenti. Non è supportato quando si esegue in Mono. |

Assicurarsi di comandi diversi utilizzano vari [le variabili di ambiente](cli-ref-environment-variables.md).

Comandi CLI NuGet dai ruoli applicabili:

| Ruolo | Comandi: |
| --- | --- |
| Utilizzo | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Creazione | `config`, `help`, `init`, `pack`, `spec` |
| Pubblicazione | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Gli sviluppatori interessati solo all'utilizzo di pacchetti, ad esempio, è necessario solo comprendere tale subset di comandi di NuGet.

> [!Note]
> I nomi delle opzioni di comando sono tra maiuscole e minuscole. Le opzioni che sono deprecate non sono inclusi in questo riferimento, ad esempio `NoPrompt` (sostituito `NonInteractive`) e `Verbose` (sostituito `Verbosity`).
