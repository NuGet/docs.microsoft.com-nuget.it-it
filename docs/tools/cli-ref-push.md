---
title: Comando push NuGet CLI
description: Informazioni di riferimento per il comando push nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bce04864224a66019a52cdfff8355f68dc424204
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974996"
---
# <a name="push-command-nuget-cli"></a>comando push (NuGet CLI)

**Si applica a:** pacchetto di pubblicazione &bullet; **le versioni supportate:** tutte: versione 4.1.0 + necessari per nuget.org

> [!Important]
> Eseguire il push dei pacchetti in nuget.org è necessario usare nuget.exe verze 4.1.0 +, che implementa la necessaria [protocolli NuGet](../api/nuget-protocols.md).

Effettua il push di un pacchetto a un'origine di pacchetto e lo pubblica.

Configurazione predefinita di NuGet si ottiene caricando `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), quindi caricando qualsiasi `Nuget.Config` oppure `.nuget\Nuget.Config` file a partire dalla radice dell'unità e di fine nella directory corrente (vedere [configurazione Comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Utilizzo

```cli
nuget push <packagePath> [options]
```

in cui `<packagePath>` identifica il pacchetto per effettuare il push nel server.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ApiKey | La chiave API per il repository di destinazione. Se non è presente, viene utilizzato quello specificato nel file di configurazione. |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| DisableBuffering | Disabilita la memorizzazione nel buffer quando si effettua il push a un server HTTP (s) per ridurre gli utilizzi della memoria. Attenzione: quando questa opzione viene usata, l'autenticazione integrata di Windows potrebbe non funzionare. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| Help | Visualizza la Guida informazioni per il comando. |
| NonInteractive | Elimina richieste di input o conferme dell'utente. |
| NoSymbols | *(3.5 +)*  Se esiste un pacchetto di simboli, non verrà inserito in un server di simboli. |
| Origine | Specifica l'URL del server. NuGet identifica un'origine di cartella locale o UNC e copia semplicemente il file invece di eseguirne il push tramite HTTP.  Inoltre, a partire da NuGet 3.4.2, questo è un parametro obbligatorio, a meno che il `NuGet.Config` file specifica un *DefaultPushSource* valore (vedere [del comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md)). |
| SkipDuplicate | Se esiste già un pacchetto e versione, ignorarlo e continuare con il pacchetto successivo nel push, se presente. |
| SymbolSource | *(3.5 +)*  Specifica l'URL del server di simboli; nuget.smbsrc.net viene usato quando il push in nuget.org |
| SymbolApiKey | *(3.5 +)*  Specifica la chiave API per l'URL specificato in `-SymbolSource`. |
| Timeout | Specifica il timeout, espresso in secondi, per effettuare il push a un server. Il valore predefinito è 300 secondi (5 minuti). |
| Verbosity | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

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
