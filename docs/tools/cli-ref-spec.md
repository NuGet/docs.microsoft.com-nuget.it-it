---
title: Comando specifica di CLI di NuGet
description: Informazioni di riferimento per il comando specifica nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794151"
---
# <a name="spec-command-nuget-cli"></a>comando Spec (NuGet CLI)

**Si applica a:** creazione del pacchetto &bullet; **le versioni supportate:** tutti

Genera un `.nuspec` file per un nuovo pacchetto. Se eseguito nella stessa cartella un file di progetto (`.csproj`, `.vbproj`, `.fsproj`), `spec` consente di creare un token `.nuspec` file. Per altre informazioni, vedere [creazione di un pacchetto](../create-packages/creating-a-package.md).

## <a name="usage"></a>Utilizzo

```cli
nuget spec [<packageID>] [options]
```

in cui `<packageID>` è un identificatore di pacchetto facoltativo per salvare il `.nuspec` file.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| AssemblyPath | Specifica il percorso dell'assembly da utilizzare per i metadati. |
| Force | Sovrascrive tutte le classi esistenti `.nuspec` file. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattive | Elimina richieste di input o conferme dell'utente. |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
