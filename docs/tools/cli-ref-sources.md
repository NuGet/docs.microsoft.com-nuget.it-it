---
title: Comando le origini NuGet CLI
description: Informazioni di riferimento per il nuget.exe origini di comandi
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610627"
---
# <a name="sources-command-nuget-cli"></a>Comando sources (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo di un pacchetto, la pubblicazione &bullet; **le versioni supportate:** tutti

Gestisce l'elenco delle origini che si trova nel file di configurazione di ambito utente o un file di configurazione specificato. Il file di configurazione di ambito utente si trova in `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Utilizzo

```cli
nuget sources <operation> -Name <name> -Source <source>
```

in cui `<operation>` è uno dei *elencare, aggiungere, rimuovere, abilitare, disabilitare* oppure *Update*, `<name>` è il nome dell'origine, e `<source>` è l'URL dell'origine. È possibile utilizzare una sola origine alla volta.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| Formato | Viene applicata il `list` azione e può essere `Detailed` (predefinito) o `Short`. |
| ? | Visualizza la Guida informazioni per il comando. |
| NonInteractive | Elimina richieste di input o conferme dell'utente. |
| Password | Specifica la password per l'autenticazione con l'origine. |
| StorePasswordInClearText | Indica di archiviare la password in testo non crittografato anziché il comportamento predefinito di un modulo crittografato di archiviazione. |
| UserName | Specifica il nome utente per l'autenticazione con l'origine. |
| Verbosity | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

> [!Note]
> Assicurarsi di aggiungere password delle origini nello stesso contesto utente come il nuget.exe viene successivamente utilizzato per accedere all'origine del pacchetto. La password verrà archiviata crittografati nel file di configurazione e può essere decrittografata solo nello stesso contesto utente perché è stato crittografato. Quindi, ad esempio quando si usa un server di compilazione per ripristinare i pacchetti NuGet che la password deve essere crittografata con lo stesso utente di Windows con cui verrà eseguita l'attività del server di compilazione.

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
