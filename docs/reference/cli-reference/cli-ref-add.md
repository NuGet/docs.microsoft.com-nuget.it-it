---
title: Comando di aggiunta CLI di NuGet
description: Riferimento per il comando Add di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327858"
---
# <a name="add-command-nuget-cli"></a>Comando add (interfaccia della riga di comando di NuGet)

**Si applica a**: &bullet; **versioni supportate**per la pubblicazione di pacchetti: 3.3+

Aggiunge un pacchetto specificato a un'origine pacchetto non HTTP (una cartella o un percorso UNC) in un layout gerarchico, in cui vengono create cartelle per l'ID del pacchetto e il numero di versione. Ad esempio:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Quando si esegue il ripristino o l'aggiornamento con l'origine del pacchetto, il layout gerarchico garantisce prestazioni significativamente migliori.

Per espandere tutti i file del pacchetto nell'origine del pacchetto di destinazione, utilizzare l' `-Expand` opzione. Ciò comporta in genere la visualizzazione di sottocartelle aggiuntive nella destinazione, ad esempio `tools` e. `lib`

## <a name="usage"></a>Utilizzo

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

dove `<packagePath>` è il percorso del pacchetto da aggiungere e `<sourcePath>` specifica l'origine del pacchetto basata su cartelle a cui verrà aggiunto il pacchetto. Le origini HTTP non sono supportate.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| Expand | Aggiunge tutti i file del pacchetto all'origine del pacchetto. |
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Help | Visualizza le informazioni della Guida per il comando. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
