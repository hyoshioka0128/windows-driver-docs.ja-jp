---
title: 異なる AV/C ユニット内の 2 つのユニット プラグ間の接続
description: 異なる AV/C ユニット内の 2 つのユニット プラグ間の接続
ms.assetid: b9c45304-33a2-4d02-9c38-1d124a33f0f2
keywords:
- WDK AV/C の接続
- AV/C WDK、接続のシナリオ
- AVCCONNECTINFO
- AVCPRECONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93d1fe5bc36ab8aa7281fadfae1cd2275784935f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374212"
---
# <a name="connections-between-two-unit-plugs-in-different-avc-units"></a>異なる AV/C ユニット内の 2 つのユニット プラグ間の接続


シナリオ 7 と 8 では、ターゲットが 1 つの AV/C 単位内でユニットの接続のサブユニットをサポートしません、別の単位でのサブユニットを 1 つのまとまりのサブユニット間の接続を表します。 このタイプの接続が必要な**信号のソース**と**入力選択**CCM コマンド。

シナリオ 7 および 8 がサブユニットの送信元または送信先のプラグを記述する、 **KSPIN\_フラグ\_AVC\_PCRONLY**フラグを設定、**フラグ**のメンバー[**AVCPRECONNECTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff554103)によって変換が構造体は、 *Avc.sys*サブユニットのアドレスの 0 xff までです。

### <a name="scenario-7"></a>**シナリオ 7**

**信号のソース**:ローカル ユニットでは、ユニット内の接続はサポートされていません。

**入力選択**:すべて使用できる (0 xff) のサブユニット変換先がローカルのユニットに接続またはローカル ユニットがターゲット ユニットで、使用可能な (0x7F) アイソクロナス出力プラグから、使用可能な (0x7F) アイソクロナス入力プラグ ローカル ユニットに接続し、特定の (0x0 0x1E) に接続.

![ローカルの pin のデータ フローのメンバーが kspin が接続を示す図\-データフロー\-で](images/avc-ccm7.gif)

シナリオ 7 は、接続をローカルのピン留めを説明の**データフロー**メンバーが KSPIN\_データフロー\_in です。

次の表に各列のメンバーに対応して、 [ **AVCCONNECTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff554101)構造体し、ソースのサブユニット プラグのこれらのメンバーの値を指定します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceID</th>
<th>SubunitAddress</th>
<th>SubunitPlugNumber</th>
<th>UnitPlugNumber (用アイソクロナス出力)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>対象</p></td>
<td><p>サブユニット アドレス</p></td>
<td><p>ソース プラグイン (0 xff) の値は無視されます</p></td>
<td><p>0x0 に 0x1E または 0 xff の場合</p></td>
</tr>
</tbody>
</table>

 

次の表の各列は、AVCCONNECTINFO 構造体のメンバーに対応し、変換先のサブユニット プラグのこれらのメンバーの値を指定します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceID</th>
<th>SubunitAddress</th>
<th>SubunitPlugNumber</th>
<th>UnitPlugNumber (用アイソクロナス入力)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Self (自己)</p></td>
<td><p>Self (自己)</p></td>
<td><p>変換先のプラグ (0x1E に「0x0」、または 0 xff)</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-8"></a>**シナリオ 8**

**信号のソース**:ローカルのユニットは、サブユニットのソース、使用可能な (0x7F) アイソクロナス出力プラグインのプラグに接続する (および、アイソクロナス出力プラグインの数を返します)。

**入力選択**:ターゲットのユニットは、(信号のソース CCM コマンドで返される) ローカルのユニットのアイソクロナス出力プラグインから、使用可能な (0x7F) アイソクロナス入力プラグ ターゲット ユニットに接続します。

![ローカルの pin のデータ フローのメンバーが kspin が接続を示す図\-データフロー\-アウト](images/avc-ccm8.gif)

シナリオ 8 は、接続をローカルのピン留めを説明の**データフロー**メンバーが KSPIN\_データフロー\_アウトします。

次の表の各列は、AVCCONNECTINFO 構造体のメンバーに対応し、ソースのサブユニット プラグのこれらのメンバーの値を指定します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceID</th>
<th>SubunitAddress</th>
<th>SubunitPlugNumber</th>
<th>UnitPlugNumber (用アイソクロナス出力)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Self (自己)</p></td>
<td><p>Self (自己)</p></td>
<td><p>ソース プラグイン (0x1E に「0x0」、または 0 xff)</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

次の表の各列は、AVCCONNECTINFO 構造体のメンバーに対応し、変換先のサブユニット プラグのこれらのメンバーの値を指定します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceID</th>
<th>SubunitAddress</th>
<th>SubunitPlugNumber</th>
<th>UnitPlugNumber (用アイソクロナス入力)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>対象</p></td>
<td><p>サブユニット アドレス</p></td>
<td><p>変換先接続 (0 xff) - 値は無視されます。</p></td>
<td><p>0x0 に 0x1E または 0x7F</p></td>
</tr>
</tbody>
</table>

 

次の一覧には、上記の表で表示される値の意味について説明します。

-   0x1E に 0x0 (10 進数では 30) の値は、特定のプラグインの番号を表します。

-   0x7f までの値は、任意、使用可能なアイソクロナス入力または出力プラグ番号 AV/C 単位を表します。

-   送信先アドレスの接続または値 0 xff は、任意のサブユニットが使用可能なソースを表します。

-   「自己」AVCCONNECTINFO 構造体を設定する暗証番号 (pin) が含まれています。 「ターゲット」AVCCONNECTINFO 構造のデータを表します。

-   内の値、 **DeviceID**に AV/C CCM コマンドを発行するターゲット AV C/デバイスの物理デバイス オブジェクト (PDO) を検索する (ソースと宛先のサブユニット プラグ) 用の列を使用します。

 

 




