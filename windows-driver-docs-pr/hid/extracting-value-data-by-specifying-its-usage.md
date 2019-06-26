---
title: その使用法を指定することで値のデータを抽出
description: その使用法を指定することで値のデータを抽出
ms.assetid: 043cdb68-ead8-4ccf-ae00-1165fe2988f4
keywords:
- HID レポート WDK、コントロールのデータの抽出
- コントロールのデータの抽出、WDK を非表示レポート
- HID コントロール データの抽出
- WDK の HID データ使用量の抽出
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8ca44de04741406a403ffcde4737995cdf7ded34
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375725"
---
# <a name="extracting-value-data-by-specifying-its-usage"></a>その使用法を指定することで値のデータを抽出





HID レポートから値のデータを抽出するには、アプリケーションまたはドライバーを使用できます、次の HID サポート ルーチンのいずれか。

<a href="" id="hidp-getscaledusagevalue"></a>[**HidP\_GetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getscaledusagevalue)  
署名とスケールの値を返します。

<a href="" id="hidp-getusagevalue"></a>[**HidP\_GetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagevalue)  
符号なしの形式か、調整された値のうちある nonscaled 値を返します、**標準**範囲。

<a href="" id="hidp-getusagevaluearray"></a>[**HidP\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagevaluearray)  
使用状況の値の配列を返します。

使用する**HidP\_GetUsageValueArray**アプリケーションとドライバーは、使用状況の値の配列を保持するのに十分な大きさがゼロに初期化のバッファーを割り当てる必要があります。 (バイト単位)、必要なサイズの製品、 **BitSize**と**ReportCount**使用率値の配列のメンバー [ **HIDP\_値\_キャップ** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_value_caps)構造体、最も近いバイトに切り上げられます。

 

 




