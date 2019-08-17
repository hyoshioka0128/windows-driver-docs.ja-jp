---
title: HID コレクションの概要
description: HID コレクションは、HID コントロールとそれぞれの HID 使用法を意味的にグループ化したものです。
ms.assetid: 2d3efb38-4eba-43db-8cff-9fac30209952
keywords:
- ヒューマンインターフェイスデバイス WDK、コレクション
- HID WDK、コレクション
- 対話型の入力デバイス WDK、コレクション
- 入力デバイス WDK、コレクション
- コレクション WDK HID
- コレクション WDK HID、HID コレクションについて
- WDK HID のサブコレクション
- ヒューマンインターフェイスデバイス WDK、コントロール
- HID WDK、コントロール
- 対話型の入力デバイス WDK、コントロール
- 入力デバイス WDK、コントロール
- WDK HID を制御します
- HID コレクション (WDK)
- HID コレクション WDK、HID コレクションについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4529cf8b912cf10db10aaa8e41a6a35b2ac9fa04
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565624"
---
# <a name="hid-collections-overview"></a>HID コレクションの概要


*Hid コレクション*は、hid コントロールとそれぞれの[hid 使用法](hid-usages.md)を意味的にグループ化したものです。

コントロールは、論理的に関連している場合や、互いに機能的に依存している場合に、グループ化する必要があります。 たとえば、キーボードの SHIFT キーと letter キーは、個別のコレクションに属さないようにする必要があります。 コレクションには、入れ子になったサブ*コレクション*([リンクコレクション](link-collections.md)とも呼ばれます) を含めることができます。 レポート記述子では、[最上位レベルのコレクション](top-level-collections.md)が1つ以上定義され、各コレクションに関連付けられたレポートアイテムによって1つ以上の HID レポートが定義されます。




Windows は、次のものを含むように、HID コレクションの概念を拡張します。

[最上位レベルのコレクション](top-level-collections.md)

[システムで使用するために Windows によって開かれた最上位レベルのコレクション](top-level-collections-opened-by-windows-for-system-use.md)

[データの Preparsed](preparsed-data.md)

[コレクションのリンク](link-collections.md)

[コレクション機能](collection-capability.md)

[ボタン機能配列](button-capability-arrays.md)

[値機能配列](value-capability-arrays.md)

[データインデックス](data-indices.md)

 

 




