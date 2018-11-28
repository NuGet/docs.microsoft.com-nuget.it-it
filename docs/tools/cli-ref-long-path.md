---
title: Supporto del percorso lungo della riga di comando di NuGet
description: Informazioni di riferimento per nuget.exe supporto del percorso lungo
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453494"
---
# <a name="long-path-support-nuget-cli"></a>Supporto del percorso lungo (NuGet CLI)

**Si applica a:** tutte &bullet; **le versioni supportate:** 4.8

NuGet.exe 4.8 e versioni successive supportano i percorsi lunghi per i file e directory per gli scenari come i Service Pack, ripristino, installazione e la maggior parte degli altri scenari che richiedono i percorsi dei file.

## <a name="required-operating-system"></a>Richiesta del sistema operativo

-   Windows 10 (versione 1607 o successiva)
-   Windows 10 (versione di luglio 2015 o versione 1511) se si esegue l'aggiornamento di .NET Framework versioni 4.6.2 o versioni successive.
-   Windows Server 2016 (tutte le versioni)

## <a name="enable-win32-long-paths-group-policy"></a>Abilitare i criteri di gruppo "Percorsi lunghi Win32"

È necessario abilitare il supporto di percorsi lunghi in tali sistemi impostando un criterio di gruppo.

Procedura:
1. Avvio veloce **Editor criteri di gruppo** : digitare "Modifica dei criteri di gruppo" nella barra di ricerca iniziale o eseguire "gpedit. msc" nel comando Esegui (Windows-R).
2. Nel **Editor criteri di gruppo locali**, abilitare "locali Computer/criteri di Computer Configuration/Administrative modelli/tutti i percorsi lunghi Win32 o abilitare le impostazioni".

![Criteri del percorso lungo](media/LongPathPolicy.png)


> [!Note]
> Abilitazione di altri strumenti di NuGet supportare i percorsi lunghi
>
> -   Dotnet CLI supporta i percorsi lunghi indipendentemente dal sistema operativo o di versione.
> -   Visual Studio o msbuild - t: ripristino non supporta ancora i percorsi lunghi.
> -   Software che utilizza librerie di NuGet per eseguire il ripristino e altri comandi, supporteranno i percorsi lunghi nei sistemi stesso che NuGet.exe funziona su, se si imposta anche longPathAware nella finestra del manifesto e configurare UseLegacyPathHandling su false tramite app. config [ Vedere altre informazioni](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

