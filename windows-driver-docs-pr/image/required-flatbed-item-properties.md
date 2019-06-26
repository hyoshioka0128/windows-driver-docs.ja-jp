---
title: 必須フラットベッド項目のプロパティ
description: 必須フラットベッド項目のプロパティ
ms.assetid: 5af295de-b5ad-47c7-b1db-9d5685ed8d19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbebc9a8ff381d9aab0efdeed14bbccd845994a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374282"
---
# <a name="required-flatbed-item-properties"></a>必須フラットベッド項目のプロパティ





WIA フラット ベッド スキャナーの項目が次の WIA プロパティをサポートするために必要です。

[**WIA\_IPA\_アクセス\_権限**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-access-rights)

[**WIA\_IPA\_ビット\_1 秒あたり\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-bits-per-channel)

[**WIA\_IPA\_バッファー\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-buffer-size)

[**WIA\_IPA\_チャネル\_1 秒あたり\_ピクセル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-channels-per-pixel)

[**WIA\_IPA\_色\_プロファイル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-color-profile)

[**WIA\_IPA\_圧縮**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-compression)

[**WIA\_IPA\_データ型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)

[**WIA\_IPA\_深さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)

[**WIA\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)

[**WIA\_IPA\_完全\_項目\_名**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-full-item-name)

[**WIA\_IPA\_ICM\_PROFILE\_NAME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-icm-profile-name)

[**WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)

[**WIA\_IPA\_項目\_名**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-name)

[**WIA\_IPA\_項目\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)

[**WIA\_IP\_最大\_水平\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-max-horizontal-size)

[**WIA\_IP\_最大\_垂直\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-max-vertical-size)

[**WIA\_IP\_MIN\_水平\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-min-horizontal-size)

[**WIA\_IP\_MIN\_垂直\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-min-vertical-size)

[**WIA\_IPA\_数\_の\_行**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-number-of-lines)

[**WIA\_IPA\_ピクセル\_1 秒あたり\_行**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-pixels-per-line)

[**WIA\_IPA\_平面**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-planar)

[**WIA\_IPA\_優先\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-preferred-format)

[**WIA\_IPA\_PROP\_STREAM\_COMPAT\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-prop-stream-compat-id)

[**WIA\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)

[**WIA\_IP\_明るさ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-brightness)

[**WIA\_IP\_コントラスト**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-contrast)

[**WIA\_IP\_CUR\_インテント**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-cur-intent)

[**WIA\_IP\_光\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-optical-xres)

[**WIA\_IP\_光\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-optical-yres)

[**WIA\_IP\_プレビュー**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-preview)

[**WIA\_IP\_XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)

[**WIA\_IP\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)

[**WIA\_IP\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xres)

[**WIA\_IP\_YEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)

[**WIA\_IP\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)

[**WIA\_IP\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yres)

**注**   、 [ **WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-raw-bits-per-channel)プロパティは必要な場合、WiaImgFmt\_生の形式がサポートされています。 [ **WIA\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)プロパティは、WiaImgFmt をサポートする必要があります\_BMP 形式。 [ **WIA\_IP\_しきい値**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-threshold)プロパティが必要なときに、 [ **WIA\_IPA\_深さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)プロパティが 1 のビット/ピクセル (BPP) 場合や、 [ **WIA\_IPA\_データ型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype) WIA に設定されて\_データ\_しきい値。

 

 

 




