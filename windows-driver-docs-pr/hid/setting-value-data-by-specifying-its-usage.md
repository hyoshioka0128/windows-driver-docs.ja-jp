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
ms.openlocfilehash: 1790f94523c243f2d8cb1b1553fc0a4ef5dde251
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358894"
---
# <a name="setting-value-data-by-specifying-its-usage"></a>その使用法を指定することで設定値のデータ





アプリケーション、ドライバーは、次の HID サポート ルーチンのいずれかを呼び出して値を適切に初期化の HID レポートに設定できます。

<a href="" id="hidp-setscaledusagevalue"></a>[**HidP\_SetScaledUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539787)  
レポートで、符号付きとスケールの値を設定します。

<a href="" id="hidp-setusagevalue"></a>[**HidP\_SetUsageValue**](https://msdn.microsoft.com/library/windows/hardware/ff539797)  
レポートで値を設定します。

<a href="" id="hidp-setusagevaluearray"></a>[**HidP\_SetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539801)  
レポートの使用状況の値の配列を設定します。

<a href="" id="see-also-initializing-hid-reports-"></a>参照してください[HID レポートの初期化](initializing-hid-reports.md)します。  

 

 




