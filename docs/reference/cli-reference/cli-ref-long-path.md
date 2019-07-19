---
title: Supporto del percorso lungo dell'interfaccia della riga di comando NuGet
description: Informazioni di riferimento sul supporto per percorsi lunghi di NuGet. exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327678"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="2a154-103">Supporto per percorsi lunghi (interfaccia della riga di comando NuGet)</span><span class="sxs-lookup"><span data-stu-id="2a154-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="2a154-104">**Si applica a:** tutte le &bullet; **versioni supportate:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="2a154-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="2a154-105">NuGet. exe 4,8 e versioni successive supportano percorsi lunghi per file e directory per scenari come Pack, Restore, install e la maggior parte degli altri scenari che richiedono percorsi di file.</span><span class="sxs-lookup"><span data-stu-id="2a154-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="2a154-106">Sistema operativo richiesto</span><span class="sxs-lookup"><span data-stu-id="2a154-106">Required Operating System</span></span>

-   <span data-ttu-id="2a154-107">Windows 10 (versione 1607 o successiva)</span><span class="sxs-lookup"><span data-stu-id="2a154-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="2a154-108">Windows 10 (versione luglio 2015 o 1511) se si esegue l'aggiornamento .NET Framework a versioni 4.6.2 o successive.</span><span class="sxs-lookup"><span data-stu-id="2a154-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="2a154-109">Windows Server 2016 (tutte le versioni)</span><span class="sxs-lookup"><span data-stu-id="2a154-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="2a154-110">Abilitare "percorsi lunghi Win32" Criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="2a154-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="2a154-111">È necessario abilitare il supporto per percorsi lunghi su tali sistemi impostando criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="2a154-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="2a154-112">Passaggi</span><span class="sxs-lookup"><span data-stu-id="2a154-112">Steps:</span></span>
1. <span data-ttu-id="2a154-113">Avviare **criteri di gruppo editor** : digitare "modifica criteri di gruppo" nella barra di ricerca iniziale o eseguire "gpedit. msc" dal comando Esegui (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="2a154-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="2a154-114">Nella **Editor criteri di gruppo locali**abilitare "criteri computer locale/Configurazione computer/modelli amministrativi/tutte le impostazioni/Abilita percorsi lunghi Win32".</span><span class="sxs-lookup"><span data-stu-id="2a154-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Criterio percorso lungo](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="2a154-116">Abilitazione di altri strumenti NuGet per supportare percorsi lunghi</span><span class="sxs-lookup"><span data-stu-id="2a154-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="2a154-117">L'interfaccia della riga di comando DotNet supporta percorsi lunghi indipendentemente dal sistema operativo o dalla versione.</span><span class="sxs-lookup"><span data-stu-id="2a154-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="2a154-118">Visual Studio o MSBuild-t:Restore non supporta ancora percorsi lunghi.</span><span class="sxs-lookup"><span data-stu-id="2a154-118">Visual Studio or msbuild -t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="2a154-119">Il software che usa le librerie NuGet per eseguire Restore e altri comandi supporterà percorsi lunghi sugli stessi sistemi su cui si basa NuGet. exe, se hanno anche impostato longPathAware nel manifesto di Windows e configurano UseLegacyPathHandling su false tramite app. config [ Vedi altre informazioni](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="2a154-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

