---
title: Supporto del percorso lungo dell'interfaccia della riga di comando NuGet
description: Riferimento per il supporto di nuget.exe Long Path
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238192"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="2350a-103">Supporto per percorsi lunghi (interfaccia della riga di comando NuGet)</span><span class="sxs-lookup"><span data-stu-id="2350a-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="2350a-104">**Si applica a:** tutte le &bullet; **versioni supportate:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="2350a-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="2350a-105">NuGet.exe 4,8 e versioni successive supportano percorsi lunghi per file e directory per scenari quali Pack, Restore, install e la maggior parte degli altri scenari che richiedono percorsi di file.</span><span class="sxs-lookup"><span data-stu-id="2350a-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="2350a-106">Sistema operativo richiesto</span><span class="sxs-lookup"><span data-stu-id="2350a-106">Required Operating System</span></span>

-   <span data-ttu-id="2350a-107">Windows 10 (versione 1607 o successiva)</span><span class="sxs-lookup"><span data-stu-id="2350a-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="2350a-108">Windows 10 (versione luglio 2015 o 1511) se si esegue l'aggiornamento .NET Framework a versioni 4.6.2 o successive.</span><span class="sxs-lookup"><span data-stu-id="2350a-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="2350a-109">Windows Server 2016 (tutte le versioni)</span><span class="sxs-lookup"><span data-stu-id="2350a-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="2350a-110">Abilitare "percorsi lunghi Win32" Criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="2350a-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="2350a-111">È necessario abilitare il supporto per percorsi lunghi su tali sistemi impostando criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="2350a-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="2350a-112">Passaggi:</span><span class="sxs-lookup"><span data-stu-id="2350a-112">Steps:</span></span>
1. <span data-ttu-id="2350a-113">Avviare **criteri di gruppo editor** : digitare "modifica criteri di gruppo" nella barra di ricerca iniziale o eseguire "gpedit. msc" dal comando Esegui (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="2350a-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="2350a-114">Nella **Editor criteri di gruppo locali** abilitare "criteri computer locale/Configurazione computer/modelli amministrativi/tutte le impostazioni/Abilita percorsi lunghi Win32".</span><span class="sxs-lookup"><span data-stu-id="2350a-114">In the **Local Group Policy Editor** , enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Criterio percorso lungo](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="2350a-116">Abilitazione di altri strumenti NuGet per supportare percorsi lunghi</span><span class="sxs-lookup"><span data-stu-id="2350a-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="2350a-117">L'interfaccia della riga di comando DotNet supporta percorsi lunghi indipendentemente dal sistema operativo o dalla versione.</span><span class="sxs-lookup"><span data-stu-id="2350a-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="2350a-118">Visual Studio o non `msbuild -t:restore` supporta ancora percorsi lunghi.</span><span class="sxs-lookup"><span data-stu-id="2350a-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="2350a-119">Il software che usa le librerie NuGet per eseguire Restore e altri comandi supporterà percorsi lunghi sugli stessi sistemi su cui NuGet.exe funziona, se hanno anche impostato `longPathAware` nel manifesto di Windows e configurati in `UseLegacyPathHandling` `false` tramite App.Config [visualizzare altre informazioni](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span><span class="sxs-lookup"><span data-stu-id="2350a-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span></span>