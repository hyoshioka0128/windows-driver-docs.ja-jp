---
title: フィルム スキャナーの省略可能な WIA アイテム プロパティ
description: フィルム スキャナーの省略可能な WIA アイテム プロパティ
ms.assetid: 6c17deed-7840-4ec0-bc19-d695b3e80c38
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d5a87679d936be9e5916991e8df110b57553efe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550763"
---
# <a name="optional-wia-item-properties-for-film-scanners"></a>フィルム スキャナーの省略可能な WIA アイテム プロパティ





WIA フィルム スキャナーの項目は、WIA の次のプロパティを必要に応じてサポートできます。

[**WIA\_IPA\_FILENAME\_拡張機能**](https://msdn.microsoft.com/library/windows/hardware/ff551549)

[**WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff551641)

[**WIA\_IP\_自動\_DESKEW**](https://msdn.microsoft.com/library/windows/hardware/ff552564)

[**WIA\_IP\_DESKEW\_X**](https://msdn.microsoft.com/library/windows/hardware/ff552581)

[**WIA\_IP\_DESKEW\_Y**](https://msdn.microsoft.com/library/windows/hardware/ff552587)

[**WIA\_IP\_LAMP**](https://msdn.microsoft.com/library/windows/hardware/ff552603)

[**WIA\_IP\_LAMP\_自動\_OFF**](https://msdn.microsoft.com/library/windows/hardware/ff552605)

[**WIA\_IP\_プレビュー\_型**](https://msdn.microsoft.com/library/windows/hardware/ff552646)

[**WIA\_IP\_回転**](https://msdn.microsoft.com/library/windows/hardware/ff552648)

[**WIA\_IP\_セグメント化**](https://msdn.microsoft.com/library/windows/hardware/ff552649)

[**WIA\_IP\_表示\_プレビュー\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff552652)

[**WIA\_IP\_サポート\_子\_項目\_の作成**](https://msdn.microsoft.com/library/windows/hardware/ff552653)

[**WIA\_IP\_しきい値**](https://msdn.microsoft.com/library/windows/hardware/ff552655)

[**WIA\_IP\_ウォーム\_を\_時間**](https://msdn.microsoft.com/library/windows/hardware/ff552660)

[**WIA\_IP\_XSCALING**](https://msdn.microsoft.com/library/windows/hardware/ff552667)

[**WIA\_IP\_YSCALING**](https://msdn.microsoft.com/library/windows/hardware/ff552676)

**注**   、 [ **WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff551641)プロパティは必要な場合、WiaImgFmt\_生の形式がサポートされています。 [ **WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)プロパティは、WiaImgFmt をサポートする必要があります\_BMP 形式。 [ **WIA\_IP\_しきい値**](https://msdn.microsoft.com/library/windows/hardware/ff552655)プロパティが必要なときに、 [ **WIA\_IPA\_深さ** ](https://msdn.microsoft.com/library/windows/hardware/ff551546) 1 ビット/ピクセルに設定されて場合や、 [ **WIA\_IPA\_DATATYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff551543) WIA に設定されて\_データ\_しきい値。

 

 

 




