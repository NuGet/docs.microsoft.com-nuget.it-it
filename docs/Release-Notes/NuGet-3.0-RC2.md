---
title: Note sulla versione di NuGet 3.0 RC2 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 3.0 RC2 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "NuGet 3.0 RC2 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67299408170ae3c3676c2866bec2945b41ad4184
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="7be5a-104">Note sulla versione di NuGet 3.0 RC2</span><span class="sxs-lookup"><span data-stu-id="7be5a-104">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="7be5a-105">[Note sulla versione RC di NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [note sulla versione di NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="7be5a-105">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="7be5a-106">NuGet 3.0 RC2 è stata rilasciata 3 giugno 2015 come una versione provvisoria dalla raccolta di estensioni di Visual Studio 2015 e [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="7be5a-106">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="7be5a-107">Questa versione include un numero di importanti correzioni di bug e miglioramenti delle prestazioni che è stato ritenuto sono importanti per rilasciare prima del rilascio di Visual Studio 2015 completato.</span><span class="sxs-lookup"><span data-stu-id="7be5a-107">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="7be5a-108">Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7be5a-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="7be5a-109">In totale, ci chiusura 158 problemi in questa versione, quindi è possibile esaminare il [elenco completo dei problemi su GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="7be5a-109">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="7be5a-110">Riepilogo dei principali problemi risolti</span><span class="sxs-lookup"><span data-stu-id="7be5a-110">Summary of top issues resolved</span></span>

* [<span data-ttu-id="7be5a-111">Aggiornamento rete frequenti viene chiamato quando viene aggiornata la finestra di gestione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="7be5a-111">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="7be5a-112">Ritardo scorrimento installato modifica per visualizzare in Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="7be5a-112">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="7be5a-113">Chiamate di rete devono essere eseguite su un thread in background</span><span class="sxs-lookup"><span data-stu-id="7be5a-113">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="7be5a-114">Aggiunta una casella di controllo 'Non visualizzare la finestra di anteprima'</span><span class="sxs-lookup"><span data-stu-id="7be5a-114">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="7be5a-115">Processo aggiunto la limitazione delle richieste per ridurre l'utilizzo del processore</span><span class="sxs-lookup"><span data-stu-id="7be5a-115">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="7be5a-116">Migliorare la gestione dei riferimenti di libreria di classi portabile</span><span class="sxs-lookup"><span data-stu-id="7be5a-116">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="7be5a-117">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="7be5a-117">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="7be5a-118">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="7be5a-118">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="7be5a-119">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="7be5a-119">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="7be5a-120">Servizio di completamento automatico è stata fatta distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="7be5a-120">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="7be5a-121">Aggiornamento di ripristinare le credenziali di autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="7be5a-121">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="7be5a-122">Registrazione migliorata degli errori</span><span class="sxs-lookup"><span data-stu-id="7be5a-122">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="7be5a-123">Messaggi di errore migliorata powershell durante la chiamata pacchetto di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="7be5a-123">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="7be5a-124">Scaricare questo [aggiornare l'estensione NuGet](https://nuget.codeplex.com/releases/view/615507) da Codeplex, tenere d'occhio [blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="7be5a-124">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>