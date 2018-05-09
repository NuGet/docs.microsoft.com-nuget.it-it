---
title: Comando delete NuGet CLI
description: Riferimento per il comando delete nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a>eliminazione di comando (CLI NuGet)

**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** tutti

Elimina o unlists un pacchetto da un'origine del pacchetto. Per nuget.org, il comando delete [unlists il pacchetto](../policies/deleting-packages.md).

## <a name="usage"></a>Utilizzo

```cli
nuget delete <packageID> <packageVersion> [options]
```

dove `<packageID>` e `<packageVersion>` identificare il pacchetto esatto per eliminare o esclusione. Il comportamento esatto dipende dall'origine. Per le cartelle locali, ad esempio, il pacchetto viene eliminato; per nuget.org il pacchetto è incluso nell'elenco.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| apiKey | La chiave API per il repository di destinazione. Se non è presente, viene utilizzato quello specificato nel file di configurazione. |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Origine | Specifica l'URL del server. L'URL per nuget.org è `https://api.nuget.org/v3/index.json`. Per i feed privati, sostituire il nome host, ad esempio, *%hostname%/api/v3*. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
