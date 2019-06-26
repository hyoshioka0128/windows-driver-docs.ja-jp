---
title: フィルム スキャナーの必須 WIA 項目のプロパティ
description: フィルム スキャナーの必須 WIA 項目のプロパティ
ms.assetid: f87e1bfc-6d85-4aba-a2ad-e491f997a3ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ff6e572d4fa342d55249e4ca73cc6cbf7da9f7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374266"
---
# <a name="required-wia-item-properties-for-film-scanners"></a>フィルム スキャナーの必須 WIA 項目のプロパティ





WIA フィルム スキャナーの項目が次の WIA プロパティをサポートするために必要です。

[**WIA\_IPA\_アクセス\_権限**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-access-rights)

[**WIA\_IPA\_ビット\_1 秒あたり\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-bits-per-channel)

[**WIA\_IPA\_圧縮**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-compression)

[**WIA\_IPA\_チャネル\_1 秒あたり\_ピクセル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-channels-per-pixel)

[**WIA\_IPA\_データ型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)

[**WIA\_IPA\_深さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)

[**WIA\_IP\_フィルム\_スキャン\_モード**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-film-scan-mode)

[**WIA\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)

[**WIA\_IPA\_完全\_項目\_名**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-full-item-name)

[**WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)

[**WIA\_IPA\_項目\_名**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-name)

[**WIA\_IPA\_項目\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)

[**WIA\_IPA\_優先\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-preferred-format)

[**WIA\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)

[**WIA\_IP\_明るさ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-brightness)

[**WIA\_IP\_コントラスト**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-contrast)

[**WIA\_IP\_CUR\_インテント**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-cur-intent)

[**WIA\_IP\_最大\_水平\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-max-horizontal-size)

[**WIA\_IP\_最大\_垂直\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-max-vertical-size)

[**WIA\_IP\_MIN\_水平\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-min-horizontal-size)

[**WIA\_IP\_MIN\_垂直\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-min-vertical-size)

[**WIA\_IP\_光\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-optical-xres)

[**WIA\_IP\_光\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-optical-yres)

[**WIA\_IP\_PHOTOMETRIC\_INTERP**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-photometric-interp)

[**WIA\_IP\_プレビュー**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-preview)

[**WIA\_IP\_XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)

[**WIA\_IP\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)

[**WIA\_IP\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xres)

[**WIA\_IP\_YEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)

[**WIA\_IP\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)

[**WIA\_IP\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yres)

**注**   、 [ **WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-raw-bits-per-channel)プロパティは必要な場合、WiaImgFmt\_生の形式がサポートされています。 [ **WIA\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)プロパティは、WiaImgFmt をサポートする必要があります\_BMP 形式。 [ **WIA\_IP\_しきい値**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-threshold)プロパティが必要なときに、 [ **WIA\_IPA\_深さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)プロパティが 1 ビット/ピクセル (BPP) 場合や、 [ **WIA\_IPA\_データ型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype) WIA に設定されて\_データ\_しきい値。

 

 

 




