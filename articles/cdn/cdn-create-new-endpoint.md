---
title: "Komma igång med Azure CDN | Microsoft Docs"
description: "Det här avsnittet beskriver hur du aktiverar Azure Content Delivery Network (CDN). Självstudiekursen beskriver steg för steg hur du skapar en ny CDN-profil och CDN-slutpunkt."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
translationtype: Human Translation
ms.sourcegitcommit: bdf6e27463fcc6186a3b15a55653fa468da91bdc
ms.openlocfilehash: d263e911d0d0b3cdc1e48e300a3c8a0994b38c39


---
# <a name="getting-started-with-azure-cdn"></a>Komma igång med Azure CDN
Det här avsnittet beskriver steg för steg hur du aktiverar Azure CDN genom att skapa en ny profil och slutpunkt för CDN.

> [!IMPORTANT]
> En introduktion till hur CDN fungerar, samt en lista över funktioner, finns i [Översikt över CDN](cdn-overview.md).
> 
> 

## <a name="create-a-new-cdn-profile"></a>Skapa en ny CDN-profil
En CDN-profil är en samling CDN-slutpunkter.  Varje profil innehåller en eller flera CDN-slutpunkter.  Du kanske vill använda flera profiler för att organisera dina CDN-slutpunkter efter Internetdomän, webbapp eller andra kriterier.

> [!NOTE]
> Som standard är en enskild Azure-prenumeration begränsad till åtta CDN-profiler. Varje CDN-profil är begränsad till tio CDN-slutpunkter.
> 
> CDN-priserna tillämpas på CDN-profilnivå. Om du vill använda en kombination av olika Azure CDN-prisnivåer behöver du flera CDN-profiler.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Skapa en ny CDN-slutpunkt
**Så här skapar du en ny CDN-slutpunkt**

1. Gå till din CDN-profil på [Azure-portalen](https://portal.azure.com).  Du kanske fäste den på instrumentpanelen i föregående steg.  Om du inte hittar den klicka du på **Bläddra**, sedan på **CDN-profiler** och sedan på den profil som du vill lägga till slutpunkten till.
   
    Bladet för CDN-profilen visas.
   
    ![CDN-profil][cdn-profile-settings]
2. Klicka på knappen **Lägg till slutpunkt**.
   
    ![Knappen Lägg till slutpunkt][cdn-new-endpoint-button]
   
    Bladet **Lägg till slutpunkt** visas.
   
    ![Bladet Lägg till slutpunkt][cdn-add-endpoint]
3. Ange ett **namn** för den här CDN-slutpunkten.  Det här namnet används för att komma åt dina cachelagrade resurser i domänen `<endpointname>.azureedge.net`.
4. I listrutan **Typ av ursprung** väljer du typ av ursprung.  Välj **Storage** för ett Azure Storage-konto, **Cloud Services** för ett Azure Cloud Services-konto, **Web Apps** för ett Azure Web Apps-konto eller **Anpassat ursprung** för ett annat ursprung i form av en offentligt tillgänglig webbserver (som finns i Azure eller någon annanstans).
   
    ![Ursprungstyp för CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. I listrutan **Ursprungets värdnamn** väljer du eller skriver din ursprungliga domän.  Listrutan visar en lista över alla tillgängliga ursprung av den typ som du angav i steg 4.  Om du valde *Anpassat ursprung* som **Typ av ursprung** skriver du domänen för ditt anpassade ursprung.
6. I textrutan **Sökväg till ursprung** anger du sökvägen till de resurser som du vill cachelagra eller lämnar fältet tomt om du vill tillåta cachelagring av alla resurser i domänen som du angav i steg 5.
7. I **Ursprungsvärdadress** anger du värdhuvudet som du vill att CDN ska skicka med varje begäran, eller så lämnar du standardvärdet.
   
   > [!WARNING]
   > Vissa typer av ursprung, till exempel Azure Storage och Web Apps, kräver att värdhuvudet matchar ursprungets domän. Lämna standardvärdet såvida du inte har ett ursprung som kräver ett värdhuvud som skiljer sig från dess domän.
   > 
   > 
8. För **Protokoll** och **Ursprungsport** anger du protokollen och portarna som används för att komma åt resurser i ursprunget.  Du måste välja minst ett protokoll (HTTP eller HTTPS).
   
   > [!NOTE]
   > **Ursprungsporten** påverkar endast vilken port som slutpunkten använder för att hämta information från ursprunget.  Själva slutpunkten är bara tillgänglig för slutklienter via HTTP- och HTTPS-standardportarna (80 och 443), oavsett **ursprungsporten**.  
   > 
   > Slutpunkter av typen **Azure CDN från Akamai** tillåter inte det fullständiga TCP-portintervallet för ursprung.  En lista över ursprungsportar som inte tillåts finns i [Azure CDN från Akamai-tillåtna ursprungsportar](https://msdn.microsoft.com/library/mt757337.aspx).  
   > 
   > Följande begränsningar gäller för åtkomst till CDN-innehåll via HTTPS:
   > 
   > * Du måste använda SSL-certifikatet som tillhandahålls av CDN. Certifikat från tredje part stöds inte.
   > * Du måste använda den CDN-definierade domänen (`<endpointname>.azureedge.net`) för att komma åt HTTPS-innehåll. HTTPS-stöd är inte tillgängligt för anpassade domännamn (CNAME-poster) eftersom CDN inte stöder anpassade certifikat för närvarande.
   > 
   > 
9. Klicka på knappen **Lägg till** för att skapa en ny slutpunkt.
10. När slutpunkten har skapats visas den i en lista över slutpunkter för profilen. I listvyn visas bara URL:en som ska användas för att komma åt cachelagrat innehåll, samt ursprungsdomänen.
    
    ![CDN-slutpunkt][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > Slutpunkten är inte direkt tillgänglig för användning eftersom det tar tid för registreringen att spridas i CDN.  För profiler av typen <b>Azure CDN från Akamai</b> slutförs spridningen vanligtvis inom en minut.  För profiler av typen <b>Azure CDN från Verizon</b> slutförs spridningen vanligtvis inom 90 minuter, men i vissa fall kan det ta längre tid.
    > 
    > HTTP 404-svarskoder returneras om användaren försöker använda CDN-domännamnet innan konfigurationen av slutpunkten har spritts till POP.  Om det har gått flera timmar sedan du skapade slutpunkten och du fortfarande får 404-svar läser du [Felsöka CDN-slutpunkter som returnerar 404-status](cdn-troubleshoot-endpoint.md).
    > 
    > 

## <a name="see-also"></a>Se även
* [Kontrollera cachelagringsbeteendet för begäranden med frågesträngar](cdn-query-string.md)
* [Mappa CDN-innehåll till en anpassad domän](cdn-map-content-to-custom-domain.md)
* [Läsa in tillgångar för en Azure CDN-slutpunkt i förväg](cdn-preload-endpoint.md)
* [Rensa en Azure CDN-slutpunkt](cdn-purge-endpoint.md)
* [Felsöka CDN-slutpunkter som returnerar 404-status](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png



<!--HONumber=Jan17_HO4-->


