---
title: Note sulla versione di NuGet 3.0 RC2
description: Note sulla versione per NuGet 3.0 RC2 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eb8b514fa967cc6ef850483b6b2a5df3ab27a550
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="997cc-103">Note sulla versione di NuGet 3.0 RC2</span><span class="sxs-lookup"><span data-stu-id="997cc-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="997cc-104">[Note sulla versione RC di NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [note sulla versione di NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="997cc-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="997cc-105">NuGet 3.0 RC2 è stata rilasciata 3 giugno 2015 come una versione provvisoria dalla raccolta di estensioni di Visual Studio 2015 e [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="997cc-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="997cc-106">Questa versione include un numero di importanti correzioni di bug e miglioramenti delle prestazioni che è stato ritenuto sono importanti per rilasciare prima del rilascio di Visual Studio 2015 completato.</span><span class="sxs-lookup"><span data-stu-id="997cc-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="997cc-107">Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="997cc-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="997cc-108">In totale, ci chiusura 158 problemi in questa versione, quindi è possibile esaminare il [elenco completo dei problemi su GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="997cc-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="997cc-109">Riepilogo dei principali problemi risolti</span><span class="sxs-lookup"><span data-stu-id="997cc-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="997cc-110">Aggiornamento rete frequenti viene chiamato quando viene aggiornata la finestra di gestione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="997cc-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="997cc-111">Ritardo scorrimento installato modifica per visualizzare in Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="997cc-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="997cc-112">Chiamate di rete devono essere eseguite su un thread in background</span><span class="sxs-lookup"><span data-stu-id="997cc-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="997cc-113">Aggiunta una casella di controllo 'Non visualizzare la finestra di anteprima'</span><span class="sxs-lookup"><span data-stu-id="997cc-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="997cc-114">Processo aggiunto la limitazione delle richieste per ridurre l'utilizzo del processore</span><span class="sxs-lookup"><span data-stu-id="997cc-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="997cc-115">Migliorare la gestione dei riferimenti di libreria di classi portabile</span><span class="sxs-lookup"><span data-stu-id="997cc-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="997cc-116">Servizio di completamento automatico è stata fatta distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="997cc-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="997cc-117">Aggiornamento di ripristinare le credenziali di autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="997cc-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="997cc-118">Registrazione migliorata degli errori</span><span class="sxs-lookup"><span data-stu-id="997cc-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="997cc-119">Messaggi di errore migliorata powershell durante la chiamata pacchetto di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="997cc-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="997cc-120">Scaricare questo [aggiornare l'estensione NuGet](https://nuget.codeplex.com/releases/view/615507) da Codeplex, tenere d'occhio [blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="997cc-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>