---
title: Comando specifica di NuGet CLI
description: Riferimento per il comando specifica di nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817086"
---
# <a name="spec-command-nuget-cli"></a>Specifica di comando (CLI NuGet)

**Si applica a:** creazione di pacchetti &bullet; **versioni supportate:** tutti

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
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
