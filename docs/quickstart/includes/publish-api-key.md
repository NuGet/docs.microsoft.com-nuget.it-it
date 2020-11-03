---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "68419912"
---
1. [Accedere all'account personale di nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) o creare un account, se non è già disponibile.

   Per altre informazioni sulla creazione dell'account, vedere [Account singoli](../../nuget-org/individual-accounts.md).

1. Selezionare il nome utente (in alto a destra) e quindi selezionare **API Keys** (Chiavi API).

1. Selezionare **Create** (Crea), specificare un nome per la chiave, selezionare **Select Scopes > Push** (Seleziona ambiti > Push). Immettere * per **Glob pattern** (Criterio GLOB) e quindi selezionare **Create** (Crea). (Vedere di seguito per altre informazioni sugli ambiti.)

1. Dopo avere creato la chiave, selezionare **Copia** per recuperare la chiave di accesso necessaria nell'interfaccia della riga di comando:

    ![Copia della chiave API negli Appunti](../media/QS_Create-02-APIKey.png)

1. **Importante** : salvare la chiave in un luogo sicuro, perché non è possibile copiare la chiave nuovamente in seguito. Se si torna alla pagina della chiave API, è necessario rigenerarla per copiarla. È anche possibile rimuovere la chiave API se non si vuole più eseguire il push tramite l'interfaccia della riga di comando.

L'assegnazione degli ambiti consente di creare chiavi API separate per scopi diversi. Per ogni chiave esiste un intervallo di tempo di scadenza ed è possibile specificare un ambito limitato a pacchetti (o criteri GLOB) specifici. L'ambito per ogni chiave può essere anche limitato a operazioni specifiche: push di nuovi pacchetti e aggiornamenti, push solo degli aggiornamenti o rimozione dall'elenco. Tramite l'assegnazione di un ambito, è possibile creare chiavi API per i diversi utenti che gestiscono i pacchetti per l'organizzazione in modo che abbiamo solo le autorizzazioni necessarie. Per altre informazioni, vedere [Chiavi API con ambito](../../nuget-org/scoped-api-keys.md).