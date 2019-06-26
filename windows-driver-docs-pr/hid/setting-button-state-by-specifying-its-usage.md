---
title: その使用法を指定することによって設定ボタンの状態
description: その使用法を指定することによって設定ボタンの状態
ms.assetid: 0806f274-2b29-44f5-b487-4c0acb7a3e42
keywords:
- HID レポート WDK、コントロールのデータの設定
- WDK を非表示に設定するコントロールのデータを報告します。
- WDK の HID ボタンの使用
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b0ebf83eec8456e0f79acae0f289f6741d91c765
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385801"
---
# <a name="setting-button-state-by-specifying-its-usage"></a>その使用法を指定することによって設定ボタンの状態





アプリケーション、ドライバーは、次の HID サポート ルーチンのいずれかを呼び出すボタンの状態を正しく初期化の HID レポートに設定できます。

<a href="" id="hidp-setbuttons--or-hidp-setusages-"></a>[**HidP\_SetButtons** ](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) (または[ **HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusages))  
オン (1) 指定されたボタンのセットを設定します。

<a href="" id="hidp-unsetbuttons--or-hidp-unsetusages-"></a>[**HidP\_UnsetButtons** ](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) (または[ **HidP\_UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_unsetusages))  
指定された一連のボタンは OFF に設定 (ゼロ)。

<a href="" id="see-also-initializing-hid-reports-"></a>参照してください[HID レポートの初期化](initializing-hid-reports.md)します。  

 

 




