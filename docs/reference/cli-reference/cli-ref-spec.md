---
title: Comando della specifica CLI di NuGet
description: Riferimento per il comando nuget.exe spec
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779147"
---
# <a name="spec-command-nuget-cli"></a>comando spec (interfaccia della riga di comando di NuGet)

**Si applica a:** versioni supportate per la creazione di pacchetti &bullet; **:** tutti

Genera un `.nuspec` file per un nuovo pacchetto. Se viene eseguito nella stessa cartella del file di progetto ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` Crea un file in `.nuspec` formato token. Per ulteriori informazioni, vedere [creazione di un pacchetto](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Utilizzo

```cli
nuget spec [<packageID>] [options]
```

dove `<packageID>` è un identificatore facoltativo del pacchetto da salvare nel `.nuspec` file.

## <a name="options"></a>Opzioni

- **`-AssemblyPath`**

  Specifica il percorso dell'assembly da utilizzare per i metadati.

- **`-Force`**

  Sovrascrive qualsiasi `.nuspec` file esistente.


- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
