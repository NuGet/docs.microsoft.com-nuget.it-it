---
title: Note sulla versione di NuGet 3.0 RC2
description: Note sulla versione per NuGet 3.0 RC2 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545821"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="8992e-103">Note sulla versione di NuGet 3.0 RC2</span><span class="sxs-lookup"><span data-stu-id="8992e-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="8992e-104">[Note sulla versione per NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [note sulla versione di NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="8992e-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="8992e-105">NuGet 3.0 RC2 è stato rilasciato 3 giugno 2015 come una versione provvisoria disponibile dalla raccolta di estensione di Visual Studio 2015 e [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="8992e-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="8992e-106">Questa versione include numerose correzioni di bug importanti e miglioramenti delle prestazioni che è stato ritenuto erano importanti per rilasciare prima del rilascio di Visual Studio 2015 completato.</span><span class="sxs-lookup"><span data-stu-id="8992e-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="8992e-107">Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8992e-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="8992e-108">In totale, abbiamo chiuso 158 problemi in questa versione, ed è possibile esaminare i [elenco completo dei problemi in GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="8992e-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="8992e-109">Riepilogo dei principali problemi risolti</span><span class="sxs-lookup"><span data-stu-id="8992e-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="8992e-110">Aggiornamenti frequenti rete viene chiamato quando viene aggiornata la finestra di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="8992e-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="8992e-111">Scorrimento un ritardo se la modifica in installato visualizzazione in Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="8992e-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="8992e-112">Le chiamate di rete devono essere eseguite su un thread in background</span><span class="sxs-lookup"><span data-stu-id="8992e-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="8992e-113">Aggiungere la casella di controllo 'Non visualizzare la finestra di anteprima'</span><span class="sxs-lookup"><span data-stu-id="8992e-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="8992e-114">Processo aggiunto la limitazione per ridurre l'utilizzo del processore</span><span class="sxs-lookup"><span data-stu-id="8992e-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="8992e-115">Migliorata la gestione dei riferimenti di libreria di classi portabile</span><span class="sxs-lookup"><span data-stu-id="8992e-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="8992e-116">Servizio di completamento automatico è stato in maiuscole / minuscole</span><span class="sxs-lookup"><span data-stu-id="8992e-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="8992e-117">Aggiornamento reintrodurre le credenziali di autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="8992e-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="8992e-118">Registrazione degli errori migliorata</span><span class="sxs-lookup"><span data-stu-id="8992e-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="8992e-119">Messaggi di errore migliorata powershell quando si chiama Update-Package</span><span class="sxs-lookup"><span data-stu-id="8992e-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="8992e-120">Scaricare questa app [aggiornare l'estensione NuGet](https://nuget.codeplex.com/releases/view/615507) da Codeplex e teniamo d'occhio [nostro blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="8992e-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>