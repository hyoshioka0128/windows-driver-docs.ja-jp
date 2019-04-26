---
title: ドライバーのランクの例
description: ドライバーのランクの例
ms.assetid: 20fe0f63-5d6c-4617-b5df-b2adb941f257
keywords:
- ドライバーのランクの範囲は WDK デバイスのインストール
- ランクの範囲は WDK デバイスのインストール
- WDK のデバイスのインストールを順位付けの範囲
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c87ab0ba7bd37ab336afc6eca445a44aea595a28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356016"
---
# <a name="driver-rank-example"></a>ドライバーのランクの例


次の一覧があるデバイスを検討してください[識別文字列](device-identification-strings.md)という、HwID_*N*と CID_*N*実際の名前を表します[ハードウェアId](hardware-ids.md)と[互換性 Id](compatible-ids.md):

-   ハードウェア Id の一覧
    ```cpp
     HwID_1, HwID_2
    ```

-   互換性 Id の一覧
    ```cpp
    CID_1, and CID_2
    ```

ハードウェア Id の一覧で最初のハードウェア ID は、デバイスの特定の識別子です。 この例では、HwID_1 です。

またを持つ INF ファイルがあるとします、 [ **INF*モデル*セクション**](inf-models-section.md)次のエントリを持つ場所、INF_*XXX_N*名実際のハードウェア Id および互換性 Id を表してください。

```cpp
DeviceDesc1 = InstallSection1, INF_HWID_1, INF_CID_1, INF_CID_2
```

さらに、ある、INF *DDInstall*という名前のセクション*InstallSection1*次が**FeatureScore**ディレクティブ、機能のスコアの対応する場所、ドライバーは、0x00*GG*0000。

```cpp
FeatureScore=0xGG
```

次の表に、各デバイスによって報告される識別子と、INF に記載されている識別子の一致のランク*モデル*セクション エントリ。 ランクがの合計、[署名スコア](signature-score--windows-vista-and-later-.md)、0 x で表される*SS*000000、[特徴スコア](feature-score--windows-vista-and-later-.md)、0x00 で表される*GG*0000、および[識別子スコア](identifier-score--windows-vista-and-later-.md)、一致する 2 つの識別子の各ケースで、依存します。

<table>
<tr>
<th>デバイス識別子</th>
<th colspan="3">識別子、INF で<i>モデル</i>セクション エントリ</th>
</tr>
<tr>
<td></td>
<td>
<p><b>INF_HwID_1</b></p>
</td>
<td>
<p><b>INF_CID_1</b></p>
</td>
<td>
<p><b>INF_CID_2</b></p>
</td>
</tr>
<tr>
<td>
<p><b>HwID_1</b></p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>0000</p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>1000</p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>1000</p>
</td>
</tr>
<tr>
<td>
<p><b>HwID_2</b></p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>0001</p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>1001</p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>1001</p>
</td>
</tr>
<tr>
<td>
<p><b>CID_1</b></p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>2000</p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>3000</p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>3100</p>
</td>
</tr>
<tr>
<td>
<p><b>CID_2</b></p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>2001</p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>3001</p>
</td>
<td>
<p>0 x をランク付け<i>SSGG</i>3101</p>
</td>
</tr>
</table>

 


