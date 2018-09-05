---
title: Riferimento dell'interfaccia della riga di comando (CLI) di NuGet
description: Indice di riferimento della riga di comando per nuget.exe CLI
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 2743dde63487124c706f2b1521ef2c6c3b28339d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548078"
---
# <a name="nuget-cli-reference"></a>Riferimento di NuGet CLI

NuGet interfaccia della riga di comando (CLI), `nuget.exe`, fornisce l'ambito completo di funzionalità di NuGet per installare, creare, pubblicare e gestire i pacchetti senza apportare alcuna modifica ai file di progetto.

Per utilizzare qualsiasi comando, aprire una finestra di comando o bash shell, quindi eseguire `nuget` seguito dal comando e opzioni appropriate, ad esempio `nuget help pack` (per visualizzare la Guida sul comando pack).

Questa documentazione riflette la versione più recente di NuGet CLI. Per informazioni dettagliate esatte per qualsiasi versione in uso, eseguire `nuget help` per il comando desiderato.

## <a name="installing-nugetexe"></a>Installazione nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Per rendere disponibili all'interno della Console di gestione pacchetti NuGet CLI in Visual Studio, vedere [tramite la CLI nuget.exe nella console di](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilità

Visualizzare [la disponibilità di funzionalità](../install-nuget-client-tools.md#feature-availability) per tutti i dettagli.

- Tutti i comandi sono disponibili in Windows.
- Tutti i comandi operano con in esecuzione in Mono, ad eccezione di dove indicato per nuget.exe `pack`, `restore`, e `update`.
- Il `pack`, `restore`, `delete`, `locals`, e `push` comandi sono disponibili anche in Mac e Linux tramite la riga di comando di dotnet.

## <a name="commands-and-applicability"></a>I comandi e l'applicabilità

I comandi disponibili e l'applicabilità alla creazione del pacchetto, l'utilizzo di un pacchetto / pubblicazione di un pacchetto in un host:

| Comandi comuni | Ruoli applicabili | Versione di NuGet | Descrizione |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Creazione | 2.7+ | Crea un pacchetto NuGet da una `.nuspec` o file di progetto. Durante l'esecuzione in Mono, creazione di un pacchetto da un file di progetto non è supportata. |
| [push](cli-ref-push.md) | Pubblicazione | Tutti | Pubblica un pacchetto di un'origine del pacchetto. |
| [config](cli-ref-config.md) | Tutti | Tutti | Ottiene o imposta i valori di configurazione NuGet. |
| [help or ?](cli-ref-help.md) | Tutti | Tutti | Visualizza la Guida informazioni o assistenza per un comando. |
| [locals](cli-ref-locals.md) | Utilizzo | 3.3+ | Elenca le località POP della *global-packages*, *http-cache*, e *temp* cartelle e cancella il contenuto di tali cartelle. |
| [restore](cli-ref-restore.md) | Utilizzo | 2.7+ | Ripristina tutti i pacchetti di cui fa riferimento il formato di gestione pacchetti in uso. Durante l'esecuzione in Mono, non è supportato il ripristino dei pacchetti usano il formato PackageReference. |
| [setapikey](cli-ref-setapikey.md) | Pubblicazione, al consumo | Tutti | Salva una chiave API per un'origine del pacchetto specificata quando tale origine del pacchetto richiede una chiave per l'accesso. |
| [spec](cli-ref-spec.md) | Creazione | Tutti | Genera un `.nuspec` file, utilizzando token se il file generato da un progetto di Visual Studio. |

| Comandi secondari | Ruoli applicabili | Versione di NuGet | Descrizione |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Pubblicazione | 3.3+ | Aggiunge un pacchetto a un'origine di pacchetti non HTTP tramite layout organizzato gerarchicamente. Per le origini HTTP, usare *push*. |
| [delete](cli-ref-delete.md) | Pubblicazione | Tutti | Rimuove o elimina un pacchetto da un'origine del pacchetto. |
| [init](cli-ref-init.md) | Creazione | 3.3+ | Consente di aggiungere pacchetti da una cartella a un'origine pacchetto tramite layout organizzato gerarchicamente. |
| [install](cli-ref-install.md) | Utilizzo | Tutti | Installa un pacchetto in corrente in un progetto, ma non modifica i progetti o fare riferimento ai file. |
| [list](cli-ref-list.md) | Utilizzo, ad esempio la pubblicazione | Tutti | Consente di visualizzare i pacchetti da un'origine specificata. |
| [mirror](cli-ref-mirror.md) | Pubblicazione | 3.2 + deprecato in | Riflette un pacchetto e le relative dipendenze da un'origine a un repository di destinazione. |
| [sources](cli-ref-sources.md) | Il consumo, pubblicazione | Tutti | Gestisce le origini di pacchetti nei file di configurazione. |
| [update](cli-ref-update.md) | Utilizzo | Tutti | Aggiorna pacchetti del progetto per le versioni più recenti disponibili. Non è supportato durante l'esecuzione in Mono. |

Assicurarsi di comandi diversi usano vari [variabili di ambiente](cli-ref-environment-variables.md).

Comandi CLI di NuGet da ruoli applicabili:

| Ruolo | Comandi: |
| --- | --- |
| Utilizzo | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Creazione | `config`, `help`, `init`, `pack`, `spec` |
| Pubblicazione | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Gli sviluppatori interessati solo con l'utilizzo dei pacchetti, ad esempio, necessitano solo comprendere tale subset di comandi NuGet.

> [!Note]
> I nomi delle opzioni di comando sono tra maiuscole e minuscole. Le opzioni che sono deprecate non sono inclusi in questo riferimento, ad esempio `NoPrompt` (sostituito da `NonInteractive`) e `Verbose` (sostituito da `Verbosity`).
