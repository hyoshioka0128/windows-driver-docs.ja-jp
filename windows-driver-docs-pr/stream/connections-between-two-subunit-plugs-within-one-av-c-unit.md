---
title: 単一 AV/C ユニット内の 2 つのサブユニット プラグ間の接続
description: 1 つの AV/C ユニット内の 2 つのサブユニット プラグ間の接続に関する情報を提供します。
ms.assetid: 2acd5f23-89b6-40f9-9154-22f1bb51d08c
keywords:
- WDK AV/C の接続
- AV/C WDK、接続のシナリオ
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ea39c3f34246109e5e875af5cdbb07ba2d6c1b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384913"
---
# <a name="connections-between-two-subunit-plugs-within-one-avc-unit"></a>単一 AV/C ユニット内の 2 つのサブユニット プラグ間の接続


シナリオ 3 と 4 では、サブユニットと同じ単位内の別のサブユニットの間の接続を表します。

### <a name="scenario-3"></a>**シナリオ 3**

接続から特定のソース プラグイン (0x0 に 0x1E)、または任意の使用可能なソースの接続 (0 xff) ローカルのサブユニットの変換先のプラグを同じ単位内の別のサブユニットの次の図に示します。

![ローカルの pin のデータ フローのメンバーが kspin が接続を示す図\-データフロー\-で](images/avc-ccm3.gif)

シナリオ 3 は、接続をローカルのピン留めを説明の**データフロー**メンバーが KSPIN\_データフロー\_in です。

次の表に各列のメンバーに対応して、 [ **AVCCONNECTINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avcconnectinfo)構造体であり、ソースのサブユニット プラグのこれらのメンバーの値を指定します。

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
<td><p>ソース単位のデバイス識別子が、サブユニットを含む単位のために使用されません。</p></td>
<td><p>サブユニット アドレス</p></td>
<td><p>変換先のプラグ (0x1E に「0x0」、または 0 xff)</p></td>
<td><p>なし</p></td>
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
<td><p>このシナリオでは、別の単位は関与しませんので、使用されません。</p></td>
<td><p>Self (自己)</p></td>
<td><p>移行先プラグ (0 xff)</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-4"></a>**シナリオ 4**

次の図に示すローカル サブユニットのソースのプラグを特定の宛先プラグ (0x0 に 0x1E)、または別のサブユニットの使用可能な任意 (0 xff) 先プラグから接続します。 シナリオ 4 では、シナリオ 3 の反対を表します。

![ローカルの pin のデータ フローのメンバーが kspin が接続を示す図\-データフロー\-アウト](images/avc-ccm4.gif)

シナリオ 4 は、接続をローカルのピン留めを説明の**データフロー**メンバーが KSPIN\_データフロー\_アウトします。

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
<td><p>ソース単位のデバイス識別子が、サブユニットを含む単位のために使用されません。</p></td>
<td><p>Self (同じサブユニット)</p></td>
<td><p>ソース プラグイン (0 xff)</p></td>
<td><p>なし</p></td>
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
<td><p>このシナリオでは、別の単位は関与しませんので、使用されません。</p></td>
<td><p>サブユニット アドレス</p></td>
<td><p>変換先のプラグ (0x1E に「0x0」、または 0 xff)</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

次の一覧には、上記の表で表示される値の意味について説明します。

-   0x1E に 0x0 (10 進数では 30) の値は、特定のプラグインの番号を表します。

-   送信先アドレスの接続または値 0 xff は、任意のサブユニットが使用可能なソースを表します。

-   「自己」AVCCONNECTINFO 構造体を設定する暗証番号 (pin) が含まれています。

-   内の値、 **DeviceID**に AV/C CCM コマンドを発行するターゲット AV C/デバイスの物理デバイス オブジェクト (PDO) を検索する (ソースと宛先のサブユニット プラグ) 用の列を使用します。

 

 




