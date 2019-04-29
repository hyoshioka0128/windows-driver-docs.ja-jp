---
title: 抽出し、コントロールのデータをデータのインデックスを設定
description: 抽出し、コントロールのデータをデータのインデックスを設定
ms.assetid: d26d169f-4116-4d81-94c7-63c92d22877d
keywords:
- HID レポート WDK、コントロールのデータの設定
- WDK を非表示に設定するコントロールのデータを報告します。
- HID レポート WDK、コントロールのデータの抽出
- コントロールのデータの抽出、WDK を非表示レポート
- HID コントロール データの抽出
- WDK を非表示にデータをインデックスします。
- インデックス データの WDK を非表示
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 51ea539124a324dc60930da9f8f9480a3d3964ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388970"
---
# <a name="extracting-and-setting-control-data-by-data-indices"></a>抽出し、コントロールのデータをデータのインデックスを設定





使用する[データのインデックス](data-indices.md)を抽出して HID レポートでデータの制御を設定、アプリケーションやドライバーを使用、次の HID サポート ルーチン。

[**HidP\_GetData**](https://msdn.microsoft.com/library/windows/hardware/ff539718)

[**HidP\_setdata メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff539783)

これらのルーチンは、アプリケーション、ドライバー「付加価値」サービスを提供するに特に便利です。 たとえば、1 つ HIDClass デバイスでサポートされているすべてのコントロールにカスタムのインターフェイスを提供します。 Microsoft DirectInput は一例です。

これらのルーチンを呼び出すことによってアプリケーションやドライバー最も効率的に取得できレポート内のすべての値を設定できます。 によってすべての値のデータの取得など、 [HID の使用](hid-usages.md)、呼び出す[ **HidP\_GetUsageValue** ](https://msdn.microsoft.com/library/windows/hardware/ff539748)ごとの使用状況の。 ただし、すべての値のデータをデータ インデックスを取得するには、のみが呼び出す**HidP\_GetData**とします。

アプリケーションやドライバーでは、コレクションの指定されたデータのインデックスを使用して[ボタン機能配列](button-capability-arrays.md)と[機能の配列の値](value-capability-arrays.md)HID の使用を識別するためにします。

 

 




