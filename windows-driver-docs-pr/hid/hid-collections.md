---
title: HID コレクション
description: HID コレクションは、HID コントロールと、それぞれの HID の使用の意味のあるグループです。
ms.assetid: 2d3efb38-4eba-43db-8cff-9fac30209952
keywords:
- ヒューマン インターフェイス デバイス WDK、コレクション
- HID WDK、コレクション
- 対話型の入力デバイス WDK、コレクション
- デバイス コレクション、WDK を入力します。
- WDK の HID コレクション
- コレクションは WDK を非表示に、HID コレクションについて
- WDK の HID サブコレクション
- ヒューマン インターフェイス デバイス WDK、コントロール
- HID WDK、コントロール
- 対話型の入力デバイス WDK、コントロール
- 入力デバイス WDK、コントロール
- WDK を非表示コントロール
- HID コレクション WDK
- HID コレクション WDK、HID コレクションについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ce277d5ec85cadb9ebfe59c1ef40e01c4daf0af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582527"
---
# <a name="hid-collections"></a>HID コレクション


A *HID コレクション*HID コントロールと、それぞれの意味のあるグループは、 [HID の使用](hid-usages.md)します。

コントロールはの論理的な関係または互いに機能的に依存する場合、まとめてグループ化する必要があります。 たとえば、SHIFT キーおよびキーボードの文字キーがコレクションを分離する属していません。 コレクションを入れ子に*サブコレクション*とも呼ば[リンク コレクション](link-collections.md)します。 1 つまたは複数のレポート記述子の定義[最上位のコレクション](top-level-collections.md)、し、各コレクションに関連付けられているレポート アイテムは、1 つまたは複数の HID レポートを定義します。




Windows は、以下を含む HID コレクションの概念を拡張します。

[最上位のコレクション](top-level-collections.md)

[システムの Windows によって開かれた最上位のコレクションを使用して、](top-level-collections-opened-by-windows-for-system-use.md)

[Preparsed データ](preparsed-data.md)

[リンクのコレクション](link-collections.md)

[コレクションの機能](collection-capability.md)

[ボタンの機能の配列](button-capability-arrays.md)

[機能の値の配列](value-capability-arrays.md)

[データのインデックス](data-indices.md)

 

 




