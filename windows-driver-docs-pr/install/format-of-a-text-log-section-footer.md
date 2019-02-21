---
title: テキスト ログのセクションのフッターの形式
description: テキスト ログのセクションのフッターの形式
ms.assetid: 3b804934-a695-4091-a3ef-03f7598cbe63
keywords:
- WDK SetupAPI のフッターをセクションします。
- WDK SetupAPI ログ出力を書式設定します。
- テキスト ログの WDK SetupAPI、セクションのフッター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4268b3ca86fd006cdcf448837d5bacf43b8f7d9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558297"
---
# <a name="format-of-a-text-log-section-footer"></a>テキスト ログのセクションのフッターの形式


A*テキスト ログのセクションのフッター*テキスト ログのセクションを閉じます。 セクション フッターは、2 つのエントリで構成されます。 フッター セクションの最初のエントリの形式が含まれています、"&lt; &lt; &lt; "、プレフィックスに続いて、 *time_stamp*フィールドと文字列「セクションの終わり」。

```cpp
<<<  [time_stamp Section end]
```

形式、 *time_stamp*フィールドが記載されているのと同じ[テキスト ログ セクション ヘッダーの形式](format-of-a-text-log-section-header.md)します。

2 番目のエントリの形式が含まれています、"&lt; &lt; &lt; "後に文字列"Exit"プレフィックスと*状態*フィールド。 次の例では、斜体のフォント スタイル内のテキスト セクションの作成者によって指定されたセクション固有のテキストのプレース ホルダーは、太字のフォントのスタイル内のテキストは、SetupAPI によって提供されるログ記録。

```cpp
<<<  [Exit Status(status)]
```

Status フィールドの形式は"0 x*hhhhhhhh*"ここで、 *hhhhhhhh* 8 桁の 16 進数です。

状態フィールドが存在しない場合、最初の行の形式のとおりです。

```cpp
<<<  [Exit]
```

"0x00000000"の終了ステータスを指定しを含むセクション フッターの例を次に、 *time_stamp*フィールド。

```cpp
<<<  [2005/02/13 22:06:28.109: Section end]
<<<  [Exit Status(0x00000000)]
```

 

 





