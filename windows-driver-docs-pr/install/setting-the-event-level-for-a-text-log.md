---
title: テキスト ログのイベント レベルの設定
description: テキスト ログのイベント レベルの設定
ms.assetid: 3dfd2df3-179e-434c-97fb-fd8329198f8a
keywords:
- イベント レベルの WDK SetupAPI ログ
- テキスト ログの WDK SetupAPI、イベント レベル
- ログ レベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5211e76e3837d4d52cdb7d99c5b7ba476444dd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538652"
---
# <a name="setting-the-event-level-for-a-text-log"></a>テキスト ログのイベント レベルの設定


[SetupAPI](setupapi.md)ログ エントリを書き込みますテキスト ログの唯一の場合に、イベント レベルを設定テキスト ログは、ログ エントリのイベント レベル以上、[イベント カテゴリ](enabling-event-categories-for-a-text-log.md)テキスト ログのログ エントリが有効にします。

次の表は、SetupAPI をサポートするイベント レベルとこれらのイベント レベルを表すマニフェスト定数を示します。 TXTLOG_ERROR は、後に次に高いイベント レベル TXTLOG_WARNING とに、最も低いイベント レベルです。 TXTLOG_VERY_VERBOSE は、最上位のイベント レベルです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント レベル</th>
<th align="left">イベント レベルのマニフェスト定数</th>
<th align="left">イベント レベルのマニフェストの値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>エラーのみを記述します。</p></td>
<td align="left"><p>TXTLOG_ERROR</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>エラーと警告の潜在的な問題を記述します。</p></td>
<td align="left"><p>TXTLOG_WARNING</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>エラー、警告、およびシステム状態の変化を記述します。</p></td>
<td align="left"><p>TXTLOG_SYSTEM_STATE_CHANGE</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="even">
<td align="left"><p>エラー、警告、システム状態の変更、および状態の変更に関連付けられている高度な操作を記述します。</p></td>
<td align="left"><p>TXTLOG_SUMMARY</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>高度な操作状態の変更、および操作の詳細に関連付けられている、エラー、警告、システム状態の変化を記述します。</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>高度な操作状態の変更、およびすべての処理の詳細に関連付けられている、エラー、警告、システム状態の変化を記述します。</p></td>
<td align="left"><p>TXTLOG_VERBOSE</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>大量は、頻繁に余分な情報を生成するものも含め、すべてのログ エントリを記述します。</p></td>
<td align="left"><p>TXTLOG_VERY_VERBOSE</p></td>
<td align="left"><p>7</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="to-set-the-event-level-for-the-setupapi-text-logs--create--or-modify--the-following-reg-dword-registry-value-"></a>SetupAPI テキスト ログのイベント レベルを設定する作成 (または変更)、次[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)レジストリ値。  
**HKEY_LOCAL_MACHINE\\ソフトウェア\\Microsoft\\Windows\\CurrentVersion\\セットアップ\\LogLevel**

場合、 **LogLevel**レジストリ値が存在しないか、0 の値を持つ、SetupAPI は、次の表で説明されている既定値に、アプリケーションのインストールとデバイスのインストールのイベント レベルにテキスト ログを設定します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">テキスト ログ</th>
<th align="left">既定値 (Windows 7 およびそれ以降のバージョン)</th>
<th align="left">既定値 (Windows Vista SP2)</th>
<th align="left">既定値 (Windows Vista SP1 と以前のバージョン)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>アプリケーションのインストールのテキスト ログ (<em>SetupAPI.app.log</em>)</p></td>
<td align="left"><p>TXTLOG_SUMMARY</p></td>
<td align="left"><p>TXTLOG_WARNING</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
</tr>
<tr class="even">
<td align="left"><p>デバイス インストールのテキスト ログ (<em>SetupAPI.dev.log</em>)</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
<td align="left"><p>TXTLOG_DETAILS</p></td>
</tr>
</tbody>
</table>

 

これらのテキスト ログ ファイルの詳細については、[SetupAPI テキスト ログ](setupapi-text-logs.md)を参照してください。

**LogLevel**レジストリ値は 0 x として書式設定*UUUUGHVW、* 場所。

-   マスク 0x000000 によって表される下位 8 ビット*VW*アプリケーションのインストール ログのログ記録をオンにするかどうかを指定し、アプリケーション ログのイベント レベルを指定します。

-   [次へ] 最高 8 ビット、マスク 0x0000 によって表される*GH*時 00 分、およびログ デバイス インストールのテキスト ログになってデバイス インストールのテキスト ログのイベント レベルを指定するかどうかを指定します。

-   0 x のマスクによって表される、最上位ビットを*UUUU*0000 では使用されません。

0 x の値*VW*ビットは、次の表に示すように、アプリケーションのインストール ログのログ記録を制御します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>0xVW</em>値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0 (既定値)</p></td>
<td align="left"><p>ログ記録がオンになっていると前述のように、イベント レベルが既定値に設定されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0F を通じて 0x01</p></td>
<td align="left"><p>ログ記録をオフにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7F まで 0x10</p></td>
<td align="left"><p>ログ記録をオンにし、イベントのレベルを 0xV に設定します。</p></td>
</tr>
</tbody>
</table>

 

0 x の値*GH*ビットは、次の表に示すようにデバイスのインストールのテキスト ログのログ記録を制御します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>0xGH</em>値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0 (既定値)</p></td>
<td align="left"><p>ログ記録がオンになっていると前述のように、イベント レベルが既定値に設定されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0F を通じて 0x01</p></td>
<td align="left"><p>ログ記録をオフにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7F まで 0x10</p></td>
<td align="left"><p>ログ記録をオンにし、イベントのレベルを 0xG に設定します。</p></td>
</tr>
</tbody>
</table>

 

次の表に、一般的な例**LogLevel**値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">LogLevel 値</th>
<th align="left">テキスト ログのイベント レベルを設定します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>既定では、アプリケーションのインストール ログとデバイスのインストール ログ ログ記録をオンにします。 ログ記録レベルを両方のログの既定値に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000101</p></td>
<td align="left"><p>アプリケーションのインストール ログとデバイスのインストール ログの両方のログオフをオンにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00001010</p></td>
<td align="left"><p>アプリケーションのインストール ログとデバイスのインストール ログ ログ記録をオンにします。 TXTLOG_ERROR に両方のログのログ記録レベルを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00002020</p></td>
<td align="left"><p>アプリケーションのインストール ログとデバイスのインストール ログ ログ記録をオンにします。 TXTLOG_WARNING に両方のログのログ記録レベルを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00005050</p></td>
<td align="left"><p>アプリケーションのインストール ログとデバイスのインストール ログ ログ記録をオンにします。 TXTLOG_DETAILS に両方のログのログ記録レベルを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00006060</p></td>
<td align="left"><p>アプリケーションのインストール ログとデバイスのインストール ログ ログ記録をオンにします。 TXTLOG_VERBOSE に両方のログのログ記録レベルを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00007070</p></td>
<td align="left"><p>アプリケーションのインストール ログとデバイスのインストール ログ ログ記録をオンにします。 TXTLOG_VERY_VERBOSE に両方のログのログ記録レベルを設定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





