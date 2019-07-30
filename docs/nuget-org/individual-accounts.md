---
title: Account personali
description: Per pubblicare i pacchetti sono necessari account personali in NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: c88b88015bd6d5bae4789765126c0a3dec527e24
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419878"
---
# <a name="individual-accounts"></a>Account personali

È necessario creare un account personale per pubblicare e gestire i pacchetti in NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Account personali e account aziendali

L'account personale (utente) è l'identità dell'utente in NuGet.org e può essere membro di un numero qualsiasi di organizzazioni. Un pacchetto può appartenere a un account aziendale come a un account personale. I consumer di pacchetti non vedono alcuna differenza tra un account personale e l'account aziendale: entrambi vengono visualizzati come pacchetto `owners`.

Un account aziendale ha uno o più account personali come membri. Questi membri possono gestire un set di pacchetti mantenendo un'unica identità per la proprietà.

## <a name="add-a-new-individual-account"></a>Aggiungere un nuovo account personale

Per creare un account di NuGet.org, è necessario avere un account Microsoft personale (MSA) o un account di Azure Active Directory (AAD). Se non se ne ha alcuno, è possibile [crearne uno](https://signup.live.com). Se si ha un account Microsoft personale o un account di Azure Active Directory, seguire questa procedura.

1. Andare alla [pagina di accesso di NuGet.org](https://www.nuget.org/users/account/LogOn).

1. Fare clic sul pulsante **Sign in with Microsoft** (Accedi con Microsoft).

1. Immettere i dettagli dell'account Microsoft o Azure Active Directory.

1. Fare clic su **Yes** (Sì) per accettare le autorizzazioni da concedere all'applicazione *NuGet.org*.

   ![Concessione delle autorizzazioni a NuGet.org](media/nuget-org-permissions.png)

1. Verrà eseguito il reindirizzamento a *nuget.org* e verrà chiesto di registrare un nome utente.

1. Specificare il nome utente nella casella di input. Si noti che il nome utente **fa** distinzione tra maiuscole e minuscole e non può essere cambiato o rinominato in seguito.

   ![Specificare un nome utente in NuGet.org](media/nuget-org-register.png) 

1. Fare clic sul pulsante **Register** (Registra).

Si ha ora un account di NuGet.org. È possibile eseguire la gestione degli account nella pagina [Account Settings](https://www.nuget.org/account) (Impostazioni account).

## <a name="enable-two-factor-authentication-2fa"></a>Abilitare l'autenticazione a due fattori (2FA)

Per migliorare la protezione dell'account, abilitare l'autenticazione a due fattori (scelta consigliata).

1. Quando si è connessi all'account, aprire il profilo e scegliere **Abilita** in **Account di accesso**.

   ![Abilitare 2FA](media/nuget-org-register-2fa.png)

   Verrà visualizzato un messaggio in cui viene indicato che al successivo accesso a *nuget.org* verranno richieste altre credenziali.

2. Per completare l'autenticazione in questo momento, disconnettersi e quindi accedere di nuovo.

3. Quando si accede, scegliere testo o posta elettronica come seconda forma di autenticazione.

   Verificare il numero di telefono o l'indirizzo di posta elettronica già associato all'account Microsoft. Potrebbe essere necessario immettere un nuovo numero di telefono o un nuovo indirizzo di posta elettronica per l'account. In tal caso, immettere le informazioni richieste come indicato e quindi fare clic su **Avanti**.

   ![Abilitare 2FA](media/nuget-org-sign-in-2fa.png)

4. Controllare il dispositivo o l'account di posta elettronica e immettere il codice appena inviato.

   ![Abilitare 2FA](media/nuget-org-enter-code-2fa.png)

5. Seguire eventuali istruzioni aggiuntive per completare l'autenticazione a due fattori.
