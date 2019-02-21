---
title: ON に設定するボタンの使用法の抽出
description: ON に設定するボタンの使用法の抽出
ms.assetid: 700cdb18-f570-4189-a33c-f57af56a52fd
keywords:
- HID レポート WDK、コントロールのデータの抽出
- コントロールのデータの抽出、WDK を非表示レポート
- HID コントロール データの抽出
- WDK の HID ボタンの使用
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f67b1fec41f5311b45a065f715c5a8b18996b687
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557367"
---
# <a name="extracting-button-usages-that-are-set-to-on"></a>ON に設定するボタンの使用法の抽出





抽出する、 [HID の使用](hid-usages.md)オン (1) に設定されているボタンの HID を次のいずれかのアプリケーションとドライバーの呼び出しがルーチンをサポートします。

<a href="" id="hidp-getbuttons--or-hidp-getusages-"></a>[**HidP\_GetButtons** ](https://msdn.microsoft.com/library/windows/hardware/ff539708) (または[ **HidP\_GetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539742))  
ON に設定されている指定された使用法 ページには、すべてのボタンの使用状況の ID を返します。

<a href="" id="hidp-getbuttonsex--or-hidp-getusagesex-"></a>[**HidP\_GetButtonsEx** ](https://msdn.microsoft.com/library/windows/hardware/ff539712) (または[ **HidP\_GetUsagesEx**](https://msdn.microsoft.com/library/windows/hardware/ff539745))  
使用状況 ページとを ON に設定されているすべてのボタンの使用状況の ID を返します。

これらのルーチンでは、現在は ON に設定されているすべてのボタンのすべての利用状況情報の配列を返します。 暗黙的に、ボタンの使用法は、これらのルーチンでは返されませんが、(ゼロ) をオフに設定されます。

これらのルーチンを呼び出すには、アプリケーションとドライバーする必要があります最初の割り当てとボタンの使用法の配列を返すために使用するバッファーを 0 に初期化します。 アプリケーションまたはドライバーを呼び出す[ **HidP\_MaxUsageListLength** ](https://msdn.microsoft.com/library/windows/hardware/ff539770)レポートで指定された使用法 ページで、ボタンの使用法の数を決定します。 アプリケーションまたはドライバーは、0 の使用に関するページを指定する場合、ルーチンは、レポートですべてのボタンの使用状況の数を返します。

必要なバッファー サイズをバイト単位で、次に示します。

-   (の[ **HidP\_GetButtons**](https://msdn.microsoft.com/library/windows/hardware/ff539708)) によって返される値**HidP\_MaxUsageListLength** sizeof(USAGE) の時間

-   (の[ **HidP\_GetButtonsEx**](https://msdn.microsoft.com/library/windows/hardware/ff539712)) によって返される値**HidP\_MaxUsageListLength**回 sizeof (使用状況\_AND\_ページ)

次のいずれかを呼び出して現在の状態と、ボタンの前の状態間の差を決定できるアプリケーションやドライバーでは、これらのルーチンを使用するボタンが現在 ON に設定情報を取得するが後、 [HIDClass サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff538865)します。 これらのルーチンでは、使用状況に関する情報の 2 つの配列間の差が返されます。

[**HidP\_UsageListDifference**](https://msdn.microsoft.com/library/windows/hardware/ff539826)

[**HidP\_UsageAndPageListDifference**](https://msdn.microsoft.com/library/windows/hardware/ff539824)

 

 




