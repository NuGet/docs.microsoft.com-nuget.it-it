---
title: Comando di eliminazione CLI di NuGet
description: Riferimento per il comando nuget.exe Delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622863"
---
# <a name="delete-command-nuget-cli"></a>comando Delete (interfaccia della riga di comando di NuGet)

**Si applica a:** versioni supportate per la pubblicazione di pacchetti &bullet; **:** tutti

Elimina o rimuove dall'elenco un pacchetto da un'origine del pacchetto. Per nuget.org, il comando delete Annulla [l'elenco del pacchetto](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Uso

```cli
nuget delete <packageID> <packageVersion> [options]
```

dove `<packageID>` e `<packageVersion>` identificano il pacchetto esatto da eliminare o rimuovere dall'elenco. Il comportamento esatto dipende dall'origine. Per le cartelle locali, ad esempio, il pacchetto viene eliminato. per nuget.org il pacchetto viene riincluso nell'elenco.

## <a name="options"></a>Opzioni

- **`-ApiKey`**

  Chiave API per il repository di destinazione. Se non è presente, viene utilizzato quello specificato nel file di configurazione.

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

 - **`-np|-NoPrompt`**

   Non chiedere conferma durante l'eliminazione.

 - **`-NoServiceEndpoint`** Non aggiunge "API/v2/Packages" all'URL di origine.

- **`-src|-Source`**

  Specifica l'URL del server. L'URL per nuget.org è `https://api.nuget.org/v3/index.json` . Per i feed privati, sostituire il nome host, ad esempio *% hostname%/API/V3*.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
