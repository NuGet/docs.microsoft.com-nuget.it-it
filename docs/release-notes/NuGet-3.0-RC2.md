---
title: Note sulla versione di NuGet 3,0 RC2
description: Note sulla versione per NuGet 3,0 RC2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780281"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="9b150-103">Note sulla versione di NuGet 3,0 RC2</span><span class="sxs-lookup"><span data-stu-id="9b150-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="9b150-104">Note sulla versione di [NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Note sulla versione di NuGet 3,0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="9b150-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="9b150-105">NuGet 3,0 RC2 è stato rilasciato il 3 giugno 2015 come versione provvisoria disponibile dalla raccolta di estensioni di Visual Studio 2015 e da [codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="9b150-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="9b150-106">Questa versione include alcune importanti correzioni di bug e miglioramenti delle prestazioni ritenuti importanti per il rilascio prima della versione completa di Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9b150-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="9b150-107">Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9b150-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="9b150-108">In totale, sono stati chiusi 158 problemi in questa versione ed è possibile esaminare l' [elenco completo dei problemi in GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="9b150-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="9b150-109">Riepilogo dei principali problemi risolti</span><span class="sxs-lookup"><span data-stu-id="9b150-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="9b150-110">Frequenti chiamate di aggiornamento della rete quando viene aggiornata la finestra di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="9b150-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="9b150-111">Scorrimento ritardato durante la modifica della visualizzazione installata in Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="9b150-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="9b150-112">Le chiamate di rete devono essere eseguite in un thread in background</span><span class="sxs-lookup"><span data-stu-id="9b150-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="9b150-113">È stata aggiunta la casella di controllo ' non visualizzare la finestra di anteprima '</span><span class="sxs-lookup"><span data-stu-id="9b150-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="9b150-114">Aggiunta limitazione del processo per ridurre l'utilizzo del processore</span><span class="sxs-lookup"><span data-stu-id="9b150-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="9b150-115">Gestione migliorata dei riferimenti alla libreria di classi portabile</span><span class="sxs-lookup"><span data-stu-id="9b150-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="9b150-116">Distinzione tra maiuscole e minuscole per il servizio AutoComplete</span><span class="sxs-lookup"><span data-stu-id="9b150-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="9b150-117">Aggiornare per reintrodurre le credenziali di autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="9b150-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="9b150-118">È stata migliorata la registrazione degli errori</span><span class="sxs-lookup"><span data-stu-id="9b150-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="9b150-119">Messaggi di errore di PowerShell migliorati quando si chiama Update-Package</span><span class="sxs-lookup"><span data-stu-id="9b150-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="9b150-120">Scaricare questo [aggiornamento nell'estensione NuGet](https://nuget.codeplex.com/releases/view/615507) da CodePlex e tenere sotto controllo il [Blog](http://blog.nuget.org) per altri progressi e annunci per NuGet 3,0!</span><span class="sxs-lookup"><span data-stu-id="9b150-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>