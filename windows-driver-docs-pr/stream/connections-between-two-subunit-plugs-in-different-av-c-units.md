---
title: 異なる AV/C ユニット内の 2 つのサブユニット プラグ間の接続
description: 異なる AV/C ユニット内の 2 つのサブユニット プラグ間の接続
ms.assetid: 20d209b3-2516-4913-9f31-b14afddb78fb
keywords:
- 接続 WDK AV/C
- AV/C WDK、接続シナリオ
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e6864ef9ec80829e31de5d30fcf84edfafcc010
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842428"
---
# <a name="connections-between-two-subunit-plugs-in-different-avc-units"></a>異なる AV/C ユニット内の 2 つのサブユニット プラグ間の接続


シナリオ5と6は、1つのユニットのサブユニットから別のユニットのサブユニットへの接続を表します。 これらの種類の接続では、**信号のソース**と**入力の選択**CCM コマンドが必要です。

### <a href="" id="scenario-5"></a>シナリオ5

**シグナルソース**: ターゲットユニットは、特定のサブユニットのソースプラグ (0x0)、または任意の使用可能なサブユニットのソースプラグ (0xff)、特定のユニットのアイソクロナス出力プラグ、または使用可能なユニットのアイソクロナス出力プラグに接続します (アイソクロナス出力プラグ番号)。

**入力の選択**: ローカルユニットは、ターゲットのサブユニットのソースプラグから任意のローカルユニットのアイソクロナス入力プラグに接続し、任意の使用可能なサブユニットのターゲットプラグに接続します。

![シナリオ5サブユニット接続](images/avc-ccm5.gif)

シナリオ5では、ローカル pin のデータ**フロー**メンバーがの kspin\_データフロー\_である接続について説明します。

次の表の各列は、 [**Avcconnectinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)構造体のメンバーに対応しています。また、これらのメンバーについて、ソースサブユニットのプラグの値を指定します。

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
<th>UnitPlugNumber (アイソクロナス出力用)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>対象</p></td>
<td><p>サブユニットアドレス</p></td>
<td><p>ソースプラグ (0x0 ~ 0x1E、または 0xFF)</p></td>
<td><p>0x0 から0x1E、または0x7F</p></td>
</tr>
</tbody>
</table>

 

次の表の各列は、AVCCONNECTINFO 構造体のメンバーに対応しています。また、これらのメンバーについては、同期先サブユニットのプラグに対して値を指定します。

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
<th>UnitPlugNumber (アイソクロナス入力用)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Self (自己)</p></td>
<td><p>Self (自己)</p></td>
<td><p>宛先プラグ (0xFF)</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="scenario-6"></a>シナリオ6

**シグナルソース**: ローカルユニットは、任意の使用可能な (0xff) サブユニットソースプラグに接続して、任意のローカルユニットのアイソクロナス出力プラグに接続します (そして、ユニットのアイソクロナス出力プラグ番号を返します)。

**入力の選択**: ターゲットユニットは、ローカルユニット固有のアイソクロナス出力プラグ (SIGNAL source CCM コマンドで返されます) から、特定の (0X0 から 0x1e)、またはターゲットユニット上の使用可能な (0x7f) アイソクロナス入力プラグに接続し、に接続します。特定の (0x0 から 0x1E)、または任意の使用可能な (0xFF) サブユニットターゲットプラグインターゲットユニット (このシナリオはシナリオ5とは逆です)。

![シナリオ6サブユニット接続](images/avc-ccm6.gif)

シナリオ6では、ローカル pin のデータ**フロー**メンバーが kspin\_データフロー\_になっている接続について説明します。

次の表の各列は、AVCCONNECTINFO 構造体のメンバーに対応しています。また、これらのメンバーについて、ソースサブユニットのプラグの値を指定します。

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
<th>UnitPlugNumber (アイソクロナス出力用)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Self (自己)</p></td>
<td><p>Self (自己)</p></td>
<td><p>ソースプラグ (0xFF)</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

次の表の各列は、AVCCONNECTINFO 構造体のメンバーに対応しています。また、これらのメンバーについては、同期先サブユニットのプラグに対して値を指定します。

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
<th>UnitPlugNumber (アイソクロナス入力用)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>対象</p></td>
<td><p>サブユニットアドレス</p></td>
<td><p>宛先プラグ (0x0 ~ 0x1E)</p></td>
<td><p>0x0 から0x1E、または0x7F</p></td>
</tr>
</tbody>
</table>

 

次の一覧では、前の表に示した値の意味について説明します。

-   値 0x0 ~ 0x1E (30 decimal) は、特定のプラグ番号を表します。

-   値0x7F は、AV/C ユニットで使用可能なすべてのアイソクロナス入力または出力プラグ番号を表します。

-   値0xFF は、使用可能なサブユニットソースまたはターゲットプラグアドレスを表します。

-   "Self" には、AVCCONNECTINFO 構造体の設定先の pin が含まれています。 "Target" は AVCCONNECTINFO 構造体のデータを表します。

-   **[デバイス ID]** 列 (ソースサブメニューとターゲットサブメニュープラグ用) の値は、Av/c CCM コマンドを発行するターゲットの Av/c デバイスの物理デバイスオブジェクト (PDO) を検索するために使用されます。

 

 




