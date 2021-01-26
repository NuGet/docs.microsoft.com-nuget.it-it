---
title: Comando push dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando nuget.exe push
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 54a09361173ae10040433b05fcfae7304e39452e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779184"
---
# <a name="push-command-nuget-cli"></a>comando Push (interfaccia della riga di comando di NuGet)

**Si applica a:** &bullet; **versioni supportate** per la pubblicazione di pacchetti: All; 4.1.0 + required for NuGet.org

> [!Important]
> Per eseguire il push dei pacchetti in nuget.org è necessario usare nuget.exe v 4.1.0 +, che implementa i [protocolli NuGet](../../api/nuget-protocols.md)necessari.

Inserisce un pacchetto in un'origine del pacchetto e lo pubblica.

La configurazione predefinita di NuGet si ottiene caricando `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), quindi caricando tutti `Nuget.Config` `.nuget\Nuget.Config` i file o a partire dalla radice dell'unità e terminando con la directory corrente (vedere [configurazioni NuGet comuni](../../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Utilizzo

```cli
nuget push <packagePath> [options]
```

dove `<packagePath>` identifica il pacchetto da inserire nel server.

## <a name="options"></a>Opzioni

- **`-ApiKey`**

  Chiave API per il repository di destinazione. Se non è presente, viene utilizzato quello specificato nel file di configurazione.

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-DisableBuffering`**

  Disabilita la memorizzazione nel buffer quando si effettua il push a un server HTTP (s) per ridurre gli utilizzi della memoria. Attenzione: quando si usa questa opzione, l'autenticazione integrata di Windows potrebbe non funzionare.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-NoServiceEndpoint`**

  Non viene accodato `api/v2/packages` all'URL di origine.

- **`-NoSymbols`**

  *(3.5 +)* Se esiste un pacchetto di simboli, non verrà eseguito il push in un server di simboli.

- **`-src|-Source`**

  Specifica l'URL del server. NuGet identifica un'origine UNC o di cartella locale ed esegue semplicemente la copia del file, anziché eseguire il push usando il protocollo HTTP.  Inoltre, a partire da NuGet 3.4.2, si tratta di un parametro obbligatorio a meno che il `NuGet.Config` file non specifichi un valore *DefaultPushSource* (vedere [configurazione del comportamento di NuGet](../../consume-packages/configuring-nuget-behavior.md)).

- **`-SkipDuplicate`**

  *(5.1 +)* Se un pacchetto e una versione esiste già, ignorarlo e continuare con il pacchetto successivo nell'eventuale push.

- **`-SymbolSource`**

  *(3.5 +)* Specifica l'URL del server di simboli. nuget.smbsrc.net viene usato quando si esegue il push in nuget.org

- **`-SymbolApiKey`**

  *(3.5 +)* Specifica la chiave API per l'URL specificato in `-SymbolSource` .

- **`-Timeout`**

  Specifica il timeout, in secondi, per il push in un server.  Il valore predefinito è 300 secondi (5 minuti).

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .


Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
