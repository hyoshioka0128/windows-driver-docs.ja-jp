---
title: 異なる AV/C ユニット内の 2 つのユニット プラグ間の接続
description: 異なる AV/C ユニット内の 2 つのユニット プラグ間の接続
ms.assetid: b9c45304-33a2-4d02-9c38-1d124a33f0f2
keywords:
- 接続 WDK AV/C
- AV/C WDK、接続シナリオ
- AVCCONNECTINFO
- AVCPRECONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06e889459dc78b223c6ace0cc8866b0007e9492c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844705"
---
# <a name="connections-between-two-unit-plugs-in-different-avc-units"></a>異なる AV/C ユニット内の 2 つのユニット プラグ間の接続


シナリオ7と8は、1つのユニットのサブユニットから別のユニットのサブユニットへの接続を表します。この場合、ターゲットは、1つの AV/C ユニット内のサブユニットに対するユニット接続をサポートしていません。 この種の接続では、**信号のソース**と入力の**選択**CCM コマンドが必要です。

シナリオ7と8では、サブユニットのソースまたはターゲットのプラグを示しています。これには、 **\_\_\_フラグ**が指定されている[**Avcpreconnectinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo) **構造体のフラグメンバーで**設定されているサブシステムのソースまたはターゲットのプラグが記述されています。これは、avc で変換され*ます。* サブユニットのアドレスを0xff にします。

### <a name="scenario-7"></a>**シナリオ7**

**シグナルソース**: ローカル単位では、ユニット内接続はサポートされていません。

**入力の選択**: ローカルユニットは、ターゲットユニット上の使用可能な (0x7f) アイソクロナス出力プラグから、ローカルユニット上の使用可能な (0x7f) アイソクロナス入力プラグに接続し、特定の (0X0 から 0x1e) または使用可能な任意の (0xff) サブユニットに接続します。ローカルユニットのターゲットプラグ。

![ローカル pin のデータフローメンバーが kspin\-データフロー\-である接続を示す図](images/avc-ccm7.gif)

シナリオ7では、ローカル pin のデータ**フロー**メンバーが kspin\_のデータフロー\_である接続について説明します。

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
<td><p>ソースプラグ (0xFF)-値は無視されます</p></td>
<td><p>0x0 から0x1E、または0xFF</p></td>
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
<td><p>ターゲットプラグ (0x0 ~ 0x1E、または 0xFF)</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-8"></a>**シナリオ8**

**シグナルソース**: ローカルユニットは、任意のサブユニットのソースプラグに接続して、使用可能な (0x7f) アイソクロナス出力プラグに接続します (そして、アイソクロナス出力プラグ番号を返します)。

**入力の選択**: ターゲットユニットは、ローカルユニットのアイソクロナス出力プラグ (SIGNAL source CCM コマンドで返されます) から、ターゲットユニット上の使用可能な (0x7f) アイソクロナス入力プラグに接続します。

![ローカル pin のデータフローメンバーが kspin\-データフロー\-の接続を示す図](images/avc-ccm8.gif)

シナリオ8では、ローカル pin のデータ**フロー**メンバーが kspin\_データフロー\_になっている接続について説明します。

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
<td><p>ソースプラグ (0x0 ~ 0x1E、または 0xFF)</p></td>
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
<td><p>宛先プラグ (0xFF)-値は無視されます</p></td>
<td><p>0x0 から0x1E、または0x7F</p></td>
</tr>
</tbody>
</table>

 

次の一覧では、前の表に示した値の意味について説明します。

-   値 0x0 ~ 0x1E (30 decimal) は、特定のプラグ番号を表します。

-   値0x7F は、AV/C ユニットで使用可能なすべてのアイソクロナス入力または出力プラグ番号を表します。

-   値0xFF は、使用可能なサブユニットソースまたはターゲットプラグアドレスを表します。

-   "Self" には、AVCCONNECTINFO 構造体の設定先の pin が含まれています。 "Target" は AVCCONNECTINFO 構造体のデータを表します。

-   **DeviceID**列 (ソースとターゲットのサブメニュープラグ) の値は、Av/c CCM コマンドを発行するターゲット Av/c デバイスの物理デバイスオブジェクト (PDO) を検索するために使用されます。

 

 




