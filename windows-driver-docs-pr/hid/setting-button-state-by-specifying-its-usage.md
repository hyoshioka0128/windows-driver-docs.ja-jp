---
title: 使用法を指定してボタンの状態を設定する
description: 使用法を指定してボタンの状態を設定する
ms.assetid: 0806f274-2b29-44f5-b487-4c0acb7a3e42
keywords:
- HID レポート WDK、コントロールデータの設定
- WDK HID を報告し、コントロールデータを設定します
- ボタンの使用法 WDK HID
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f289a214e5e09d1e8bf4e8986e1ae29c7b5d844b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841555"
---
# <a name="setting-button-state-by-specifying-its-usage"></a>使用法を指定してボタンの状態を設定する





アプリケーションまたはドライバーは、次のいずれかの HID サポートルーチンを呼び出すことによって、適切に初期化された HID レポートのボタンの状態を設定できます。

<a href="" id="hidp-setbuttons--or-hidp-setusages-"></a>[**Hidp\_SetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) (または[**Hidp\_setbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages))  
指定されたボタンのセットを ON (1) に設定します。

<a href="" id="hidp-unsetbuttons--or-hidp-unsetusages-"></a>[**Hidp\_UnsetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) (または[**Hidp\_unsetbuttons**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages))  
指定されたボタンのセットを OFF (ゼロ) に設定します。

<a href="" id="see-also-initializing-hid-reports-"></a>「 [HID レポートの初期化](initializing-hid-reports.md)」も参照してください。  

 

 




