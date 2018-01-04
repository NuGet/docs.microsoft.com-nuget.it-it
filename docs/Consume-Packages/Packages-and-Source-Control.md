---
title: Pacchetti NuGet e controllo del codice sorgente | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c874e6f-99eb-46dd-997f-f67d98d0237e
description: "Considerazioni sulle modalità di gestione dei pacchetti NuGet all'interno di sistemi di controllo della versione e di controllo del codice sorgente e su come omettere i pacchetti con Git e il controllo della versione di Team Foundation."
keywords: Controllo del codice sorgente NuGet, controllo della versione NuGet, NuGet e Git, NuGet e TFS, NuGet e il controllo della versione di Team Foundation, omissione di pacchetti, repository di controllo del codice sorgente, repository di controllo della versione
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c73dea74f2363f49fb476a5812c29de63fec89a3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Omissione di pacchetti NuGet nei sistemi di controllo del codice sorgente

Gli sviluppatori omettono in genere i pacchetti NuGet nei repository di controllo del codice sorgente e si affidano invece al [ripristino dei pacchetti](../consume-packages/package-restore.md) per reinstallare le dipendenze di un progetto prima di una compilazione.

Di seguito sono indicati i motivi validi per affidarsi al ripristino dei pacchetti:

1. I sistemi di controllo della versione distribuiti, come Git, includono copie complete di ogni versione di ogni file all'interno del repository. I file binari che vengono aggiornati di frequente causano aumenti notevoli delle dimensioni del repository e prolungano il tempo necessario per la sua clonazione.
1. Quando i pacchetti vengono inclusi nel repository, gli sviluppatori sono tenuti ad aggiungere i riferimenti direttamente al contenuto del pacchetto su disco anziché fare riferimento ai pacchetti tramite NuGet, e ciò può portare a nomi di percorso hardcoded nel progetto.
1. Diventa più difficile ripulire la soluzione da eventuali cartelle di pacchetti inutilizzate, perché è necessario accertarsi di non eliminare eventuali cartelle di pacchetti ancora in uso.
1. L'omissione dei pacchetti consente di mantenere limiti di proprietà ben definiti tra il proprio codice e i pacchetti di altri da cui si dipende. Molti pacchetti NuGet vengono già gestiti in repository di controllo del codice sorgente specifici.

Anche se il ripristino dei pacchetti è il comportamento predefinito con NuGet, sono necessari alcuni interventi manuali per omettere i pacchetti dal controllo del codice sorgente, ovvero la cartella `packages`, come descritto nelle sezioni seguenti.

## <a name="omitting-packages-with-git"></a>Omissione di pacchetti con Git

Usare il [file con estensione gitignore](https://git-scm.com/docs/gitignore) per evitare di includere la cartella `packages` nel controllo del codice sorgente. Per riferimento, vedere il [file `.gitignore` di esempio per i progetti di Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Le parti importanti del file `.gitignore` sono:

```
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>Omissione dei pacchetti con il controllo della versione di Team Foundation

> [!Note]
> Se possibile, seguire queste istruzioni *prima* di aggiungere il progetto al controllo del codice sorgente. In caso contrario, eliminare manualmente la cartella `packages` dal repository e archiviare la modifica prima di continuare.

Per disabilitare l'integrazione del controllo del codice sorgente con il controllo della versione di Team Foundation per una selezione di file:

1. Creare una cartella denominata `.nuget` nella cartella della soluzione (dove si trova il file `.sln`).
    - Suggerimento: in Windows, per creare la cartella in Esplora risorse usare il nome `.nuget.` *con* il punto finale.

1. In questa cartella creare un file denominato `NuGet.Config` e aprirlo per la modifica.

1. Aggiungere come minimo il testo seguente, in cui l'impostazione [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) indica a Visual Studio di ignorare tutti gli elementi nella cartella `packages`:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Se si usa TFS 2010 o versioni precedenti, mascherare la cartella `packages` nei mapping dell'area di lavoro.

1. In TFS 2012 o versione successiva oppure con Visual Studio Team Services, creare un file `.tfignore` come descritto in [Add files to the server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore) (Aggiungere file al server). In tale file, includere il contenuto seguente per ignorare in modo esplicito le modifiche per la cartella `\packages` a livello del repository e alcuni altri file intermedi. È possibile creare il file in Esplora risorse usando il nome `.tfignore.` con il punto finale, ma potrebbe essere necessario disabilitare prima di tutto l'opzione per nascondere le estensioni di file conosciute:

   ```
   # Ignore NuGet Packages
   *.nupkg   

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Aggiungere `NuGet.Config` e `.tfignore` al controllo del codice sorgente e archiviare le modifiche.
