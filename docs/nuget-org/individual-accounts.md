---
title: Account personali - NuGet.org
description: Per pubblicare i pacchetti sono necessari account personali in NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: d032b69f6eb4cbd3687ca60190c15aed9b7a4d79
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323895"
---
# <a name="individual-accounts-on-nugetorg"></a>Account personali in NuGet.org

È necessario creare un account personale per pubblicare e gestire i pacchetti in NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Account personali e account aziendali

L'account personale (utente) è l'identità dell'utente in NuGet.org e può essere membro di un numero qualsiasi di organizzazioni. Un pacchetto può appartenere a un account aziendale come a un account individuale. I consumer di pacchetti non notano differenze tra un account personale e l'account aziendale: entrambi vengono visualizzati come `owners` del pacchetto.

Un account aziendale ha uno o più account personali come membri. Questi membri possono gestire un set di pacchetti mantenendo un'unica identità per la proprietà.

## <a name="add-a-new-individual-account"></a>Aggiungere un nuovo account personale

Per creare un account di NuGet.org, è necessario avere un account Microsoft personale (MSA) o un account di Azure Active Directory (AAD). Se non se ne ha alcuno, è possibile [crearne uno](https://signup.live.com). Se si ha un account Microsoft personale o un account di Azure Active Directory, seguire questa procedura.

1. Passare alla pagina [NuGet.org di accesso.](https://www.nuget.org/users/account/LogOn)

1. Fare clic sul pulsante **Sign in with Microsoft** (Accedi con Microsoft).

1. Immettere i dettagli dell'account Microsoft o Azure Active Directory.

1. Fare clic su **Yes** (Sì) per accettare le autorizzazioni da concedere all'applicazione *NuGet.org*.

   ![Concessione delle autorizzazioni a NuGet.org](media/nuget-org-permissions.png)

1. Si verrà reindirizzati a *nuget.org* e verrà richiesto di registrare un nome utente.

1. Specificare il nome utente nella casella di input. Si noti che il nome utente **fa** distinzione tra maiuscole e minuscole e non può essere cambiato o rinominato in seguito.

   ![Specificare un nome utente in NuGet.org](media/nuget-org-register.png) 

1. Fare clic **sul pulsante** Registra.

Si ha ora un account di NuGet.org. È possibile eseguire la gestione degli account nella pagina [Account Settings](https://www.nuget.org/account) (Impostazioni account).

## <a name="enable-two-factor-authentication-2fa"></a>Abilitare l'autenticazione a due fattori (2FA)

L'autenticazione a due fattori, o 2FA, è un livello di sicurezza aggiuntivo usato per l'accesso a siti Web o app. Con 2FA, è necessario accedere con l'account Microsoft (MSA) e fornire un'altra forma di autenticazione che solo l'utente conosce o a cui ha accesso. Per migliorare la protezione dell'account, abilitare l'autenticazione a due fattori (scelta consigliata).

1. Quando si è connessi all'account, aprire il profilo e scegliere **Abilita** in **Account di accesso**.

   ![Abilitare 2FA](media/nuget-org-register-2fa.png)

   Verrà visualizzato un messaggio in cui viene indicato che al successivo accesso a *nuget.org* verranno richieste altre credenziali.

2. Per completare l'autenticazione in questo momento, disconnettersi e quindi accedere di nuovo.

3. Quando si accede, scegliere testo o posta elettronica come seconda forma di autenticazione.

   Verificare il numero di telefono o l'indirizzo di posta elettronica già associato all'account Microsoft. Potrebbe essere necessario immettere un nuovo numero di telefono o un nuovo indirizzo di posta elettronica per l'account. In tal caso, immettere le informazioni richieste come indicato e quindi fare clic su **Avanti**.

   ![Abilitare 2FA e immettere il telefono](media/nuget-org-sign-in-2fa.png)

4. Controllare il dispositivo o l'account di posta elettronica e immettere il codice appena inviato.

   ![Abilitare 2FA e immettere il codice](media/nuget-org-enter-code-2fa.png)

5. Seguire eventuali istruzioni aggiuntive per completare l'autenticazione a due fattori.

> [!Tip]
> L'abilitazione di 2FA per l'account NuGet.org non influisce sulle impostazioni di autenticazione per altri account o servizi che potrebbero essere collegati al account Microsoft utilizzato per accedere a NuGet.org.

## <a name="delete-a-nugetorg-account"></a>Eliminare un account di NuGet.org

Per informazioni su altre attività correlate all'account, ad esempio l'eliminazione di un account NuGet.org , vedere [Gestione degli account di NuGet.org](/nuget/nuget-org/nuget-org-faq#nuget.org-account-management).
