---
title: テキスト ログ セクション フッターの書式
description: テキスト ログ セクション フッターの書式
ms.assetid: 3b804934-a695-4091-a3ef-03f7598cbe63
keywords:
- WDK SetupAPI のフッターをセクションします。
- WDK SetupAPI ログ出力を書式設定します。
- テキスト ログの WDK SetupAPI、セクションのフッター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4268b3ca86fd006cdcf448837d5bacf43b8f7d9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322268"
---
# <a name="format-of-a-text-log-section-footer"></a>テキスト ログ セクション フッターの書式


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

 

 





