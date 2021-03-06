---
title: "Komma igång med VoD med hjälp av Azure Portal | Microsoft Docs"
description: "De här självstudierna visar dig stegen för att implementera ett grundläggande leveransprogram för Video-on-Demand-innehåll (VoD) med Azure Media Services-appen (AMS) med hjälp av Azure Portal."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: juliako
ms.translationtype: Human Translation
ms.sourcegitcommit: 555e0b6340d09517bfd87efe209f0304f3266788
ms.openlocfilehash: 76fd245f91e1bfab3df68120859c69e459283e5b
ms.contentlocale: sv-se
ms.lasthandoff: 01/27/2017

---
# Komma igång med att leverera innehåll på begäran med hjälp av Azure Portal
<a id="get-started-with-delivering-content-on-demand-using-the-azure-portal" class="xliff"></a>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

De här självstudierna visar dig stegen för att implementera ett grundläggande leveransprogram för Video-on-Demand-innehåll (VoD) med Azure Media Services-appen (AMS) med hjälp av Azure Portal.

## Krav
<a id="prerequisites" class="xliff"></a>
Följande krävs för att kunna genomföra vägledningen:

* Ett Azure-konto. Mer information om den [kostnadsfria utvärderingsversionen av Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Ett Media Services-konto. Information om hur du skapar ett Media Services-konto finns i [Så här skapar du ett Media Services-konto](media-services-portal-create-account.md).

Vägledningen innehåller följande uppgifter:

1. Starta slutpunkt för direktuppspelning.
2. Överföra en videofil.
3. Koda källfilen till en uppsättning MP4-filer med anpassningsbar bithastighet.
4. Publicera tillgången och få URL:er för strömning och progressiv överföring.  
5. Spela upp ditt innehåll.

## Starta slutpunkter för direktuppspelning
<a id="start-streaming-endpoints" class="xliff"></a> 

När du arbetar med Azure Media Services är ett av de vanligaste scenarierna att leverera video via direktuppspelning med anpassningsbar bithastighet. Media Services tillhandahåller en dynamisk paketering som gör att du kan leverera ditt MP4-kodade innehåll med anpassningsbar bithastighet i direktuppspelningsformat som stöds av Media Services (MPEG DASH, HLS, Smooth Streaming) direkt när du så önskar, utan att du behöver lagra på förhand paketerade versioner av vart och ett av dessa direktuppspelningsformat.

>[!NOTE]
>När ditt AMS-konto skapas läggs en **standard**-slutpunkt för direktuppspelning till på ditt konto med tillståndet **Stoppad**. Om du vill starta direktuppspelning av innehåll och dra nytta av dynamisk paketering och dynamisk kryptering måste slutpunkten för direktuppspelning som du vill spela upp innehåll från ha tillståndet **Körs**. 

Starta slutpunkten för direktuppspelning genom att göra följande:

1. Logga in på [Azure-portalen](https://portal.azure.com/).
2. I fönstret Inställningar klickar du på Slutpunkter för direktuppspelning. 
3. Klicka på den slutpunkt för direktuppspelning som är standard. 

    Fönstret INFORMATION OM DEN SLUTPUNKT FÖR DIREKTUPPSPELNING SOM ÄR STANDARD visas.

4. Klicka på ikonen Start.
5. Klicka på knappen Spara för att spara ändringarna.

## Överföra filer
<a id="upload-files" class="xliff"></a>
För att strömma videor med Azure Media Services behöver du överföra källvideorna, koda dem till flera olika bithastigheter och publicera resultatet. I det här avsnittet beskrivs det första steget. 

1. I fönstret **Inställning** klickar du på **Tillgångar**.
   
    ![Överföra filer](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. Klicka på knappen **Överför**.
   
    Fönstret **Överför en videotillgång** visas.
   
   > [!NOTE]
   > Det finns inga filstorleksbegränsningar.
   > 
   > 
3. Bläddra till den önskade videon på datorn, markera den och tryck på OK.  
   
    Överföringen startar och du kan följa förloppet under filnamnet.  

När överföringen är klar visas den nya tillgången i listan **Tillgångar**. 

## Koda tillgångar
<a id="encode-assets" class="xliff"></a>
När du arbetar med Azure Media Services är ett av de vanligaste scenarierna att leverera strömning med anpassad bithastighet till dina klienter. Media Services har stöd för följande strömningstekniker med anpassningsbar bithastighet: HTTP-liveuppspelning (HLS), jämn direktuppspelning, MPEG DASH. För att förbereda dina videor för strömning med anpassad bithastighet måste du koda källvideon till filer i multibithastighet. Du bör använda kodaren **Media Encoder Standard** för att koda dina videor.  

Media Services tillhandahåller också en dynamisk paketering som gör att du kan leverera dina MP4-filer med flera bithastigheter i följande strömningsformat: MPEG DASH, HLS eller jämn direktuppspelning utan att du behöver packa om till dessa strömningsformat. Med dynamisk paketering behöver du bara lagra och betala för filerna i ett enda lagringsformat, och Media Services skapar och ger lämplig respons baserat på begäranden från en klient.

Om du vill dra nytta av dynamisk paketering måste du koda din källfil till en uppsättning MP4-filer med flera bithastigheter (kodningsstegen visas längre fram i det här avsnittet).

### Använda portalen för att koda
<a id="to-use-the-portal-to-encode" class="xliff"></a>
I det här avsnittet beskrivs de steg som du kan vidta för att koda ditt innehåll med Media Encoder Standard.

1. I fönstret **Inställningar** väljer du **Tillgångar**.  
2. I fönstret **Tillgångar** väljer du den tillgång som du vill koda.
3. Tryck på knappen **Koda**.
4. I fönstret **Koda en tillgång** väljer du processorn ”Media Encoder Standard” och en förinställning. Om du till exempel vet att din indatavideo har en upplösning på 1 920 x 1 080 bildpunkter, kan du använda förinställningen ”H264 multibithastighet 1080p”. Mer information om förinställningar finns i [denna](media-services-mes-presets-overview.md) artikel – det är viktigt att välja den förinställning som är mest lämplig för din videoinmatning. Om du har en video med låg upplösning (640 x 360) bör du inte använda standardförinställningen ”H264 multibithastighet 1080p”.
   
   Du kan redigera namnet på utdatatillgången och namnet på jobbet för enklare hantering.
   
   ![Koda tillgångar](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. Tryck på **Skapa**.

### Övervaka förloppet för kodningsjobb
<a id="monitor-encoding-job-progress" class="xliff"></a>
Klicka på **Inställningar** (överst på sidan) för att övervaka förloppet för kodningsjobbet och välj sedan **Jobb**.

![Jobb](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## Publicera innehåll
<a id="publish-content" class="xliff"></a>
För att ge din användare en URL som kan användas för att strömma eller hämta ditt innehåll måste du först ”publicera” din tillgång genom att skapa en lokaliserare. Lokaliserare ger åtkomst till filer som finns i tillgången. Media Services stöder två typer av lokaliserare: 

* Strömningslokaliserare (OnDemandOrigin), som används för anpassad strömning (till exempel för strömning av MPEG DASH, HLS och Smooth Streaming). Om du vill skapa en strömningslokaliserare måste din tillgång innehålla en .ism-fil. 
* Progressiva SAS-lokaliserare, som används för leverans av video via progressiv hämtning.

En strömnings-URL har följande format och du kan använda det för att spela upp Smooth Streaming-tillgångar.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

Lägg till (format = m3u8 aapl) till URL:en för att skapa en HLS-strömnings-URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

Lägg till (format=mpd-time-csf) till URL:en för att skapa en MPEG DASH-strömnings-URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


En SAS-URL har följande format.

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> Om du har använt portalen för att skapa lokaliserare före mars 2015, skapades lokaliserare med ett utgångsdatum två år senare.  
> 
> 

Du uppdaterar ett utgångsdatum för en lokaliserare med [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator)- eller [.NET](http://go.microsoft.com/fwlink/?LinkID=533259)-API:er. URL:en ändras när du uppdaterar en SAS-lokaliserare.

### Använda portalen för att publicera en tillgång
<a id="to-use-the-portal-to-publish-an-asset" class="xliff"></a>
Gör följande för att använda portalen för att publicera en tillgång:

1. Välj **Inställningar** > **Tillgångar**.
2. Välj den tillgång som du vill publicera.
3. Klicka sedan på knappen **Publicera**.
4. Välj typ av lokaliserare.
5. Tryck på **Lägg till**.
   
    ![Publicera](./media/media-services-portal-vod-get-started/media-services-publish1.png)

URL:en läggs till i listan över **publicerade URL:er**.

## Spela upp innehåll från portalen
<a id="play-content-from-the-portal" class="xliff"></a>
Azure Portal har en innehållsspelare som du kan använda för att testa videon.

Klicka på önskad video och klicka sedan på knappen **Spela upp**.

![Publicera](./media/media-services-portal-vod-get-started/media-services-play.png)

Vissa förutsättningar gäller:

* Kontrollera att videon har publicerats.
* Denna**Media Player** spelar upp från den strömningsslutpunkt som är standard. Klicka för att kopiera URL:en och använd en annan spelare om du vill spela upp från en strömningsslutpunkt som inte är standard. Till exempel [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

## Nästa steg
<a id="next-steps" class="xliff"></a>
Granska sökvägarna för Media Services-utbildning.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## Ge feedback
<a id="provide-feedback" class="xliff"></a>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


