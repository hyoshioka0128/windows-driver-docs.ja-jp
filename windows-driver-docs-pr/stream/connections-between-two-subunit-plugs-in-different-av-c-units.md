---
title: 2 つのサブユニット プラグ AV/C の異なる単位間の接続
description: 2 つのサブユニット プラグ AV/C の異なる単位間の接続
ms.assetid: 20d209b3-2516-4913-9f31-b14afddb78fb
keywords:
- WDK AV/C の接続
- AV/C WDK、接続のシナリオ
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cca8650152be9426efe116983dc958ac08dcf6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537887"
---
# <a name="connections-between-two-subunit-plugs-in-different-avc-units"></a>2 つのサブユニット プラグ AV/C の異なる単位間の接続


シナリオ 5 および 6 では、別の単位でのサブユニットを 1 つのまとまりのサブユニット間の接続を表します。 これらの種類の接続が必要な**信号のソース**と**入力選択**CCM コマンド。

### <a href="" id="scenario-5"></a> シナリオ 5

**信号のソース**:(0x0 に 0x1E)、特定のサブユニット ソース プラグに接続するターゲット ユニットまたは任意のサブユニットが使用可能なソースを特定の単位アイソクロナス出力プラグインでは、または使用可能なユニット アイソクロナス出力 (0 xff) をプラグインするプラグイン (およびユニットのアイソクロナス出力プラグインの数を返します)。

**入力選択**:ローカル ユニットでは、ローカル ユニットのアイソクロナス入力プラグインするときのいずれかにターゲットのサブユニットのソース プラグインから接続し、使用可能なサブユニット先プラグに接続します。

![シナリオ 5 サブユニット接続](images/avc-ccm5.gif)

シナリオ 5 は、接続をローカルのピン留めを説明の**データフロー**メンバーが KSPIN\_データフロー\_in です。

次の表に各列のメンバーに対応して、 [ **AVCCONNECTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff554101)構造体であり、ソースのサブユニット プラグのこれらのメンバーの値を指定します。

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
<td><p>ソース プラグイン (0x1E に「0x0」、または 0 xff)</p></td>
<td><p>0x0 に 0x1E または 0x7F</p></td>
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
<td><p>移行先プラグ (0 xff)</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="scenario-6"></a> シナリオ 6

**信号のソース**:ローカル ユニット アイソクロナス出力プラグインするときに、ローカルの単位のいずれかに、使用可能な (0 xff) サブユニット ソース プラグに接続する (をユニットのアイソクロナス出力プラグインの数を返します)

**入力選択**:ターゲット ユニットが (信号のソース CCM コマンドで返される) ローカル ユニットの特定アイソクロナス出力プラグインから特定の (0x0 0x1E) に接続または使用可能な (0x7F) アイソクロナス入力ターゲット ユニットに接続および特定 (0x0 0x1E) またはそのいずれかに接続し、(0 xff) のサブユニットの使用できる変換先は、ターゲットの単位 (このシナリオではシナリオ 5 の逆) に接続します。

![シナリオ 6 サブユニット接続](images/avc-ccm6.gif)

シナリオ 6 は、接続をローカルのピン留めを説明の**データフロー**メンバーが KSPIN\_データフロー\_アウトします。

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
<td><p>ソース プラグイン (0 xff)</p></td>
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
<td><p>移行先プラグ (0x0 0x1E)</p></td>
<td><p>0x0 に 0x1E または 0x7F</p></td>
</tr>
</tbody>
</table>

 

次の一覧には、上記の表で表示される値の意味について説明します。

-   0x1E に 0x0 (10 進数では 30) の値は、特定のプラグインの番号を表します。

-   0x7f までの値は、任意、使用可能なアイソクロナス入力または出力プラグ番号 AV/C 単位を表します。

-   送信先アドレスの接続または値 0 xff は、任意のサブユニットが使用可能なソースを表します。

-   「自己」AVCCONNECTINFO 構造体を設定する暗証番号 (pin) が含まれています。 「ターゲット」AVCCONNECTINFO 構造のデータを表します。

-   内の値、**デバイス ID**に AV/C CCM コマンドを発行するターゲット AV C/デバイスの物理デバイス オブジェクト (PDO) を検索する (ソースと宛先のサブユニット プラグ) 用の列を使用します。

 

 




