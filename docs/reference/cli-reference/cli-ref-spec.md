---
title: Comando della specifica CLI di NuGet
description: Informazioni di riferimento sul comando NuGet. exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327568"
---
# <a name="spec-command-nuget-cli"></a>comando spec (interfaccia della riga di comando di NuGet)

**Si applica a:** &bullet; **versioni supportate** per la creazione di pacchetti: tutti

Genera un `.nuspec` file per un nuovo pacchetto. Se viene eseguito nella stessa cartella del file di progetto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un `.nuspec` file in formato token. Per ulteriori informazioni, vedere [creazione di un pacchetto](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Utilizzo

```cli
nuget spec [<packageID>] [options]
```

dove `<packageID>` è un identificatore facoltativo del `.nuspec` pacchetto da salvare nel file.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| AssemblyPath | Specifica il percorso dell'assembly da utilizzare per i metadati. |
| Force | Sovrascrive qualsiasi file esistente `.nuspec` . |
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Help | Visualizza le informazioni della Guida per il comando. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
