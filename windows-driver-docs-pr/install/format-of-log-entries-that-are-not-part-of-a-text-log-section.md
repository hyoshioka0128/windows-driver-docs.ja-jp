---
title: テキスト ログ セクションの一部ではないログ エントリの書式
description: テキスト ログ セクションの一部ではないログ エントリの書式
ms.assetid: c2c7567e-dfb4-49d3-acc9-034f6544633e
keywords:
- WDK SetupAPI ログ出力を書式設定します。
- テキスト ログの WDK SetupAPI、エントリのセクションの一部ではないです。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8489381804a608883393c34c73ddd9a987b519af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377054"
---
# <a name="format-of-log-entries-that-are-not-part-of-a-text-log-section"></a>テキスト ログ セクションの一部ではないログ エントリの書式


テキスト ログは、テキスト ログのヘッダーのテキストのログ セクションに含まれていないログ エントリを含めることができます。 このようなエントリでは、任意のセクションに関連付けられていないと、セクション間一般に、混在しています。 このようなログ エントリの形式では、*エントリ*_*プレフィックス*フィールド、 *time_stamp*フィールド、 *event_category*フィールド、および、 *formatted_message*フィールドに、次のようにします。

*entry_prefix time_stamp event_category formatted_message*

次の一覧には、ログ エントリのフィールドについて説明します。

<a href="" id="entry-prefix-field"></a>*entry_prefix*フィールド  
メッセージの種類を示します。 *Entry_prefix*フィールドは常に存在し、左側の列の右側の列に文字列の意味が示されます、次の表に記載されている文字列のいずれかが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Entry_prefix フィールド</th>
<th align="left">［メッセージの種類］</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"!!!  "</code></pre></td>
<td align="left"><p>テキスト ログでエラー メッセージ</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"!    "</code></pre></td>
<td align="left"><p>テキスト ログに警告メッセージ</p></td>
</tr>
<tr class="odd">
<td align="left"><pre space="preserve"><code>"   . "</code></pre></td>
<td align="left"><p>情報メッセージ (エラー メッセージまたは警告メッセージ) を除くテキスト ログ</p></td>
</tr>
<tr class="even">
<td align="left"><pre space="preserve"><code>"     "</code></pre></td>
<td align="left"><p>情報メッセージ (エラー メッセージまたは警告メッセージ) を除く、アプリケーションのインストールのテキスト ログ</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="time-stamp-field"></a>*time_stamp*フィールド  
ログに記録されたイベントが発生したときのシステム時刻を示します。 *Time_stamp*フィールドはオプションであり、インストール アプリケーションのタイムスタンプがログ エントリを含めることが要求された場合にのみ表示されます。 形式、 *time_stamp*フィールドが記載されているのと同じ[テキスト ログ セクション ヘッダーの形式](format-of-a-text-log-section-header.md)します。

<a href="" id="event-category-field"></a>*event_category*フィールド  
ログ エントリを作成した SetupAPI 操作のカテゴリを示します。 *Event_category*フィールドは、通常はあるは必要ありません。 存在する場合、 *event_category*フィールドでは、記載されている文字列のいずれかが含まれる[ログ セクションのテキスト本文の形式](format-of-a-text-log-section-body.md)します。

<a href="" id="formatted-message"></a>*formatted_message*  
ログ エントリに固有の情報が含まれています。 *Formatted_message*フィールドが一般に存在するは必要ありません。

**注**  ログ エントリの文字の最大長は 336 します。

 

テキスト ログ エントリの次の例は、デバイスのインストールのテキスト ログから取得されます。 例では、最初の 2 つのログ エントリと、テキスト ログのセクションの一部ではありません。 ユーザー モードのプラグ アンド プレイ (PnP) マネージャーでは、サーバー側の PCI デバイスのインストールの開始を示すデバイス インストールのテキスト ログでこれらのログ エントリを作成しました。 サーバー側のインストールには、さらに、最初の 2 つのログ エントリの例を次のテキストのログ セクション ヘッダーで示されるテキスト ログ セクションが作成されます。

注意を*event_category*フィールドの最初の 2 つのログ エントリをユーザー モードの PnP マネージャーがこれらのログ エントリを書いたこと示します。

```cpp
   . ump: Start service install for: PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38
   . ump: Creating Install Process: rundll32.exe

>>>  [Device Install - PCI\VEN_104C&DEV_8019&SUBSYS_8010104C&REV_00\3&61aaa01&0&38]
>>>  2005/02/13 22:06:28.109: Section start
```

 

 





