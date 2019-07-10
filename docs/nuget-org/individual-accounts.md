---
title: Account personali
description: Per pubblicare i pacchetti sono necessari account personali in NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427136"
---
# <a name="individual-accounts"></a><span data-ttu-id="997b6-103">Account personali</span><span class="sxs-lookup"><span data-stu-id="997b6-103">Individual accounts</span></span>

<span data-ttu-id="997b6-104">È necessario creare un account personale per pubblicare e gestire i pacchetti in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="997b6-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="997b6-105">Account personali e account aziendali</span><span class="sxs-lookup"><span data-stu-id="997b6-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="997b6-106">L'account personale (utente) è l'identità dell'utente in NuGet.org e può essere membro di un numero qualsiasi di organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="997b6-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="997b6-107">Un pacchetto può appartenere a un account aziendale come a un account personale.</span><span class="sxs-lookup"><span data-stu-id="997b6-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="997b6-108">I consumer di pacchetti non vedono alcuna differenza tra un account personale e l'account aziendale: entrambi vengono visualizzati come pacchetto `owners`.</span><span class="sxs-lookup"><span data-stu-id="997b6-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="997b6-109">Un account aziendale ha uno o più account personali come membri.</span><span class="sxs-lookup"><span data-stu-id="997b6-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="997b6-110">Questi membri possono gestire un set di pacchetti mantenendo un'unica identità per la proprietà.</span><span class="sxs-lookup"><span data-stu-id="997b6-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="997b6-111">Aggiungere un nuovo account personale</span><span class="sxs-lookup"><span data-stu-id="997b6-111">Add a new individual account</span></span>

<span data-ttu-id="997b6-112">Per creare un account di NuGet.org, è necessario avere un account Microsoft personale (MSA) o un account di Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="997b6-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="997b6-113">Se non se ne ha alcuno, è possibile [crearne uno](https://signup.live.com).</span><span class="sxs-lookup"><span data-stu-id="997b6-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="997b6-114">Se si ha un account Microsoft personale o un account di Azure Active Directory, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="997b6-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="997b6-115">Andare alla [pagina di accesso di NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="997b6-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="997b6-116">Fare clic sul pulsante **Sign in with Microsoft** (Accedi con Microsoft).</span><span class="sxs-lookup"><span data-stu-id="997b6-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="997b6-117">Immettere i dettagli dell'account Microsoft o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="997b6-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="997b6-118">Fare clic su **Yes** (Sì) per accettare le autorizzazioni da concedere all'applicazione *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="997b6-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Concessione delle autorizzazioni a NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="997b6-120">Verrà eseguito il reindirizzamento a *nuget.org* e verrà chiesto di registrare un nome utente.</span><span class="sxs-lookup"><span data-stu-id="997b6-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="997b6-121">Specificare il nome utente nella casella di input.</span><span class="sxs-lookup"><span data-stu-id="997b6-121">Specify the username in the input box.</span></span> <span data-ttu-id="997b6-122">Si noti che il nome utente **fa** distinzione tra maiuscole e minuscole e non può essere cambiato o rinominato in seguito.</span><span class="sxs-lookup"><span data-stu-id="997b6-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Specificare un nome utente in NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="997b6-124">Fare clic sul pulsante **Register** (Registra).</span><span class="sxs-lookup"><span data-stu-id="997b6-124">Click the **Register** button.</span></span>

<span data-ttu-id="997b6-125">Si ha ora un account di NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="997b6-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="997b6-126">È possibile eseguire la gestione degli account nella pagina [Account Settings](https://www.nuget.org/account) (Impostazioni account).</span><span class="sxs-lookup"><span data-stu-id="997b6-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
