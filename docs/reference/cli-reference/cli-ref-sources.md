---
title: Comando origini CLI NuGet
description: Informazioni di riferimento sul comando NuGet. exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327598"
---
# <a name="sources-command-nuget-cli"></a>Comando sources (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo del pacchetto &bullet; , pubblicazione delle **versioni supportate:** tutti

Gestisce l'elenco delle origini presenti nel file di configurazione dell'ambito utente o in un file di configurazione specificato. Il file di configurazione dell'ambito utente si `%appdata%\NuGet\NuGet.Config` trova in (Windows `~/.nuget/NuGet/NuGet.Config` ) e (Mac/Linux).

Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Utilizzo

```cli
nuget sources <operation> -Name <name> -Source <source>
```

dove `<operation>` è un *elenco, Aggiungi, Rimuovi, Abilita, Disabilita* o *Aggiorna* `<name>` è il nome dell'origine e `<source>` è l'URL dell'origine. È possibile operare su una sola origine alla volta.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Formato | Si applica all' `list` azione e può essere `Detailed` (impostazione predefinita) o `Short`. |
| ? | Visualizza le informazioni della Guida per il comando. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| Password | Specifica la password per l'autenticazione con l'origine. |
| StorePasswordInClearText | Indica per archiviare la password in testo non crittografato anziché il comportamento predefinito di archiviazione di un modulo crittografato. |
| UserName | Specifica il nome utente per l'autenticazione con l'origine. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

> [!Note]
> Assicurarsi di aggiungere la password delle origini nello stesso contesto utente in cui NuGet. exe verrà usato in un secondo momento per accedere all'origine del pacchetto. La password verrà archiviata crittografata nel file di configurazione e potrà essere decrittografata solo nello stesso contesto utente in cui è stata crittografata. Quindi, ad esempio, quando si usa un server di compilazione per ripristinare i pacchetti NuGet, la password deve essere crittografata con lo stesso utente di Windows in cui verrà eseguita l'attività del server di compilazione.

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
