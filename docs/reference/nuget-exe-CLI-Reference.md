---
title: Guida di riferimento all'interfaccia della riga di comando (CLI) NuGet
description: Indice di riferimento della riga di comando per l'interfaccia della riga di comando nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: e9343f1fdddcf839322849925372587e685aef4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623149"
---
# <a name="nuget-cli-reference"></a>Informazioni di riferimento sull'interfaccia della riga di comando di NuGet

L'interfaccia della riga di comando di NuGet, `nuget.exe` , fornisce l'ambito completo della funzionalità NuGet per l'installazione, la creazione, la pubblicazione e la gestione dei pacchetti senza apportare modifiche ai file di progetto.

Per usare qualsiasi comando, aprire una finestra di comando o una shell bash, quindi eseguire `nuget` seguito dal comando e dalle opzioni appropriate, ad esempio `nuget help pack` (per visualizzare la guida sul comando Pack).

Questa documentazione rispecchia la versione più recente dell'interfaccia della riga di comando di NuGet. Per informazioni dettagliate esatte su una determinata versione in uso, eseguire `nuget help` per il comando desiderato.

Per informazioni su come usare i comandi di base con l'interfaccia della riga di comando di `nuget.exe`, vedere [Installare e usare pacchetti tramite l'interfaccia della riga di comando di nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Installazione di nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Per rendere l'interfaccia della riga di comando di NuGet disponibile nella console di gestione pacchetti in Visual Studio, vedere [uso dell'interfaccia della riga di comando nuget.exe nella console di](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilità

Per informazioni dettagliate, vedere [disponibilità delle funzionalità](../install-nuget-client-tools.md#feature-availability) .

- Tutti i comandi sono disponibili in Windows.
- Tutti i comandi funzionano con nuget.exe eseguiti in mono, tranne nei casi indicati per `pack` , `restore` e `update` .
- I `pack` `restore` comandi,, `delete` , `locals` e `push` sono disponibili anche in Mac e Linux tramite l'interfaccia della riga di comando di DotNet.

## <a name="commands-and-applicability"></a>Comandi e applicabilità

Comandi e applicabilità disponibili per la creazione di pacchetti, l'utilizzo di pacchetti e/o la pubblicazione di un pacchetto in un host:

| Comandi comuni | Ruoli applicabili | Versione di NuGet | Descrizione |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | Creazione | 2.7+ | Crea un pacchetto NuGet da un `.nuspec` file di progetto o. Quando è in esecuzione in mono, la creazione di un pacchetto da un file di progetto non è supportata. |
| [push](cli-reference/cli-ref-push.md) | Pubblicazione | Tutti | Pubblica un pacchetto in un'origine del pacchetto. |
| [config](cli-reference/cli-ref-config.md) | Tutti | Tutti | Ottiene o imposta i valori di configurazione NuGet. |
| [help or ?](cli-reference/cli-ref-help.md) | Tutti | Tutti | Visualizza informazioni della guida o la guida per un comando. |
| [locals](cli-reference/cli-ref-locals.md) | Consumo | 3.3 + | Elenca i percorsi delle cartelle *Global-Packages*, *http-cache*e *Temp* e cancella il contenuto di tali cartelle. |
| [restore](cli-reference/cli-ref-restore.md) | Consumo | 2.7+ | Ripristina tutti i pacchetti a cui fa riferimento il formato di gestione dei pacchetti in uso. Quando si esegue in mono, il ripristino dei pacchetti con il formato PackageReference non è supportato. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | Pubblicazione, utilizzo | Tutti | Salva una chiave API per una determinata origine del pacchetto quando tale origine richiede una chiave per l'accesso. |
| [spec](cli-reference/cli-ref-spec.md) | Creazione | Tutti | Genera un `.nuspec` file, usando i token se genera il file da un progetto di Visual Studio. |

| Comandi secondari | Ruoli applicabili | Versione di NuGet | Descrizione |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Pubblicazione | 3.3 + | Aggiunge un pacchetto a un'origine pacchetto non HTTP utilizzando il layout gerarchico. Per le origini HTTP, usare *push*. |
| [delete](cli-reference/cli-ref-delete.md) | Pubblicazione | Tutti | Rimuove o rimuove dall'elenco un pacchetto da un'origine del pacchetto. |
| [init](cli-reference/cli-ref-init.md) | Creazione | 3.3 + | Aggiunge pacchetti da una cartella a un'origine del pacchetto usando il layout gerarchico. |
| [install](cli-reference/cli-ref-install.md) | Consumo | Tutti | Installa un pacchetto nel progetto corrente, ma non modifica i progetti o i file di riferimento. |
| [list](cli-reference/cli-ref-list.md) | Consumo, probabilmente pubblicazione | Tutti | Visualizza i pacchetti da un'origine specificata. |
| [mirror](cli-reference/cli-ref-mirror.md) | Pubblicazione | Deprecato in 3.2 + | Rispecchia un pacchetto e le relative dipendenze da un'origine a un repository di destinazione. |
| [search](cli-reference/cli-ref-search.md) | Consumo | 5.8 + | Esegue la ricerca di una determinata origine utilizzando la stringa di query specificata. |
| [sources](cli-reference/cli-ref-sources.md) | Consumo, pubblicazione | Tutti | Gestisce le origini dei pacchetti nei file di configurazione. |
| [update](cli-reference/cli-ref-update.md) | Consumo | Tutti | Aggiorna i pacchetti di un progetto alle versioni più recenti disponibili. Non supportato durante l'esecuzione in mono. |

Comandi diversi usano diverse variabili di [ambiente](cli-reference/cli-ref-environment-variables.md).

Comandi dell'interfaccia della riga di comando NuGet per ruoli applicabili:

| Ruolo | Comandi |
| --- | --- |
| Consumo | `config`, `help`, `install`, `list`, `locals`, `restore`, `search`, `setapikey`, `sources`, `update` |
| Creazione | `config`, `help`, `init`, `pack`, `spec` |
| Pubblicazione | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Gli sviluppatori interessati solo all'utilizzo di pacchetti, ad esempio, devono comprendere solo quel subset di comandi NuGet.

> [!Note]
> I nomi delle opzioni di comando non fanno distinzione tra maiuscole e minuscole. Le opzioni deprecate non sono incluse in questo riferimento, ad esempio `NoPrompt` (sostituito da `NonInteractive` ) e `Verbose` (sostituite da `Verbosity` ).
