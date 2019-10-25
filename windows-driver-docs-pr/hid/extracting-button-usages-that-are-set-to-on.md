---
title: ON に設定されているボタンの使用法を抽出しています
description: ON に設定されているボタンの使用法を抽出しています
ms.assetid: 700cdb18-f570-4189-a33c-f57af56a52fd
keywords:
- HID レポート WDK、抽出 (コントロールデータを)
- WDK HID を報告し、コントロールデータを抽出します
- HID コントロールデータの抽出
- ボタンの使用法 WDK HID
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 206c3a9d97ff8ece84d60b90c939a1fbea66f1fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824821"
---
# <a name="extracting-button-usages-that-are-set-to-on"></a>ON に設定されているボタンの使用法を抽出しています





ON (1) に設定されているボタンの[hid 使用](hid-usages.md)を抽出するために、アプリケーションとドライバーは次のいずれかの hid サポートルーチンを呼び出します。

<a href="" id="hidp-getbuttons--or-hidp-getusages-"></a>[**Hidp\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) (または[**Hidp\_getbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages))  
ON に設定されている、指定された使用状況ページのすべてのボタンの使用状況 ID を返します。

<a href="" id="hidp-getbuttonsex--or-hidp-getusagesex-"></a>[**Hidp\_GetButtonsEx**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) (または[**Hidp\_getて sex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex))  
[使用状況] ページと、[オン] に設定されているすべてのボタンの使用状況 ID を返します。

これらのルーチンは、現在 ON に設定されているすべてのボタンのすべての使用状況情報の配列を返します。 暗黙的に、これらのルーチンによって使用されていないボタンは、OFF (ゼロ) に設定されます。

これらのルーチンを呼び出すには、まず、アプリケーションとドライバーが、ボタンの使用の配列を返すために使用されるバッファーを割り当て、ゼロ初期化する必要があります。 アプリケーションまたはドライバーが[**Hidp\_Max使用 Listlength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxusagelistlength)を呼び出して、レポート内の指定された使用状況ページでのボタンの使用回数を決定します。 アプリケーションまたはドライバーが使用状況ページをゼロに指定した場合、ルーチンはレポート内のすべてのボタンの使用状況の数を返します。

必要なバッファーサイズ (バイト単位) は次のとおりです。

-   ( [**Hidp\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros))Hidp によって返される値 **\_Max使用 Listlength** times SIZEOF (USAGE)

-   ( [**Hidp\_GetButtonsEx**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros))Hidp によって返される値は、 **max\_Listlength**時間 SIZEOF (USAGE\_と\_ ページ) です。

アプリケーションまたはドライバーが、現在 ON に設定されているボタンに関する情報を取得するためにこれらのルーチンを使用した後、次のいずれかの HIDClass を呼び出すことにより、ボタンの現在の状態と以前の状態の違いを判断できます。 [サポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 これらのルーチンは、使用状況情報の2つの配列の差を返します。

[**HidP\_の使い方 List相違点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_usagelistdifference)

[**HidP\_の使い方 Andpagelist減法**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff539824(v=vs.85))

 

 




