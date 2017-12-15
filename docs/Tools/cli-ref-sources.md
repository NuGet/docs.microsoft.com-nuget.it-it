---
title: NuGet CLI origini comando | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: Riferimento per il nuget.exe origini comando
keywords: NuGet origini di riferimento, le origini di comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a>comando origini (NuGet CLI)

**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti

Gestisce l'elenco delle origini nel `%AppData%\NuGet\NuGet.Config` o file di configurazione specificato.

## <a name="usage"></a>Utilizzo

```
nuget sources <operation> -Name <name> -Source <source>
```

dove `<operation>` è uno dei *elenco, aggiungere, rimuovere, attivare, disattivare* o *aggiornamento*, `<name>` è il nome dell'origine, e `<source>` è l'URL dell'origine.


## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | *(2.5 +)*  Questo file di configurazione da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| Formato | Si applica al `list` azione e può essere `Detailed` (impostazione predefinita) o `Short`. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Password | Specifica la password per l'autenticazione con l'origine. |
| StorePasswordInClearText | Indica di archiviare la password in testo non crittografato anziché il comportamento predefinito di archiviazione di un formato crittografato. |
| UserName | Specifica il nome utente per l'autenticazione con l'origine. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*. |

> [!Note]
> Assicurarsi di aggiungere password delle origini nel contesto dell'utente stesso come il nuget.exe viene successivamente utilizzato per accedere all'origine del pacchetto. La password verrà archiviata crittografati nel file di configurazione e può essere decrittografata solo nello stesso contesto utente come è stato crittografato. Ad esempio quando si utilizza un server di compilazione per il ripristino dei pacchetti NuGet che la password deve essere crittografata con lo stesso utente di Windows in cui verrà eseguita l'attività del server di compilazione.

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
