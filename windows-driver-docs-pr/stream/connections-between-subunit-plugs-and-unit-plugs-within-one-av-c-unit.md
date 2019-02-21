---
title: サブユニット プラグと 1 つの AV/C 単位内でユニット プラグ間の接続
description: サブユニット プラグとユニット プラグインするときに 1 つの AV/C ユニット内の間の接続に関する情報を提供します。
ms.assetid: 12132a0c-9657-4cff-a582-8404a103c46a
keywords:
- WDK AV/C の接続
- AV/C WDK、接続のシナリオ
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63bd1a5309063d7c144c34cbd66b79bae51f4939
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557359"
---
# <a name="connections-between-subunit-plugs-and-unit-plugs-within-one-avc-unit"></a>サブユニット プラグと 1 つの AV/C 単位内でユニット プラグ間の接続


シナリオ 1 と 2 では、サブユニットと単位を含む、サブユニットの間の接続を表します。

### <a name="scenario-1"></a>**シナリオ 1**

次の図に示すユニットのアイソクロナス出力のプラグにローカルのサブユニットのソースのプラグを接続します。

このシナリオでサポートされていた最初の接続の種類は、 *Avc.sys*します。

![ローカルの pin のデータ フローのメンバーが kspin が接続を示す図\-データフロー\-で](images/avc-ccm1.gif)

シナリオ 1 は、接続をローカルのピン留めを説明の**データフロー**メンバーが KSPIN\_データフロー\_in です。

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
<td><p>使用されなくソース ユニット&#39;s デバイス識別子は、サブユニットを含むユニット</p></td>
<td><p>0 xff (のサブユニットを含むユニット)</p></td>
<td><p>iPlug (0x0 に 0x1E または 0x7F)</p></td>
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
<td><p>移行先プラグ (0x0 0x1E)</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-2"></a>**シナリオ 2**

次の図に示すユニットのアイソクロナス入力プラグからローカル サブユニットの変換先のプラグに接続します。

![ローカルの pin のデータ フローのメンバーが kspin が接続を示す図\-データフロー\-アウト](images/avc-ccm2.gif)

シナリオ 2 は、接続をローカルのピン留めを説明の**データフロー**メンバーが KSPIN\_データフロー\_アウトします。

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
<td><p>使用されなくソース ユニット&#39;s デバイス識別子は、サブユニットを含むユニット</p></td>
<td><p>サブユニット アドレス</p></td>
<td><p>ソース プラグイン (0x0 0x1E)</p></td>
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
<td><p>0 xff (のサブユニットを格納している単位)</p></td>
<td><p>oPCR (0x0 に 0x1E または 0x7F)</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

次の一覧には、上記の表で表示される値の意味について説明します。

-   0x1E に 0x0 (10 進数では 30) の値は、特定のプラグインの番号を表します。

-   0x7f までの値は、任意、使用可能なアイソクロナス入力または出力プラグ番号 AV/C 単位を表します。

-   送信先アドレスの接続または値 0 xff は、任意のサブユニットが使用可能なソースを表します。

-   内の値、 **DeviceID**に AV/C CCM コマンドを発行するターゲット AV C/デバイスの物理デバイス オブジェクト (PDO) を検索する (ソースと宛先のサブユニット プラグ) 用の列を使用します。

 

 




