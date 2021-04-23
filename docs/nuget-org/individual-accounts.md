---
title: Account personali - NuGet.org
description: Per pubblicare i pacchetti sono necessari account personali in NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 5224a4f5be519e1d72285562c1611d047582f7de
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901564"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="14594-103">Account personali in NuGet.org</span><span class="sxs-lookup"><span data-stu-id="14594-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="14594-104">È necessario creare un account personale per pubblicare e gestire i pacchetti in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="14594-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="14594-105">Account personali e account aziendali</span><span class="sxs-lookup"><span data-stu-id="14594-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="14594-106">L'account personale (utente) è l'identità dell'utente in NuGet.org e può essere membro di un numero qualsiasi di organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="14594-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="14594-107">Un pacchetto può appartenere a un account aziendale come a un account individuale.</span><span class="sxs-lookup"><span data-stu-id="14594-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="14594-108">I consumer di pacchetti non notano differenze tra un account personale e l'account aziendale: entrambi vengono visualizzati come `owners` del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="14594-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="14594-109">Un account aziendale ha uno o più account personali come membri.</span><span class="sxs-lookup"><span data-stu-id="14594-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="14594-110">Questi membri possono gestire un set di pacchetti mantenendo un'unica identità per la proprietà.</span><span class="sxs-lookup"><span data-stu-id="14594-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="14594-111">Aggiungere un nuovo account personale</span><span class="sxs-lookup"><span data-stu-id="14594-111">Add a new individual account</span></span>

<span data-ttu-id="14594-112">Per creare un account di NuGet.org, è necessario avere un account Microsoft personale (MSA) o un account di Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="14594-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="14594-113">Se non se ne ha alcuno, è possibile [crearne uno](https://signup.live.com).</span><span class="sxs-lookup"><span data-stu-id="14594-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="14594-114">Se si ha un account Microsoft personale o un account di Azure Active Directory, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="14594-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="14594-115">Passare alla pagina [NuGet.org di accesso.](https://www.nuget.org/users/account/LogOn)</span><span class="sxs-lookup"><span data-stu-id="14594-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="14594-116">Fare clic sul pulsante **Sign in with Microsoft** (Accedi con Microsoft).</span><span class="sxs-lookup"><span data-stu-id="14594-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="14594-117">Immettere i dettagli dell'account Microsoft o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="14594-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="14594-118">Fare clic su **Yes** (Sì) per accettare le autorizzazioni da concedere all'applicazione *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="14594-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Concessione delle autorizzazioni a NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="14594-120">Si verrà reindirizzati a *nuget.org* e verrà richiesto di registrare un nome utente.</span><span class="sxs-lookup"><span data-stu-id="14594-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="14594-121">Specificare il nome utente nella casella di input.</span><span class="sxs-lookup"><span data-stu-id="14594-121">Specify the username in the input box.</span></span> <span data-ttu-id="14594-122">Si noti che il nome utente **fa** distinzione tra maiuscole e minuscole e non può essere cambiato o rinominato in seguito.</span><span class="sxs-lookup"><span data-stu-id="14594-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Specificare un nome utente in NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="14594-124">Fare clic **sul pulsante** Registra.</span><span class="sxs-lookup"><span data-stu-id="14594-124">Click the **Register** button.</span></span>

<span data-ttu-id="14594-125">Si ha ora un account di NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="14594-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="14594-126">È possibile eseguire la gestione degli account nella pagina [Account Settings](https://www.nuget.org/account) (Impostazioni account).</span><span class="sxs-lookup"><span data-stu-id="14594-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="14594-127">Abilitare l'autenticazione a due fattori (2FA)</span><span class="sxs-lookup"><span data-stu-id="14594-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="14594-128">L'autenticazione a due fattori, o 2FA, è un livello di sicurezza aggiuntivo usato per l'accesso a siti Web o app.</span><span class="sxs-lookup"><span data-stu-id="14594-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="14594-129">Con 2FA, è necessario accedere con l'account Microsoft (MSA) e fornire un'altra forma di autenticazione che solo l'utente conosce o a cui ha accesso.</span><span class="sxs-lookup"><span data-stu-id="14594-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="14594-130">Per migliorare la protezione dell'account, abilitare l'autenticazione a due fattori (scelta consigliata).</span><span class="sxs-lookup"><span data-stu-id="14594-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="14594-131">Quando si è connessi all'account, aprire il profilo e scegliere **Abilita** in **Account di accesso**.</span><span class="sxs-lookup"><span data-stu-id="14594-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Abilitare 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="14594-133">Verrà visualizzato un messaggio in cui viene indicato che al successivo accesso a *nuget.org* verranno richieste altre credenziali.</span><span class="sxs-lookup"><span data-stu-id="14594-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="14594-134">Per completare l'autenticazione in questo momento, disconnettersi e quindi accedere di nuovo.</span><span class="sxs-lookup"><span data-stu-id="14594-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="14594-135">Quando si accede, scegliere testo o posta elettronica come seconda forma di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="14594-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="14594-136">Verificare il numero di telefono o l'indirizzo di posta elettronica già associato all'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="14594-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="14594-137">Potrebbe essere necessario immettere un nuovo numero di telefono o un nuovo indirizzo di posta elettronica per l'account.</span><span class="sxs-lookup"><span data-stu-id="14594-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="14594-138">In tal caso, immettere le informazioni richieste come indicato e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="14594-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Abilitare 2FA e immettere il telefono](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="14594-140">Controllare il dispositivo o l'account di posta elettronica e immettere il codice appena inviato.</span><span class="sxs-lookup"><span data-stu-id="14594-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Abilitare 2FA e immettere il codice](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="14594-142">Seguire eventuali istruzioni aggiuntive per completare l'autenticazione a due fattori.</span><span class="sxs-lookup"><span data-stu-id="14594-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="14594-143">L'abilitazione di 2FA per l'account NuGet.org non influisce sulle impostazioni di autenticazione per altri account o servizi che potrebbero essere collegati al account Microsoft utilizzato per accedere a NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="14594-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="14594-144">Eliminare un account di NuGet.org</span><span class="sxs-lookup"><span data-stu-id="14594-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="14594-145">Per informazioni su altre attività correlate all'account, ad esempio l'eliminazione di un account NuGet.org , vedere [Gestione degli account di NuGet.org](nuget-org-faq.md#nugetorg-account-management).</span><span class="sxs-lookup"><span data-stu-id="14594-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
