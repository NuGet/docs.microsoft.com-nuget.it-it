---
title: Comando di aggiunta CLI di NuGet
description: Riferimento per il comando nuget.exe Aggiungi
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776091"
---
# <a name="add-command-nuget-cli"></a>comando Add (interfaccia della riga di comando di NuGet)

**Si applica a**: versioni supportate per la pubblicazione di pacchetti &bullet; : 3.3 +

Aggiunge un pacchetto specificato a un'origine pacchetto non HTTP (una cartella o un percorso UNC) in un layout gerarchico, in cui vengono create cartelle per l'ID del pacchetto e il numero di versione. Ad esempio:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

Quando si esegue il ripristino o l'aggiornamento con l'origine del pacchetto, il layout gerarchico garantisce prestazioni significativamente migliori.

Per espandere tutti i file del pacchetto nell'origine del pacchetto di destinazione, utilizzare l' `-Expand` opzione. Ciò comporta in genere la visualizzazione di sottocartelle aggiuntive nella destinazione, ad esempio `tools` e `lib` .

## <a name="usage"></a>Utilizzo

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

dove `<packagePath>` è il percorso del pacchetto da aggiungere e `<sourcePath>` specifica l'origine del pacchetto basata su cartelle a cui verrà aggiunto il pacchetto. Le origini HTTP non sono supportate.

## <a name="options"></a>Opzioni

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-Expand`**

  Aggiunge tutti i file del pacchetto all'origine del pacchetto.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.
Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-src|-Source`**

   Specifica l'origine del pacchetto, ovvero una cartella o una condivisione UNC, a cui verranno aggiunti i nupkg. Le origini http non sono supportate.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
