---
title: Comando delete NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando delete nuget.exe
keywords: NuGet Elimina riferimento, eliminare il comando di pacchetto
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3412d38edbdb011d050b9b61c7c144568edd4cca
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
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
| ApiKey | La chiave API per il repository di destinazione. Se non è presente, quella specificata nella *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| NonInteractive | Elimina richieste per l'input dell'utente o le conferme. |
| Origine | Specifica l'URL del server. L'URL per nuget.org è `https://api.nuget.org/v3/index.json`. Per i feed privati, sostituire il nome host, ad esempio, *%hostname%/api/v3*. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
