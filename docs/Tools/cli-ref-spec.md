---
title: Comando specifica CLI NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: Riferimento per il comando specifica di nuget.exe
keywords: riferimento specifica NuGet, specifiche di comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>Specifica di comando (CLI NuGet)

**Si applica a:** creazione di pacchetti &bullet; **le versioni supportate:** tutti

Genera un `.nuspec` file per un nuovo pacchetto. Se l'esecuzione nella stessa cartella un file di progetto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un token `.nuspec` file. Per ulteriori informazioni, vedere [creazione di un pacchetto](../create-packages/creating-a-package.md).

## <a name="usage"></a>Utilizzo

```
nuget spec [<packageID>] [options]
```

dove `<packageID>` è un identificatore di pacchetto facoltativo per salvare il `.nuspec` file.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| AssemblyPath | Specifica il percorso dell'assembly da usare per i metadati. |
| Force | Sovrascrive qualsiasi esistente `.nuspec` file. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
