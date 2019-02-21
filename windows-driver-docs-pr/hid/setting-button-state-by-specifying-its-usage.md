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
ms.openlocfilehash: 9ed759ad3b03575026bff05c1889c680511bf666
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538854"
---
# <a name="setting-button-state-by-specifying-its-usage"></a>その使用法を指定することによって設定ボタンの状態





アプリケーション、ドライバーは、次の HID サポート ルーチンのいずれかを呼び出すボタンの状態を正しく初期化の HID レポートに設定できます。

<a href="" id="hidp-setbuttons--or-hidp-setusages-"></a>[**HidP\_SetButtons** ](https://msdn.microsoft.com/library/windows/hardware/ff539779) (または[ **HidP\_SetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539792))  
オン (1) 指定されたボタンのセットを設定します。

<a href="" id="hidp-unsetbuttons--or-hidp-unsetusages-"></a>[**HidP\_UnsetButtons** ](https://msdn.microsoft.com/library/windows/hardware/ff539812) (または[ **HidP\_UnsetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539819))  
指定された一連のボタンは OFF に設定 (ゼロ)。

<a href="" id="see-also-initializing-hid-reports-"></a>参照してください[HID レポートの初期化](initializing-hid-reports.md)します。  

 

 




