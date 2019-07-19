---
title: Comando di eliminazione CLI di NuGet
description: Informazioni di riferimento sul comando NuGet. exe delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327838"
---
# <a name="delete-command-nuget-cli"></a>comando Delete (interfaccia della riga di comando di NuGet)

**Si applica a:** &bullet; **versioni supportate** per la pubblicazione di pacchetti: tutti

Elimina o rimuove dall'elenco un pacchetto da un'origine del pacchetto. Per nuget.org, il comando delete Annulla [l'elenco del pacchetto](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Utilizzo

```cli
nuget delete <packageID> <packageVersion> [options]
```

dove `<packageID>` e`<packageVersion>` identificano il pacchetto esatto da eliminare o rimuovere dall'elenco. Il comportamento esatto dipende dall'origine. Per le cartelle locali, ad esempio, il pacchetto viene eliminato. per nuget.org il pacchetto viene riincluso nell'elenco.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ApiKey | Chiave API per il repository di destinazione. Se non è presente, viene utilizzato quello specificato nel file di configurazione. |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Help | Visualizza le informazioni della Guida per il comando. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| Source | Specifica l'URL del server. L'URL per nuget.org è `https://api.nuget.org/v3/index.json`. Per i feed privati, sostituire il nome host, ad esempio *% hostname%/API/V3*. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
