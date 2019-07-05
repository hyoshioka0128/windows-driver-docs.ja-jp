---
title: HID の使用状況
description: HID の使用法は、HID コントロールとコントロールが実際に測定の使用目的を特定します。
ms.assetid: 84fed314-3554-4291-b51c-734d874a4bab
keywords:
- ヒューマン インターフェイス デバイス WDK、使用状況
- HID WDK、使用状況
- 対話型の入力デバイス WDK、使用状況
- 入力デバイス WDK、使用状況
- ヒューマン インターフェイス デバイス WDK、コントロール
- HID WDK、コントロール
- 対話型の入力デバイス WDK、コントロール
- 入力デバイス WDK、コントロール
- WDK を非表示コントロール
- WDK HID 使用法をページします。
- Id WDK HID の使用状況
- WDK の HID 拡張の使用法
- 使用状況の範囲は WDK を非表示
- WDK の HID エイリアスの使用法
- WDK の HID の使用状況
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43f88332071171ce90e145e9abfacb36d4c26e61
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388805"
---
#  <a name="hid-usages"></a>HID の使用状況


*HID の使用法*HID コントロールとコントロールが実際に測定の使用目的を識別します。




次の概念と用語は、WDK の HID ドキュメント全体で使用されます。

[使用状況 ページ](#usage-page)

[使用状況 ID](#usage-id)

[拡張の使用状況](#extended-usage)

[使用状況の範囲](#usage-range)

[エイリアスの使用法](#aliased-usages)

Windows コンポーネントにアクセスする使用法の具体的な例については、次を参照してください。[最上位のコレクションは、Windows システムの使用によって開かれた](top-level-collections-opened-by-windows-for-system-use.md)します。

HIDClass デバイスをサポートする使用状況を確認する方法の詳細についてを参照してください。

[コレクションの機能](collection-capability.md)

[ボタンの機能の配列](button-capability-arrays.md)

[機能の値の配列](value-capability-arrays.md)

[HID レポートの解釈](interpreting-hid-reports.md)

業界標準の HID 使用法の詳細については、ユニバーサル シリアル バス (USB) 仕様を参照してください。 *HID Usage Tables*にある、 [USB Implementers Forum](https://go.microsoft.com/fwlink/?linkid=830142) web サイト。 (このリソースできない場合がありますのいくつかの言語および国。)

### <a name="usage-page"></a>使用状況 ページ

HID の使用法が編成されます *[使い方] ページ*の関連するコントロール。 使用状況 ページで特定のコントロールの使用量が定義されている、[使用状況 ID](#usage-id)名、および説明します。 [使い方] ページの例には、汎用的なデスクトップのコントロール、ゲームのコントロール、Led、ボタン、およびなどが含まれます。 一般的なデスクトップのコントロールの使用状況 ページに表示されるコントロールの例についてには、ポインター、マウスとキーボード デバイス、ジョイスティック、およびなどが含まれます。 使用状況 ページの値は、16 ビット符号なし値です。

### <a name="usage-id"></a>使用状況 ID

有効な使用方法の識別子では、使用状況 ページのコンテキストでまたは*使用状況 ID*、使用状況 ページでの使用状況を示します。 0 の使用状況の ID は予約されています。 使用法の ID 値は、符号なし 16 ビット値です。

### <a name="extended-usage"></a>拡張の使用状況

*拡張使用法*16 ビットを指定する 32 ビット値は、 [使用状況ページ](#usage-page) の最上位の 2 つのバイト数と 16 ビット値[使用状況 ID](#usage-id) (最下位の 2 つのバイト単位)拡張使用法の値。

### <a name="usage-range"></a>使用状況の範囲

A*使用状況の範囲*の包括的な連続する範囲[Id の使用状況](#usage-id)、すべて同じであるの[使用状況 ページ](#usage-page)します。 使用状況の範囲は、使用量の最小値とレポート記述子の使用量の最大アイテムによって指定されます。

### <a name="aliased-usages"></a>エイリアスの使用法

1 つ以上の使用量を指定できます、 [**リンク コレクション**](link-collections.md)または HID コントロール。 このような使用法のグループ、特定のコレクションやコントロールは、別のエイリアスですと呼ばれます*エイリアスの使用法*します。 項目の区切り記号を使用すると、別名の使用法を指定します。 [使用状況の範囲](#usage-range)エイリアスにすることはできません。

最上位のコレクションの機能の配列でエイリアスの使用法を指定する方法については、次を参照してください。[ボタン機能配列](button-capability-arrays.md)と[値機能配列](value-capability-arrays.md)します。

 

 




