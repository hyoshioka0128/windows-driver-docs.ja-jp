---
title: その使用法を指定することで設定値のデータ
description: その使用法を指定することで設定値のデータ
ms.assetid: 69dc3bb4-8999-4990-950c-8581328030eb
keywords:
- HID レポート WDK、コントロールのデータの設定
- WDK を非表示に設定するコントロールのデータを報告します。
- WDK の HID データ使用状況の設定
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9276ed90640f62e90606513d468c116f8c25c92c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385797"
---
# <a name="setting-value-data-by-specifying-its-usage"></a>その使用法を指定することで設定値のデータ





アプリケーション、ドライバーは、次の HID サポート ルーチンのいずれかを呼び出して値を適切に初期化の HID レポートに設定できます。

<a href="" id="hidp-setscaledusagevalue"></a>[**HidP\_SetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setscaledusagevalue)  
レポートで、符号付きとスケールの値を設定します。

<a href="" id="hidp-setusagevalue"></a>[**HidP\_SetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusagevalue)  
レポートで値を設定します。

<a href="" id="hidp-setusagevaluearray"></a>[**HidP\_SetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusagevaluearray)  
レポートの使用状況の値の配列を設定します。

<a href="" id="see-also-initializing-hid-reports-"></a>参照してください[HID レポートの初期化](initializing-hid-reports.md)します。  

 

 




