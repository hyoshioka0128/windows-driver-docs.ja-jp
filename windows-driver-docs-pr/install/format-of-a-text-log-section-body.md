---
title: テキスト ログのセクションの本文の形式
description: テキスト ログのセクションの本文の形式
ms.assetid: 37995fc8-9822-4c2f-ba6a-154a86e1eadf
keywords:
- WDK SetupAPI にセクションの本文
- WDK SetupAPI ログ出力を書式設定します。
- テキスト ログの WDK SetupAPI、セクションの本文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea4c7c443019a11f101b411df8c67f037c2e1711
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559870"
---
# <a name="format-of-a-text-log-section-body"></a>テキスト ログのセクションの本文の形式


A*テキスト ログ セクション本文*テキスト ログのセクションに関連付けられている操作に適用される 0 個以上のログ エントリが含まれています。 セクション本文のログ エントリの形式が含まれます、 *entry_prefix*フィールド、 *time_stamp*フィールド、 *event_category*フィールド、*インデント*フィールド、および*formatted_message*フィールドに、次のように。

*entry_prefix time_stamp event_category インデント formatted_message*

セクションの本文のログ エントリの文字の最大長は 336 です。

<a href="" id="entry-prefix-field"></a>*entry_prefix*フィールド  
ログ エントリが、エラー メッセージ、警告メッセージまたは情報メッセージかどうかを示します。 *Entry_prefix*フィールドは常に存在し、次の表に記載されている文字列のいずれかが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>Entry_prefix</em>フィールド</th>
<th align="left">メッセージの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre space="preserve"><code>&quot;!!!  &quot;</code></pre></td>
<td align="left"><p>エラー メッセージ</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>&quot;!    &quot;</code></pre></td>
<td align="left"><p>警告メッセージ</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>&quot;     &quot;</code></pre></td>
<td align="left"><p>エラー メッセージまたは警告メッセージ以外の情報メッセージ</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="time-stamp-field"></a>*time_stamp*フィールド  
ログに記録されたイベントが発生したときのシステム時刻を示します。 *Time_stamp*フィールドは省略可能と SetupAPI では、既定では、タイムスタンプが含まれません。 ただし、 [ **SetupWriteTextLog** ](https://msdn.microsoft.com/library/windows/hardware/ff552218)ログ エントリの時刻スタンプを含むをサポートしています。 形式、 *time_stamp*フィールドは、の形式と同じ、 *time_stamp*で説明されているフィールド[テキスト ログ セクション ヘッダーの形式](format-of-a-text-log-section-header.md)します。

<a href="" id="event-category-field"></a>*event_category*フィールド  
ログ エントリを作成した SetupAPI 操作のカテゴリを示します。 *Event_category*フィールドは、通常はあるは必要ありません。 場合、 *event_category*フィールドが存在する、次の表に記載されている文字列のいずれかが含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>Event_category</em>文字列をフィールド</th>
<th align="left">SetupAPI 操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre space="preserve"><code>&quot;...: &quot;</code></pre></td>
<td align="left"><p>ベンダーから提供された操作</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>&quot;bak: &quot;</code></pre></td>
<td align="left"><p>バックアップ データ</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>&quot;cci: &quot;</code></pre></td>
<td align="left"><p>クラスのインストーラーや共同インストーラーの操作</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>&quot;cpy: &quot;</code></pre></td>
<td align="left"><p>ファイルのコピー</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>&quot;dvi: &quot;</code></pre></td>
<td align="left"><p>デバイスのインストール</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>&quot;flq: &quot;</code></pre></td>
<td align="left"><p>ファイルのキューを管理します。</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>&quot;inf: &quot;</code></pre></td>
<td align="left"><p>INF ファイルを管理します。</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>&quot;ndv: &quot;</code></pre></td>
<td align="left"><p>デバイスの新規作成ウィザード</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>&quot;prp: &quot;</code></pre></td>
<td align="left"><p>デバイスとドライバーのプロパティを管理します。</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>&quot;reg: &quot;</code></pre></td>
<td align="left"><p>レジストリ設定を管理します。</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>&quot;set: &quot;</code></pre></td>
<td align="left"><p>セットアップ全般</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>&quot;sig: &quot;</code></pre></td>
<td align="left"><p>デジタル署名を確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>&quot;sto: &quot;</code></pre></td>
<td align="left"><p>ドライバー ストアを管理します。</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>&quot;ui : &quot;</code></pre></td>
<td align="left"><p>管理ユーザー インターフェイス ダイアログ ボックス</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>&quot;ump: &quot;</code></pre></td>
<td align="left"><p>ユーザー モードの PnP マネージャー</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="indentation-field"></a>*インデント*フィールド  
0 個以上のシーケンスから成る*インデント ユニット*インデント単位は 5 つのスペースを含む固定幅文字列です。 *インデント*フィールドは省略可能、既定では、SetupAPI がインデントを含まない。 **SetupWriteTextLog**インデント ユニットに含まれるログ エントリの数の変更をサポートしています。

<a href="" id="formatted-message-field"></a>*formatted_message*フィールド  
ログ エントリに適用される特定の情報が含まれています。

ログに記録されるセクション本文エントリは、ログが設定されているイベントのレベルと、ログを有効になっているカテゴリ レベルによって異なります。 これらの設定の詳細については、次を参照してください。 [SetupAPI ログのレジストリ設定](setupapi-logging-registry-settings.md)します。

SetupAPI がデバイスのインストールに適用される操作をグループ化するセクションを作成するときにも再帰的にグループ化のサブセクションにセクション本文ログ エントリ。 方法は、ログ エントリにインデントを設定して注釈を付けますでは、SetupAPI にサブセクションが区別されます。 一般的なデバイスのインストール」セクションから次の例では、このような 1 つのサブセクションが表示されます。 サブセクションは、ログ エントリで始まる"dvi: {ドライバーのリストを作成しました"ログ エントリで終了"dvi: {ドライバーのリスト作成 - exit(0x00000000)}"。 このサブセクションが含まれるログ エントリの一般的なシーケンスを示しています、 *entry_prefix*、 *event_category*、*インデント*、および*formatted_message*フィールド。 ログ エントリを記述した SetupAPI 操作は、インデントを作成して、書式設定されたメッセージの内容を指定します。 この例では、イベント レベルが TXTLOG_DETAILS に設定されており、この例では有効にしていたすべてのカテゴリ レベル。

```cpp
>>>  [Device Install - PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38]
>>>  2005/02/13 22:06:28.109: Section start
...
 Deleted section body log entries
...
     dvi: {Build Driver List}
     dvi:      Enumerating all INFs...
     dvi:      Found driver match:
     dvi:           HardwareID - PCI\VEN_104C&DEV_8019
     dvi:           InfName    - C:\WINDOWS\inf\1394.inf
     dvi:           DevDesc    - Texas Instruments OHCI Compliant IEEE 1394 Host Controller
     dvi:           DrvDesc    - Texas Instruments OHCI Compliant IEEE 1394 Host Controller
     dvi:           Provider   - Microsoft
     dvi:           Mfg        - Texas Instruments
     dvi:           InstallSec - TIOHCI_Install
     dvi:           ActualSec  - TIOHCI_Install.NT
 dvi:           Rank       - 0x00002001
     dvi:           DrvDate    - 10/01/2002
 dvi:           Version    - 6.0.5033.0 
!!!  inf:      InfCache: Error flagging 1394.inf for match string pci\ven_104c&dev_8019
     dvi: {Build Driver List - exit(0x00000000)}
...
 Deleted section body log entries 
...
<<<  [2005/02/13 22:06:29.000: Section end]
<<<  [Exit Status(0x00000000)]
```

 

 





