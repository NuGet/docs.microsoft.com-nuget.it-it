---
title: Comando origini CLI NuGet
description: Riferimento per il comando nuget.exe sources
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780002"
---
# <a name="sources-command-nuget-cli"></a>comando Sources (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo del pacchetto, pubblicazione delle &bullet; **versioni supportate:** tutti

Gestisce l'elenco delle origini presenti nel file di configurazione dell'ambito utente o in un file di configurazione specificato. Il file di configurazione dell'ambito utente si trova in `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Utilizzo

```cli
nuget sources <operation> -Name <name> -Source <source>
```

dove `<operation>` è un *elenco, Aggiungi, Rimuovi, Abilita, Disabilita* o *Aggiorna* `<name>` è il nome dell'origine e `<source>` è l'URL dell'origine. È possibile operare su una sola origine alla volta.

## <a name="options"></a>Opzioni

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-Format`**

  Si applica all' `list` azione e può essere `Detailed` (impostazione predefinita) o `Short` .

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-Name`**

  Nome dell'origine.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-Password`**

  Specifica la password per l'autenticazione con l'origine.

- **`-src|-Source`**

  Percorso dell'origine dei pacchetti.

- **`-StorePasswordInClearText`**

  Indica per archiviare la password in testo non crittografato anziché il comportamento predefinito di archiviazione di un modulo crittografato.

- **`-UserName`**

  Specifica il nome utente per l'autenticazione con l'origine.

- **`-ValidAuthenticationTypes`**

  Elenco delimitato da virgole di tipi di autenticazione validi per questa origine. Per impostazione predefinita, tutti i tipi di autenticazione sono validi. Esempio: `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

> [!Note]
> Assicurarsi di aggiungere la password delle origini nello stesso contesto utente in cui il nuget.exe viene usato in un secondo momento per accedere all'origine del pacchetto. La password verrà archiviata crittografata nel file di configurazione e potrà essere decrittografata solo nello stesso contesto utente in cui è stata crittografata. Quindi, ad esempio, quando si usa un server di compilazione per ripristinare i pacchetti NuGet, la password deve essere crittografata con lo stesso utente di Windows in cui verrà eseguita l'attività del server di compilazione.

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
