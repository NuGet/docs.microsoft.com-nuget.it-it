---
title: Risoluzione dei problemi relativi al ripristino dei pacchetti NuGet in Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Descrizione degli errori di ripristino comuni per NuGet in Visual Studio e di come risolverli.
keywords: Ripristinare pacchetti NuGet, ripristino di pacchetti, risoluzione dei problemi, risolvere problemi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0993e2585452e3c64da28d14bb1bbe1bea27768
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Risoluzione degli errori relativi al ripristino dei pacchetti in Visual Studio

> [!Note]
> Questa pagina è dedicata agli errori comuni durante il ripristino dei pacchetti in Visual Studio e alle procedure per risolverli. Per istruzioni su come ripristinare i pacchetti, vedere [Ripristino di pacchetti](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Per impostazione predefinita, quando si compila un progetto in Visual Studio vengono ripristinati automaticamente i pacchetti NuGet a cui si fa riferimento nel progetto. Tuttavia, le compilazioni avranno esito negativo se il ripristino dei pacchetti è disabilitato nelle impostazioni **Strumenti > Opzioni > Gestione pacchetti NuGet > Ripristino pacchetto** e i pacchetti necessari non sono disponibili nel computer. In questi casi potrebbero essere visualizzati gli errori seguenti:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

Per abilitare il ripristino dei pacchetti, aprire **Strumenti > Opzioni > Gestione pacchetti NuGet** e selezionare le opzioni **Consenti a NuGet di scaricare i pacchetti mancanti** e **Verificare in automatico i pacchetti mancanti durante il build in Visual Studio**:

![Abilitare il ripristino dei pacchetti NuGet in Strumenti/Opzioni](../consume-packages/media/restore-01-autorestoreoptions.png)
