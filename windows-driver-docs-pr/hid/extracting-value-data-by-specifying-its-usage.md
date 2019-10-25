---
title: 使用法を指定して値データを抽出する
description: 使用法を指定して値データを抽出する
ms.assetid: 043cdb68-ead8-4ccf-ae00-1165fe2988f4
keywords:
- HID レポート WDK、抽出 (コントロールデータを)
- WDK HID を報告し、コントロールデータを抽出します
- HID コントロールデータの抽出
- データ使用量抽出 WDK HID
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6c6982fb567b1ee0319a5d5411c94a123c3869a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824820"
---
# <a name="extracting-value-data-by-specifying-its-usage"></a>使用法を指定して値データを抽出する





HID レポートから値データを抽出するために、アプリケーションまたはドライバーは、次のいずれかの HID サポートルーチンを使用できます。

<a href="" id="hidp-getscaledusagevalue"></a>[**HidP\_Get/Edの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)  
符号付きおよびスケーリングされた値を返します。

<a href="" id="hidp-getusagevalue"></a>[**HidP\_Getの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)  
非スケール値を符号なしの形式で返します。または、**通常**の範囲外のスケール値を返します。

<a href="" id="hidp-getusagevaluearray"></a>[**HidP\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)  
使用状況の値の配列を返します。

**Hidp\_GetUsageValueArray**を使用するには、アプリケーションとドライバーが、使用状況の値の配列を保持するのに十分な大きさのゼロ初期化バッファーを割り当てる必要があります。 必要なサイズ (バイト単位) は、使用状況値配列の[**Hidp\_value\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_value_caps)構造体の**ビットサイズ**と**reportcount**メンバーの積で、最も近いバイトに切り上げられます。

 

 




