---
title: 1つの AV/C ユニット内のサブユニットプラグとユニットプラグ間の接続
description: 1つの AV/C ユニット内のサブユニットプラグとユニットプラグ間の接続に関する情報を提供します。
ms.assetid: 12132a0c-9657-4cff-a582-8404a103c46a
keywords:
- 接続 WDK AV/C
- AV/C WDK、接続シナリオ
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ca02f7a8144e4ff1e0e4068add375241433e4bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844714"
---
# <a name="connections-between-subunit-plugs-and-unit-plugs-within-one-avc-unit"></a>1つの AV/C ユニット内のサブユニットプラグとユニットプラグ間の接続


シナリオ1と2は、サブユニットとサブユニットを含むユニットとの間の接続を表します。

### <a name="scenario-1"></a>**シナリオ1**

次の図に示すように、ローカルサブユニットのソースプラグをユニットのアイソクロナス出力プラグインに接続します。

このシナリオは、もともと*Avc*でサポートされていた接続の種類です。

![ローカル pin のデータフローメンバーが kspin\-データフロー\-である接続を示す図](images/avc-ccm1.gif)

シナリオ1では、ローカル pin のデータ**フロー**メンバーがの kspin\_データフロー\_である接続について説明します。

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
<td><p>0xFF (サブユニットを含む単位)</p></td>
<td><p>iPlug (0x0 ~ 0x1E または 0x7F)</p></td>
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
<td><p>宛先プラグ (0x0 ~ 0x1E)</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-2"></a>**シナリオ2**

次の図に示すように、ユニットのアイソクロナス入力プラグからローカルサブユニットのターゲットプラグに接続します。

![ローカル pin のデータフローメンバーが kspin\-データフロー\-の接続を示す図](images/avc-ccm2.gif)

シナリオ2では、ローカル pin のデータ**フロー**メンバーが kspin\_データフロー\_になる接続について説明します。

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
<td><p>サブユニットアドレス</p></td>
<td><p>ソースプラグ (0x0 ~ 0x1E)</p></td>
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
<td><p>0xFF (サブユニットを含む単位)</p></td>
<td><p>oPCR (0x0 から0x1E、または 0x7F)</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>

 

次の一覧では、前の表に示した値の意味について説明します。

-   値 0x0 ~ 0x1E (30 decimal) は、特定のプラグ番号を表します。

-   値0x7F は、AV/C ユニットで使用可能なすべてのアイソクロナス入力または出力プラグ番号を表します。

-   値0xFF は、使用可能なサブユニットソースまたはターゲットプラグアドレスを表します。

-   **DeviceID**列 (ソースとターゲットのサブメニュープラグ) の値は、Av/c CCM コマンドを発行するターゲット Av/c デバイスの物理デバイスオブジェクト (PDO) を検索するために使用されます。

 

 




