---
title: フィルム スキャナーの省略可能 WIA 項目のプロパティ
description: フィルム スキャナーの省略可能 WIA 項目のプロパティ
ms.assetid: 6c17deed-7840-4ec0-bc19-d695b3e80c38
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13997f23e3b9301ec3b7a88160a56991f59c4ca5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376546"
---
# <a name="optional-wia-item-properties-for-film-scanners"></a>フィルム スキャナーの省略可能 WIA 項目のプロパティ





WIA フィルム スキャナーの項目は、WIA の次のプロパティを必要に応じてサポートできます。

[**WIA\_IPA\_FILENAME\_拡張機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-filename-extension)

[**WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-raw-bits-per-channel)

[**WIA\_IP\_自動\_DESKEW**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-auto-deskew)

[**WIA\_IP\_DESKEW\_X**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-deskew-x)

[**WIA\_IP\_DESKEW\_Y**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-deskew-y)

[**WIA\_IP\_LAMP**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-lamp)

[**WIA\_IP\_LAMP\_自動\_OFF**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-lamp-auto-off)

[**WIA\_IP\_プレビュー\_型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-preview-type)

[**WIA\_IP\_回転**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-rotation)

[**WIA\_IP\_セグメント化**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-segmentation)

[**WIA\_IP\_表示\_プレビュー\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-show-preview-control)

[**WIA\_IP\_サポート\_子\_項目\_の作成**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-supports-child-item-creation)

[**WIA\_IP\_しきい値**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-threshold)

[**WIA\_IP\_ウォーム\_を\_時間**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-warm-up-time)

[**WIA\_IP\_XSCALING**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xscaling)

[**WIA\_IP\_YSCALING**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yscaling)

**注**   、 [ **WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-raw-bits-per-channel)プロパティは必要な場合、WiaImgFmt\_生の形式がサポートされています。 [ **WIA\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)プロパティは、WiaImgFmt をサポートする必要があります\_BMP 形式。 [ **WIA\_IP\_しきい値**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-threshold)プロパティが必要なときに、 [ **WIA\_IPA\_深さ** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth) 1 ビット/ピクセルに設定されて場合や、 [ **WIA\_IPA\_DATATYPE** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype) WIA に設定されて\_データ\_しきい値。

 

 

 




