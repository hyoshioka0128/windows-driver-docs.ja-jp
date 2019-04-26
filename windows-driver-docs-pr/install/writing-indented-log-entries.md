---
title: インデントされたログ エントリの記述
description: インデントされたログ エントリの記述
ms.assetid: 8ce6b433-a004-43f6-9481-9c23c5e7e8da
keywords:
- WDK SetupAPI のインデントを設定したログ エントリ
- WDK SetupAPI ログ出力を書式設定します。
- テキスト ログの WDK SetupAPI、インデントを設定したログ エントリ
- SetupWriteTextLog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b40ef65859e8919d115c1da2922c9807e860908e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339137"
---
# <a name="writing-indented-log-entries"></a>インデントされたログ エントリの記述


」の説明に従って[ログ セクションのテキスト本文の形式](format-of-a-text-log-section-body.md)にセクション本文のログ エントリの形式を[SetupAPI テキスト ログ](setupapi-text-logs.md)次のフィールドで構成されています。

```cpp
entry_prefix time_stamp event_category indentation formatted_message
```

使用することができます、*インデント*フィールドにインデントを設定するログ エントリ、 *formatted_message*ログ エントリを理解し、やすくためにフィールド。 インデント フィールドでインデントの量は、セクションに対して設定されているインデントの深さに依存します。 インデントの深さは、位置、インデント単位は、5 つの固定幅テキスト スペースのインデント ユニットの数です。 たとえば、インデントの深さの 5 つの空白、インデントで結果が 1 のインデント深さが 2 の結果の 10 個の空白、インデント。 最小のインデントの深さは 0 とインデントの最大の深さは 16 です。

既定では、セクションのインデントの深さは 0 です。 インデントの深さが 0 の場合、 *formatted_message*フィールドはインデントされません。 アプリケーションが対応する一連のインデントの深さは、アプリケーションは、その後の書き込み前にゼロにリセットする」セクションのエントリを書き込む必要がありますもインデント深さインデントされたセクション エントリのシーケンスを記述するアプリケーションが増加すると、インデントされません追加のセクションのエントリ。

セクションのインデントの深さを変更するには、SetupAPI ログ関数の呼び出しを次のシステム定義のマニフェスト定数のいずれかと、SetupAPI ログ関数に渡される flags パラメーター間でビットごとの OR を使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マニフェスト定数</th>
<th align="left">インデントの深さを変更します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>TXTLOG_DEPTH_INCR</p></td>
<td align="left"><p>現在のログ エントリの 1 とすべての後続のログ エントリをインデントの深さが向上します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TXTLOG_DEPTH_DECR</p></td>
<td align="left"><p>インデントの深さは、現在のログ エントリの 1 とすべての後続のログ エントリが減少します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TXTLOG_TAB_1</p></td>
<td align="left"><p>インデントの深さが現在のログ エントリに対してのみ 1 増加します。</p></td>
</tr>
</tbody>
</table>

 

次の一連の呼び出しなど[ **SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)セクション ヘッダーの後にインデントを設定したログ エントリのシーケンスを書き込みが*section_title*フィールド"インデント Example"し*instance_identifier*フィールドが「0 をインスタンス化」します。

```cpp
// The LogToken value was previously returned by a call to 
// SetupGetThreadLogToken.
// The LogToken value specifies a section in one of the text logs.

DWORD Category = TXTLOG_VENDOR; 
DWORD Flags = TXTLOG_DETAILS;

SetupWriteTextLog(LogToken, Category, Flags, TEXT("Subsection A"));

// Additional SetupWriteTextLog calls that write entries at Subsection A indentation level

SetupWriteTextLog(LogToken, Category, Flags | TXTLOG_DEPTH_INCR, TEXT("Subsection A.1"));

// Additional SetupWriteTextLog calls that write entries at Subsection A.1 indentation level

SetupWriteTextLog(LogToken, Category, Flags | TXTLOG_DEPTH_INCR, TEXT("Subsection A.1.1"));

// Additional SetupWriteTextLog calls that write entries at Subsection A.1.1 indentation level

SetupWriteTextLog(LogToken, Category, Flags, TEXT("End of Subsection A.1.1"));

// Additional SetupWriteTextLog calls that write entries at Subsection A.1 indentation level

SetupWriteTextLog(LogToken, Category, Flags | TXTLOG_DEPTH_DECR, TEXT("End of Subsection A.1"));

// Additional SetupWriteTextLog calls that write entries at Subsection A indentation level
SetupWriteTextLog(LogToken, Category, Flags | TXTLOG_DEPTH_DECR, TEXT("End of Subsection A"));
```

テキスト ログのイベント レベルが TXTLOG_DETAILS 以上には、テキスト ログのイベント カテゴリ TXTLOG_VENDOR が有効になっている場合は、前のコードがセクション ヘッダーの後、次のログ エントリを記述します。

次の例では、省略記号 (...) で、以前のログ エントリとしてインデントの同じレベルに 0 個以上の追加のログ エントリを表します。 タイムスタンプは、実際のタイムスタンプで置き換えられます。

```cpp
>>>  [Indentation Example - Instance 0]
>>>  2005/02/13 22:06:28.109: Section start
        : Subsection A
...
        :      Subsection A.1
...
        :           Subsection A.1.1
...
        :           End Subsection A.1.1
...
        :      End of Subsection A.1
...
        : End of Subsection A
```

実際のテキスト ログから取得された、インデントされたセクション エントリの別の例を参照してください[ログ セクションのテキスト本文の形式](format-of-a-text-log-section-body.md)します。

 

 





