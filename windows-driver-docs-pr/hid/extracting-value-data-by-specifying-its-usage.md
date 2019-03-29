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
ms.openlocfilehash: b1afadef2e51cf600b5f048a269843e3e2907e44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570347"
---
# <a name="extracting-value-data-by-specifying-its-usage"></a>その使用法を指定することで値のデータを抽出





HID レポートから値のデータを抽出するには、アプリケーションまたはドライバーを使用できます、次の HID サポート ルーチンのいずれか。

<a href="" id="hidp-getscaledusagevalue"></a>[**HidP\_GetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539729)  
署名とスケールの値を返します。

<a href="" id="hidp-getusagevalue"></a>[**HidP\_GetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539748)  
符号なしの形式か、調整された値のうちある nonscaled 値を返します、**標準**範囲。

<a href="" id="hidp-getusagevaluearray"></a>[**HidP\_GetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539750)  
使用状況の値の配列を返します。

使用する**HidP\_GetUsageValueArray**アプリケーションとドライバーは、使用状況の値の配列を保持するのに十分な大きさがゼロに初期化のバッファーを割り当てる必要があります。 (バイト単位)、必要なサイズの製品、 **BitSize**と**ReportCount**使用率値の配列のメンバー [ **HIDP\_値\_キャップ** ](https://msdn.microsoft.com/library/windows/hardware/ff539832)構造体、最も近いバイトに切り上げられます。

 

 




