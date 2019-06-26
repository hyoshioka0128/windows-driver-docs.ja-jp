---
title: 未処理形式転送のプロパティ検証
description: 未処理形式転送のプロパティ検証
ms.assetid: ad58f94e-d59e-4d04-be27-cc87f89f3d76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ee353bc505b536adbb95e04ea999b0f060d782e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376508"
---
# <a name="property-validation-for-raw-format-transfers"></a>未処理形式転送のプロパティ検証


ドライバーは、RAW 形式のデータ転送する前に、WIA プロパティの設定を検証する必要があります。 WIA プロパティは、次のように設定する必要があります。

<a href="" id="wia-ips-xpos--wia-ips-ypos"></a>[**WIA\_IP\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)、 [ **WIA\_IP\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)  
これらのプロパティの設定が RAW の他のイメージ形式です。 これらのプロパティは、選択したイメージの左上隅のピクセル単位で、座標を含めることが

<a href="" id="wia-ips-xres--wia-ips-yres"></a>[**WIA\_IP\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xres)、 [ **WIA\_IP\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yres)  
これらのプロパティの設定が RAW の他のイメージ形式です。 これらのプロパティをそれぞれ現在の水平および垂直方向を含む、デバイスの 1 インチあたりのピクセル単位での解決

<a href="" id="wia-ips-xextent--wia-ips-yextent"></a>[**WIA\_IP\_XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)、 [ **WIA\_IP\_YEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)  
これらのプロパティ、アプリケーションによって設定されたによって読み取られ、は、ドライバーによって更新します。 プロパティは、元の値から変更された可能性があります、ため、アプリケーションは、生のストリームを処理するときに、これらのプロパティに格納されている値を読み取る必要があります。

<a href="" id="wia-ipa-depth"></a>[**WIA\_IPA\_深さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)  
このプロパティは、ピクセルあたりのビット数を格納します。 ドライバーが、アプリケーションを設定すると、このプロパティの値を設定[ **WIA\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)に**WiaImgFmt\_RAW**します。 すべてのエントリで、WIA の合計\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル プロパティは、WIA に格納されている数と一致する必要があります\_IPA\_DEPTH プロパティ。 WIA\_IPA\_の深さが、ドライバーは、複数の構成をサポートしている場合、書き込み可能な。 たとえば、32 ビット/ピクセルと構成のピクセルあたり 48 ビットをサポートするドライバーの場合は、アプリケーションが 1 つの設定を選択でき、ドライバーは、WIA を設定する必要があります\_IPA\_RAW\_ビット\_1 秒あたり\_チャネルと関連付けられているプロパティに応じて。

<a href="" id="wia-ipa-raw-bits-per-channel"></a>[**WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-raw-bits-per-channel)  
このプロパティの値への応答中にドライバーによって**WiaImgFmt\_RAW** 、WIA で\_IPA\_プロパティを書式設定し、更新されます WIA\_IPA\_データ型変更されました。 WIA のエントリがすべて\_IPA\_RAW\_ビット\_1 秒あたり\_WIA に格納されているピクセルあたりのビット数でなければなりません。 チャネル\_IPA\_深度。

<a href="" id="wia-ipa-channels-per-pixel"></a>[**WIA\_IPA\_チャネル\_1 秒あたり\_ピクセル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-channels-per-pixel)  
このプロパティが選択されている未加工のピクセルあたりのチャネルの数に、ドライバーで WIA サブタイプ\_IPA\_データ型。

<a href="" id="wia-ipa-datatype"></a>[**WIA\_IPA\_データ型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)  
ときに WIA\_IPA\_に形式が設定されている**WiaImgFmt\_RAW**ドライバーは、このプロパティを既定値を設定します。 ドライバーには、既定値を変更する元のアプリケーションを選択できます許容値の一覧も決定します。 WIA\_IPA\_ドライバーによってデータ型の既定値が選択されているは、デバイスで使用できる任意の値をすることができます。

<a href="" id="wia-ipa-bytes-per-line"></a>[**WIA\_IPA\_バイト\_1 秒あたり\_行**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-bytes-per-line)  
に従って、WIA ミニドライバーで更新する必要があります\_IPA\_形式と WIA\_IPA\_データ型を設定します。

<a href="" id="wia-ipa-item-size"></a>[**WIA\_IPA\_項目\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)  
0 にする必要があります。

 

 




