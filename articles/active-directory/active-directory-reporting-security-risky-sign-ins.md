---
title: Rapporten om riskfyllda inloggningar i Azure Active Directory-portalen | Microsoft Docs
description: "Lär dig mer om rapporten över riskfyllda inloggningar i Azure Active Directory-portalen"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.translationtype: Human Translation
ms.sourcegitcommit: 2db2ba16c06f49fd851581a1088df21f5a87a911
ms.openlocfilehash: e21b7733bc0f6b8625fbdcec3529ad603ce306c1
ms.contentlocale: sv-se
ms.lasthandoff: 05/08/2017

---
# Rapporten över riskfyllda inloggningar i Azure Active Directory-portalen
<a id="risky-sign-ins-report-in-the-azure-active-directory-portal" class="xliff"></a>

Med hjälp av säkerhetsrapporterna i Azure Active Directory (Azure AD) kan du bedöma risken för att användarkonton i din miljö har komprometterats. 

Azure AD identifierar misstänkta åtgärder relaterade till dina användarkonton. För varje identifierad åtgärd skapas en post med namnet *riskhändelse*. Mer information finns i avsnittet om [Azure Active Directory-riskhändelser](active-directory-identity-protection-risk-events.md). 

De identifierade riskhändelserna används för att beräkna:

- **Riskfyllda inloggningar** – En riskfylld inloggning indikerar ett potentiellt inloggningsförsök av någon annan än användarkontots ägare. Mer information finns i avsnittet om [riskfyllda inloggningar](active-directory-identityprotection.md#risky-sign-ins). 

- **Användare som har flaggats för risk** – En användare som har flaggats för risk indikerar att ett användarkonto kan ha komprometterats. Mer information finns i avsnittet om [användare som har flaggats för risk](active-directory-identityprotection.md#users-flagged-for-risk).  

I [Azure Portal](https://portal.azure.com) hittar du säkerhetsrapporter på bladet **Azure Active Directory** i avsnittet **Säkerhet**. 

![Riskfyllda inloggningar](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## Azure Active Directory kostnadsfri och grundläggande utgåva
<a id="azure-active-directory-free-and-basic-edition" class="xliff"></a>

Den grundläggande och den kostnadsfria versionen av Azure Active Directory tillhandahåller en lista över riskfyllda inloggningar som har identifierats för dina användare. Rapporten över riskhändelser innehåller följande information:

- **Användare** – Namnet på användaren som användes vid inloggningen.
- **IP-adress** – IP-adressen för enheten som användes för att ansluta till Azure Active Directory.
- **Plats** – Platsen som används för att ansluta till Azure Active Directory.
- **Inloggningstid** – Tidpunkten för inloggningen.
- **Status** – Inloggningens status.

Rapporten tillhandahåller ett alternativ för att hämta rapportdata.

![Riskfyllda inloggningar](./media/active-directory-reporting-security-risky-sign-ins/01.png)

Baserat på din undersökning av den riskfyllda inloggningen kan du lämna feedback till Azure Active Directory genom någon av följande åtgärder:

- Lös
- Markera som falskt positivt resultat
- Ignorera
- Återaktivera

![Riskfyllda inloggningar](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Mer information finns i [Stänga riskhändelser manuellt](active-directory-identityprotection.md#closing-risk-events-manually).

## Azure Active Directory Premium-versioner
<a id="azure-active-directory-premium-editions" class="xliff"></a>

Rapporten om riskfyllda inloggningar i Azure Active Directory Premium-versionerna ger dig följande:

- Sammanställd information om de [riskhändelsetyper](active-directory-identity-protection-risk-events.md) som har identifierats

- Ett alternativ för att ladda ned rapporten


![Riskfyllda inloggningar](./media/active-directory-reporting-security-risky-sign-ins/456.png)


När du väljer en riskhändelse kan få en detaljerad rapportvy för den här riskhändelsen som gör att du kan göra följande:

- Ett alternativ för att konfigurera en [princip för att åtgärda användarrisker](active-directory-identityprotection.md#user-risk-security-policy)  

- Granska identifieringstidslinjen för riskhändelsen  

- Granska en lista över användare för vilka den här riskhändelsen har upptäckts

- [Stänga riskhändelser manuellt](active-directory-identityprotection.md#closing-risk-events-manually) eller återaktivera en manuellt stängd riskhändelse. 


![Riskfyllda inloggningar](./media/active-directory-reporting-security-risky-sign-ins/457.png)

När du väljer en användare får du en detaljerad rapportvy för den här användaren som du kan använda för att göra följande:

- Öppna vyn Alla inloggningar

- Återställ användarens lösenord

- Ignorera alla händelser

- Undersök rapporterade riskhändelser för användaren. 


![Riskfyllda inloggningar](./media/active-directory-reporting-security-risky-sign-ins/324.png)


Välj en riskhändelse i listan om du vill undersöka den.  
Detta öppnar bladet **Information** för den här riskhändelsen. På bladet **Information** har du möjlighet att antingen [stänga en riskhändelse manuellt](active-directory-identityprotection.md#closing-risk-events-manually) eller återaktivera en manuellt stängd riskhändelse. 


![Riskfyllda inloggningar](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## Nästa steg
<a id="next-steps" class="xliff"></a>

- Mer information om Azure Active Directory Identity Protection finns i [Azure Active Directory Identity Protection](active-directory-identityprotection.md).


