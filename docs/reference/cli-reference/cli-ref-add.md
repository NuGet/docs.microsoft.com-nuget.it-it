---
title: Comando di aggiunta CLI di NuGet
description: Riferimento per il comando nuget.exe Aggiungi
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622902"
---
# <a name="add-command-nuget-cli"></a>comando Add (interfaccia della riga di comando di NuGet)

**Si applica a**: versioni supportate per la pubblicazione di pacchetti &bullet; **Supported versions**: 3.3 +

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

## <a name="usage"></a>Uso

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
