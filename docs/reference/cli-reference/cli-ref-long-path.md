---
title: Supporto del percorso lungo dell'interfaccia della riga di comando NuGet
description: Informazioni di riferimento sul supporto per percorsi lunghi di NuGet. exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 9b5a97d963eab7fbbde4aefae1c9b1a8bfcdeb11
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036955"
---
# <a name="long-path-support-nuget-cli"></a>Supporto per percorsi lunghi (interfaccia della riga di comando NuGet)

**Si applica a:** tutte le versioni di &bullet; **supportate:** 4.8 +

NuGet. exe 4,8 e versioni successive supportano percorsi lunghi per file e directory per scenari come Pack, Restore, install e la maggior parte degli altri scenari che richiedono percorsi di file.

## <a name="required-operating-system"></a>Sistema operativo richiesto

-   Windows 10 (versione 1607 o successiva)
-   Windows 10 (versione luglio 2015 o 1511) se si esegue l'aggiornamento .NET Framework a versioni 4.6.2 o successive.
-   Windows Server 2016 (tutte le versioni)

## <a name="enable-win32-long-paths-group-policy"></a>Abilitare "percorsi lunghi Win32" Criteri di gruppo

È necessario abilitare il supporto per percorsi lunghi su tali sistemi impostando criteri di gruppo.

Passaggi:
1. Avviare **criteri di gruppo editor** : digitare "modifica criteri di gruppo" nella barra di ricerca iniziale o eseguire "gpedit. msc" dal comando Esegui (Windows-R).
2. Nella **Editor criteri di gruppo locali**abilitare "criteri computer locale/Configurazione computer/modelli amministrativi/tutte le impostazioni/Abilita percorsi lunghi Win32".

![Criterio percorso lungo](media/LongPathPolicy.png)


> [!Note]
> Abilitazione di altri strumenti NuGet per supportare percorsi lunghi
>
> -   L'interfaccia della riga di comando DotNet supporta percorsi lunghi indipendentemente dal sistema operativo o dalla versione.
> -   Visual Studio o `msbuild -t:restore` non supporta ancora percorsi lunghi.
> -   Il software che usa le librerie NuGet per eseguire Restore e altri comandi supporterà percorsi lunghi sugli stessi sistemi su cui è in esecuzione NuGet. exe, se hanno anche impostato `longPathAware` nel manifesto di Windows e configurano `UseLegacyPathHandling` per `false` tramite app. config. [vedere altre informazioni](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

