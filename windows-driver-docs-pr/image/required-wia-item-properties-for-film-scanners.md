---
title: フィルム スキャナーの WIA 項目が必要なプロパティ
description: フィルム スキャナーの WIA 項目が必要なプロパティ
ms.assetid: f87e1bfc-6d85-4aba-a2ad-e491f997a3ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cda555c85ee31138b6f6cf4e5365dd486e933251
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530267"
---
# <a name="required-wia-item-properties-for-film-scanners"></a>フィルム スキャナーの WIA 項目が必要なプロパティ





WIA フィルム スキャナーの項目が次の WIA プロパティをサポートするために必要です。

[**WIA\_IPA\_アクセス\_権限**](https://msdn.microsoft.com/library/windows/hardware/ff551518)

[**WIA\_IPA\_ビット\_1 秒あたり\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff551526)

[**WIA\_IPA\_圧縮**](https://msdn.microsoft.com/library/windows/hardware/ff551540)

[**WIA\_IPA\_チャネル\_1 秒あたり\_ピクセル**](https://msdn.microsoft.com/library/windows/hardware/ff551535)

[**WIA\_IPA\_データ型**](https://msdn.microsoft.com/library/windows/hardware/ff551543)

[**WIA\_IPA\_深さ**](https://msdn.microsoft.com/library/windows/hardware/ff551546)

[**WIA\_IP\_フィルム\_スキャン\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff552598)

[**WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)

[**WIA\_IPA\_完全\_項目\_名**](https://msdn.microsoft.com/library/windows/hardware/ff551561)

[**WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581)

[**WIA\_IPA\_項目\_名**](https://msdn.microsoft.com/library/windows/hardware/ff551590)

[**WIA\_IPA\_項目\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551594)

[**WIA\_IPA\_優先\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551623)

[**WIA\_IPA\_TYMED**](https://msdn.microsoft.com/library/windows/hardware/ff551656)

[**WIA\_IP\_明るさ**](https://msdn.microsoft.com/library/windows/hardware/ff552567)

[**WIA\_IP\_コントラスト**](https://msdn.microsoft.com/library/windows/hardware/ff552573)

[**WIA\_IP\_CUR\_インテント**](https://msdn.microsoft.com/library/windows/hardware/ff552579)

[**WIA\_IP\_最大\_水平\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff552607)

[**WIA\_IP\_最大\_垂直\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff552611)

[**WIA\_IP\_MIN\_水平\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff552612)

[**WIA\_IP\_MIN\_垂直\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff552614)

[**WIA\_IP\_光\_XRES**](https://msdn.microsoft.com/library/windows/hardware/ff552620)

[**WIA\_IP\_光\_YRES**](https://msdn.microsoft.com/library/windows/hardware/ff552622)

[**WIA\_IP\_PHOTOMETRIC\_INTERP**](https://msdn.microsoft.com/library/windows/hardware/ff552640)

[**WIA\_IP\_プレビュー**](https://msdn.microsoft.com/library/windows/hardware/ff552643)

[**WIA\_IP\_XEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552661)

[**WIA\_IP\_XPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552663)

[**WIA\_IP\_XRES**](https://msdn.microsoft.com/library/windows/hardware/ff552665)

[**WIA\_IP\_YEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552669)

[**WIA\_IP\_YPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552671)

[**WIA\_IP\_YRES**](https://msdn.microsoft.com/library/windows/hardware/ff552673)

**注**   、 [ **WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff551641)プロパティは必要な場合、WiaImgFmt\_生の形式がサポートされています。 [ **WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)プロパティは、WiaImgFmt をサポートする必要があります\_BMP 形式。 [ **WIA\_IP\_しきい値**](https://msdn.microsoft.com/library/windows/hardware/ff552655)プロパティが必要なときに、 [ **WIA\_IPA\_深さ**](https://msdn.microsoft.com/library/windows/hardware/ff551546)プロパティが 1 ビット/ピクセル (BPP) 場合や、 [ **WIA\_IPA\_データ型**](https://msdn.microsoft.com/library/windows/hardware/ff551543) WIA に設定されて\_データ\_しきい値。

 

 

 




