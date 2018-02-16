---
title: Comando push NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di nuget.exe push
keywords: riferimento push NuGet, il comando push
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: df8ef42f650a20b92a281fff3e597ac8d484544e
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="push-command-nuget-cli"></a>comando push (NuGet CLI)

**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** tutti; 4.1.0+ necessari per nuget.org

> [!Important]
> Per inviare pacchetti a nuget.org è necessario utilizzare nuget.exe v4.1.0 +, che implementa la [NuGet protocolli](../api/nuget-protocols.md).

Inserisce un pacchetto a un'origine del pacchetto e la pubblicazione.

Configurazione predefinita di NuGet consente di ottenere il caricamento `%AppData%\NuGet\NuGet.Config`, quindi caricare qualsiasi `Nuget.Config` o `.nuget\Nuget.Config` file a partire dalla radice dell'unità e di fine nella directory corrente (vedere [configurazione NuGet comportamento](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Utilizzo

```cli
nuget push <packagePath> [options]
```

dove `<packagePath>` identifica il pacchetto da inviare al server.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ApiKey | La chiave API per il repository di destinazione. Se non è presente, quella specificata nella *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| DisableBuffering | Disabilita la memorizzazione nel buffer quando push a un server HTTP (s) per ridurre l'utilizzo di memoria. Attenzione: quando si utilizza questa opzione, l'autenticazione integrata di Windows potrebbe non funzionare. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| NonInteractive | Elimina richieste per l'input dell'utente o le conferme. |
| NoSymbols | *(3.5 +)*  Se esiste un pacchetto di simboli, non sarà inserito in un server di simboli. |
| Origine | Specifica l'URL del server. NuGet identifica un origine cartella locale o UNC e copiato il file anziché il push tramite HTTP.  Inoltre, a partire da NuGet sezione 3.4.2, questo è un parametro obbligatorio, a meno che il `NuGet.Config` file specifica un *DefaultPushSource* valore (vedere [il comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 +)*  Specifica l'URL del server di simboli; nuget.smbsrc.net viene usato quando l'inserimento di nuget.org |
| SymbolApiKey | *(3.5 +)*  Specifica la chiave API per l'URL specificato nel `-SymbolSource`. |
| Timeout | Specifica il timeout in secondi, per l'inserimento di un server. Il valore predefinito è 300 secondi (5 minuti). |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

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

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
