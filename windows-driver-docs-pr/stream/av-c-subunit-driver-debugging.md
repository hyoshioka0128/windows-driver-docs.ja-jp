---
title: AV/C サブユニット ドライバーのデバッグ
description: AV/C サブユニット ドライバーのデバッグ
ms.assetid: d669157c-60fa-4b7a-8f33-58923a3f2230
keywords:
- Avc.sys 関数ドライバー WDK、デバッグ
- トレース メッセージ WDK AV/C
- メッセージ WDK AV/C
- ドライバー WDK AV/C のデバッグ
- ジェネリック メッセージ WDK AV/C
- プラグ アンド プレイ WDK AV/C
- PnP WDK AV/C
- 電源管理 WDK AV/C
- I/O WDK AV/C
- 接続メッセージ WDK AV/C
- AV/C WDK、デバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35ef78fbb475fc80fff515b32170c17ae84535d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323508"
---
# <a name="avc-subunit-driver-debugging"></a>AV/C サブユニット ドライバーのデバッグ





Windows Vista では、デバッグ バージョンの前に*Avc.sys*デバッグ ウィンドウに出力するメッセージをトレースすることができます。 Windows Vista バージョンの*Avc.sys* Event Tracing for Windows (ETW) を使用します。

*AvcDebugLevel* ULONG 型は、トレース レベルのビットマップ。 各ニブルでは、トレース出力のカテゴリを表します。 既定値は、0x00CCCCCC で、すべてのメッセージのカテゴリをエラーと警告の出力のレベルに設定します。 AV/C コマンドの動作を監視する最適な設定は、0x000ECCCC (メッセージのトレース クラスは、出力の AV/C カテゴリを追加します)。 すべてのデバッグ出力をオフにすべてのビットを 0 に設定します。 各カテゴリ用のビットマップを以下に示します。

**一般的なメッセージのカテゴリ**

ジェネリックのカテゴリは、すべての一般的な出力に適用されます。 出力の最も興味深いクラスはフローを有効にすると、各関数の開始と終了ポイントでのメッセージのログ記録。 Windows Millennium Edition (Windows Me)、Windows 98、または Windows 95 では、すべて TL を実行するコンピューターで\_フロー (とほとんど TL\_トレース メッセージ)、.ntkern 循環バッファー プールに移動します。 ログ エントリを型を使用してこれらを表示する **.ntkern**デバッガー、および D のオプションを選択します。 後のバッファーを一度に 1 つのページのダンプを続行する D キーを押して、space キーを押します。 ダンプをキャンセルするその他の任意のキーを押します。 .Ntkern 記録を無効にし、標準的なデバッグ出力に、メッセージの送信、使用、 **e ulind**デバッガーを設定するコマンド、 **ulind**変数を 1 (既定値は 0)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>説明</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_MASK</p></td>
<td><p>0x0000000F</p></td>
</tr>
<tr class="even">
<td><p>TL_FLOW</p></td>
<td><p>0x00000001</p></td>
</tr>
<tr class="odd">
<td><p>TL_TRACE</p></td>
<td><p>0x00000002</p></td>
</tr>
<tr class="even">
<td><p>TL_WARNING</p></td>
<td><p>0x00000004</p></td>
</tr>
<tr class="odd">
<td><p>TL_ERROR</p></td>
<td><p>0x00000008</p></td>
</tr>
</tbody>
</table>

 

**プラグ アンド プレイ メッセージ カテゴリ**

プラグ アンド プレイ (PnP) カテゴリは、PnP に関連するすべての出力に適用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>説明</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_PNP_MASK</p></td>
<td><p>0x000000F0</p></td>
</tr>
<tr class="even">
<td><p>TL_PNP_TRACE</p></td>
<td><p>0x00000020</p></td>
</tr>
<tr class="odd">
<td><p>TL_PNP_WARNING</p></td>
<td><p>0x00000040</p></td>
</tr>
<tr class="even">
<td><p>TL_PNP_ERROR</p></td>
<td><p>0x00000080</p></td>
</tr>
</tbody>
</table>

 

**電源管理メッセージのカテゴリ**

電源管理カテゴリは、休止状態など、電源管理に関連するすべての出力に適用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>説明</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_POWER_MASK</p></td>
<td><p>0x00000F00</p></td>
</tr>
<tr class="even">
<td><p>TL_POWER_TRACE</p></td>
<td><p>0x00000200</p></td>
</tr>
<tr class="odd">
<td><p>TL_POWER_WARNING</p></td>
<td><p>0x00000400</p></td>
</tr>
<tr class="even">
<td><p>TL_POWER_ERROR</p></td>
<td><p>0x00000800</p></td>
</tr>
</tbody>
</table>

 

**I/O のメッセージのカテゴリ**

I/O のカテゴリは IRP の処理など、interdriver の通信に関連するすべての出力に適用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>説明</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_IO_MASK</p></td>
<td><p>0x0000F000</p></td>
</tr>
<tr class="even">
<td><p>TL_IO_NOISE</p></td>
<td><p>0x00001000</p></td>
</tr>
<tr class="odd">
<td><p>TL_IO_TRACE</p></td>
<td><p>0x00002000</p></td>
</tr>
<tr class="even">
<td><p>TL_IO_WARNING</p></td>
<td><p>0x00004000</p></td>
</tr>
<tr class="odd">
<td><p>TL_IO_ERROR</p></td>
<td><p>0x00008000</p></td>
</tr>
</tbody>
</table>

 

**AV/C メッセージ カテゴリ**

AV/C カテゴリは、AV/C コマンドに関連付けられているすべての出力とオブジェクトのリストと、スピン ロックするには、潜在的な関連性の一部のドライバーの内部メッセージに適用されます (TL\_IO\_ノイズ I/O メッセージ カテゴリ)。 TL に含まれる\_IO\_メッセージのトレース カテゴリはコマンドの実行時間。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>説明</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_AVC_MASK</p></td>
<td><p>0x000F0000</p></td>
</tr>
<tr class="even">
<td><p>TL_AVC_NOISE</p></td>
<td><p>0x00010000</p></td>
</tr>
<tr class="odd">
<td><p>TL_AVC_TRACE</p></td>
<td><p>0x00020000</p></td>
</tr>
<tr class="even">
<td><p>TL_AVC_WARNING</p></td>
<td><p>0x00040000</p></td>
</tr>
<tr class="odd">
<td><p>TL_AVC_ERROR</p></td>
<td><p>0x00080000</p></td>
</tr>
</tbody>
</table>

 

**接続メッセージ カテゴリ**

接続のカテゴリは、すべてのプラグイン接続に関連する出力を処理します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>説明</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TL_CXN_MASK</p></td>
<td><p>0x00F00000</p></td>
</tr>
<tr class="even">
<td><p>TL_CXN_NOISE</p></td>
<td><p>0x00100000</p></td>
</tr>
<tr class="odd">
<td><p>TL_CXN_TRACE</p></td>
<td><p>0x00200000</p></td>
</tr>
<tr class="even">
<td><p>TL_CXN_WARNING</p></td>
<td><p>0x00400000</p></td>
</tr>
<tr class="odd">
<td><p>TL_CXN_ERROR</p></td>
<td><p>0x00800000</p></td>
</tr>
</tbody>
</table>

 

 

 




