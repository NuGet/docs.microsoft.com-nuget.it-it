---
title: Supporto del percorso lungo della riga di comando di NuGet
description: Informazioni di riferimento per nuget.exe supporto del percorso lungo
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547826"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="e7b0e-103">Supporto del percorso lungo (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e7b0e-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="e7b0e-104">**Si applica a:** tutte &bullet; **le versioni supportate:** 4.8</span><span class="sxs-lookup"><span data-stu-id="e7b0e-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="e7b0e-105">NuGet.exe 4.8 e versioni successive supportano i percorsi lunghi per i file e directory per gli scenari come i Service Pack, ripristino, installazione e la maggior parte degli altri scenari che richiedono i percorsi dei file.</span><span class="sxs-lookup"><span data-stu-id="e7b0e-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="e7b0e-106">Richiesta del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e7b0e-106">Required Operating System</span></span>

-   <span data-ttu-id="e7b0e-107">Windows 10 (versione 1607 o successiva)</span><span class="sxs-lookup"><span data-stu-id="e7b0e-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="e7b0e-108">Windows 10 (versione di luglio 2015 o versione 1511) se si esegue l'aggiornamento di .NET Framework versioni 4.6.2 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="e7b0e-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="e7b0e-109">Windows Server 2016 (tutte le versioni)</span><span class="sxs-lookup"><span data-stu-id="e7b0e-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="e7b0e-110">Abilitare i criteri di gruppo "Percorsi lunghi Win32"</span><span class="sxs-lookup"><span data-stu-id="e7b0e-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="e7b0e-111">È necessario abilitare il supporto di percorsi lunghi in tali sistemi impostando un criterio di gruppo.</span><span class="sxs-lookup"><span data-stu-id="e7b0e-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="e7b0e-112">Procedura:</span><span class="sxs-lookup"><span data-stu-id="e7b0e-112">Steps:</span></span>
1. <span data-ttu-id="e7b0e-113">Avvio veloce **Editor criteri di gruppo** : digitare "Modifica dei criteri di gruppo" nella barra di ricerca iniziale o eseguire "gpedit. msc" nel comando Esegui (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="e7b0e-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="e7b0e-114">Nel **Editor criteri di gruppo locali**, abilitare "locali Computer/criteri di Computer Configuration/Administrative modelli/tutti i percorsi lunghi Win32 o abilitare le impostazioni".</span><span class="sxs-lookup"><span data-stu-id="e7b0e-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Criteri del percorso lungo](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="e7b0e-116">Abilitazione di altri strumenti di NuGet supportare i percorsi lunghi</span><span class="sxs-lookup"><span data-stu-id="e7b0e-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="e7b0e-117">Dotnet CLI supporta i percorsi lunghi indipendentemente dal sistema operativo o di versione.</span><span class="sxs-lookup"><span data-stu-id="e7b0e-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="e7b0e-118">Visual Studio o msbuild /t: Restore non supporta ancora i percorsi lunghi.</span><span class="sxs-lookup"><span data-stu-id="e7b0e-118">Visual Studio or msbuild /t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="e7b0e-119">Software che utilizza librerie di NuGet per eseguire il ripristino e altri comandi, supporteranno i percorsi lunghi nei sistemi stesso che NuGet.exe funziona su, se si imposta anche longPathAware nella finestra del manifesto e configurare UseLegacyPathHandling su false tramite app. config [ Vedere altre informazioni](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="e7b0e-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

