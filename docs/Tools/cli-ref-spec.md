---
title: Comando specifica CLI NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando specifica di nuget.exe
keywords: riferimento specifica NuGet, specifiche di comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="spec-command-nuget-cli"></a>Specifica di comando (CLI NuGet)

**Si applica a:** creazione di pacchetti &bullet; **le versioni supportate:** tutti

Genera un `.nuspec` file per un nuovo pacchetto. Se l'esecuzione nella stessa cartella un file di progetto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un token `.nuspec` file. Per ulteriori informazioni, vedere [creazione di un pacchetto](../create-packages/creating-a-package.md).

## <a name="usage"></a>Utilizzo

```cli
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
| NonInteractive | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
