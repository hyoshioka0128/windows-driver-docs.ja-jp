---
title: 統合テスト
description: 統合テストを最適なエンド ツー エンド ユーザー エクスペリエンスを実行する重要です。
ms.assetid: 61C1AC15-498B-432B-8D26-0303425114FF
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fbddea454f0fdd56f4f159d6fcb79ebb6df99cd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355769"
---
# <a name="integration-testing"></a>統合テスト


統合テストを最適なエンド ツー エンド ユーザー エクスペリエンスを実行することが重要

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="indicator-testing.md" data-raw-source="[Indicator testing](indicator-testing.md)">インジケーターのテスト</a></p></td>
<td align="left"><p>このトピックでは、インジケーターの一般的な手順の手順と例について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="convertible-testing.md" data-raw-source="[Convertible testing](convertible-testing.md)">変換可能なテスト</a></p></td>
<td align="left"><p>このトピックでは、コンバーチブルのテストについて説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="touchscreen-laptop-system-testing.md" data-raw-source="[Touchscreen laptop system testing](touchscreen-laptop-system-testing.md)">タッチ スクリーン ラップトップ システムのテスト</a></p></td>
<td align="left"><p>このトピックでは、タッチ スクリーンのラップトップ システムのテストについて説明します。</p></td>
</tr>
</tbody>
</table>

 

各システムに実装して、次の方法は、内で一意では、します。

-   ハードウェアのボタンと場所
-   ラップトップ コンピューターとスレート モード (コンバーチブル) の間の切り替えをさまざまな方法

このセクションで説明したシナリオの詳細については、次を参照してください。 [Windows 8.1 の GPIO ボタンとインジケーター実装ガイド](gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md)します。

*表 1 インジケーターの組み合わせの期待どおり動作*インジケーターの組み合わせごとに想定される動作を示しています。

**表 1 のインジケーターの組み合わせが想定された動作**

| Mode   | Dock     | スクリーン キーボードが表示されます。 | 自動ローテーションが有効になっています。 |
|--------|----------|-----------------------------|-----------------------|
| ノート PC | ドッキングされていません。 | X                          | X                    |
| ノート PC | ドッキング   | X                          | X                    |
| スレート  | ドッキングされていません。 | 〇                         | 〇                   |
| スレート  | ドッキング   | 〇                         | X                    |

 

このセクションでは、一連のドッキングとラップトップ/スレート モードのインジケーターに関連するさまざまなシナリオのテストについて説明します。 テストが不合格の場合は、次を参照してください。 [GPIO ログ記録と調査](gpio-logging-and-investigations.md)します。

 

 




