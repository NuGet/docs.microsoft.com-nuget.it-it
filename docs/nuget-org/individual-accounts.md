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
