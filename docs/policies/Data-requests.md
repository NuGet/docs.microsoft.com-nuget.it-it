---
title: Richieste di dati degli utenti
description: Criteri per le richieste di esportazione ed eliminazione dei dati degli utenti
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2018
ms.locfileid: "33086204"
---
# <a name="user-data-requests"></a><span data-ttu-id="2c451-103">Richieste di dati degli utenti</span><span class="sxs-lookup"><span data-stu-id="2c451-103">User Data Requests</span></span>

<span data-ttu-id="2c451-104">Gli utenti di nuget.org possono inviare le richieste di eliminazione ed esportazione delle informazioni tramite [nuget.org](https://www.nuget.org). Entrambi i tipi vengono inviati sotto forma di richieste di supporto e vengono eseguiti dagli amministratori di nuget.org entro 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="2c451-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="2c451-105">I dati utente seguenti sono accessibili direttamente tramite nuget.org:</span><span class="sxs-lookup"><span data-stu-id="2c451-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="2c451-106">Dati relativi all'account, ad esempio indirizzo di posta elettronica, account di accesso, immagine del profilo e impostazioni di notifica tramite posta elettronica</span><span class="sxs-lookup"><span data-stu-id="2c451-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="2c451-107">Chiavi API di proprietà</span><span class="sxs-lookup"><span data-stu-id="2c451-107">Owned API Keys</span></span>
* <span data-ttu-id="2c451-108">Elenco dei pacchetti di proprietà</span><span class="sxs-lookup"><span data-stu-id="2c451-108">List of owned packages</span></span>

<span data-ttu-id="2c451-109">Questi dati non sono inclusi nei dati esportati tramite la richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="2c451-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="2c451-110">Identificazione dei dati dei clienti</span><span class="sxs-lookup"><span data-stu-id="2c451-110">Identifying customer data</span></span>

<span data-ttu-id="2c451-111">I dati dei clienti possono essere identificati come nomi di account utente di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2c451-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="2c451-112">Eliminazione dei dati dei clienti</span><span class="sxs-lookup"><span data-stu-id="2c451-112">Deleting customer data</span></span>

<span data-ttu-id="2c451-113">Per richiedere l'eliminazione dei dati degli utenti da nuget.org:</span><span class="sxs-lookup"><span data-stu-id="2c451-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="2c451-114">L'utente deve accedere a [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="2c451-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="2c451-115">L'utente deve inviare una richiesta di eliminazione del proprio account [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="2c451-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="2c451-116">Gli utenti che sono gli unici proprietari dei pacchetti sono invitati a trovare nuovi proprietari prima di richiedere l'eliminazione del proprio account.</span><span class="sxs-lookup"><span data-stu-id="2c451-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="2c451-117">Se non è possibile trasferire la proprietà del pacchetto, il pacchetto NuGet viene escluso dall'elenco e, di conseguenza, non è più disponibile nelle query di ricerca in Visual Studio o nel sito Web nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2c451-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="2c451-118">Prima di eliminare l'account, gli amministratori di nuget.org collaborano con l'utente per trovare nuovi proprietari per i pacchetti di loro proprietà.</span><span class="sxs-lookup"><span data-stu-id="2c451-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="2c451-119">L'azione di eliminazione dell'account viene completata dall'amministratore di nuget.org entro 30 giorni dalla data della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2c451-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="2c451-120">In seguito all'eliminazione dell'account, tutti i dati dell'utente vengono rimossi dal sistema nuget.org e vengono eseguite le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2c451-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="2c451-121">L'account eliminato diventa non registrato con nuget.org</span><span class="sxs-lookup"><span data-stu-id="2c451-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="2c451-122">Tutte le chiavi API di proprietà vengono eliminate</span><span class="sxs-lookup"><span data-stu-id="2c451-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="2c451-123">Tutti gli spazi dei nomi riservati vengono rilasciati</span><span class="sxs-lookup"><span data-stu-id="2c451-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="2c451-124">Tutte le proprietà dei pacchetti vengono rimosse</span><span class="sxs-lookup"><span data-stu-id="2c451-124">Any package ownership are removed</span></span>

<span data-ttu-id="2c451-125">I pacchetti di proprietà *non* vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="2c451-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="2c451-126">Anche se rimossi dall'elenco dei risultati della ricerca, rimangono disponibili tramite il ripristino del pacchetto per i progetti che dipendono da essi.</span><span class="sxs-lookup"><span data-stu-id="2c451-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="2c451-127">Esportazione dei dati dei clienti</span><span class="sxs-lookup"><span data-stu-id="2c451-127">Exporting customer data</span></span>

<span data-ttu-id="2c451-128">Dopo l'accesso a nuget.org, un utente può inviare una richiesta di esportazione tramite [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="2c451-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="2c451-129">I dati esportati vengono resi disponibili per 48 ore all'utente per il download tramite un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c451-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="2c451-130">Dopo 48 ore, l'accesso scade e l'utente deve inviare una nuova richiesta di esportazione in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="2c451-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="2c451-131">I dati esportati includono:</span><span class="sxs-lookup"><span data-stu-id="2c451-131">The exported data includes:</span></span>

* <span data-ttu-id="2c451-132">Le richieste di supporto dell'utente</span><span class="sxs-lookup"><span data-stu-id="2c451-132">The user's support requests</span></span>
* <span data-ttu-id="2c451-133">Le azioni dell'utente (pubblicazione del pacchetto, creazione di account) come resi persistenti nei log di controllo</span><span class="sxs-lookup"><span data-stu-id="2c451-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="2c451-134">Le informazioni sull'utente come rese persistenti nei log di IIS</span><span class="sxs-lookup"><span data-stu-id="2c451-134">Any user information as persisted in the IIS logs</span></span>
