---
title: 単一 AV/C ユニット内の 2 つのサブユニット プラグ間の接続
description: 1つの AV/C ユニット内の2つのサブユニットプラグ間の接続に関する情報を提供します。
ms.assetid: 2acd5f23-89b6-40f9-9154-22f1bb51d08c
keywords:
- 接続 WDK AV/C
- AV/C WDK、接続シナリオ
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4b3bfc26963b23af8d928e0701fdee1c3682e9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844707"
---
# <a name="connections-between-two-subunit-plugs-within-one-avc-unit"></a>単一 AV/C ユニット内の 2 つのサブユニット プラグ間の接続


シナリオ3と4は、サブユニットと同じ単位の別のサブユニット間の接続を表します。

### <a name="scenario-3"></a>**シナリオ3**

次の図に示すように、特定のソースプラグ (0x0 から 0x1E)、または同じユニット内の別のサブユニットの任意の使用可能なソースプラグ (0xFF) からローカルサブユニットのターゲットプラグに接続します。

![ローカル pin のデータフローメンバーが kspin\-データフロー\-である接続を示す図](images/avc-ccm3.gif)

シナリオ3では、ローカル pin のデータ**フロー**メンバーがの kspin\_データフロー\_である接続について説明します。

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
<td><p>ソースユニットのデバイス識別子がサブユニットを含む単位であるため、使用されません。</p></td>
<td><p>サブユニットアドレス</p></td>
<td><p>ターゲットプラグ (0x0 ~ 0x1E、または 0xFF)</p></td>
<td><p>該当なし</p></td>
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
<td><p>このシナリオには別のユニットが含まれないため、使用されません</p></td>
<td><p>Self (自己)</p></td>
<td><p>宛先プラグ (0xFF)</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-4"></a>**シナリオ4**

次の図に示すように、ローカルサブユニットのソースプラグから特定の宛先プラグ (0x0 から 0x1E)、または別のサブユニットの使用可能な (0xFF) 宛先プラグに接続します。 シナリオ4は、シナリオ3の逆を表します。

![ローカル pin のデータフローメンバーが kspin\-データフロー\-の接続を示す図](images/avc-ccm4.gif)

シナリオ4では、ローカル pin のデータ**フロー**メンバーが kspin\_データフロー\_になっている接続について説明します。

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
<td><p>ソースユニットのデバイス識別子がサブユニットを含む単位であるため、使用されません。</p></td>
<td><p>Self (同じサブユニット)</p></td>
<td><p>ソースプラグ (0xFF)</p></td>
<td><p>該当なし</p></td>
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
<td><p>このシナリオには別のユニットが含まれないため、使用されません</p></td>
<td><p>サブユニットアドレス</p></td>
<td><p>ターゲットプラグ (0x0 ~ 0x1E、または 0xFF)</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>

 

次の一覧では、前の表に示した値の意味について説明します。

-   値 0x0 ~ 0x1E (30 decimal) は、特定のプラグ番号を表します。

-   値0xFF は、使用可能なサブユニットソースまたはターゲットプラグアドレスを表します。

-   "Self" には、AVCCONNECTINFO 構造体の設定先の pin が含まれています。

-   **DeviceID**列 (ソースとターゲットのサブメニュープラグ) の値は、Av/c CCM コマンドを発行するターゲット Av/c デバイスの物理デバイスオブジェクト (PDO) を検索するために使用されます。

 

 




