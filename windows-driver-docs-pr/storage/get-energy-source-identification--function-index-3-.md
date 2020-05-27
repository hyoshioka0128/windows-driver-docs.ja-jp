---
title: 動力源 ID の取得 (関数インデックス 3)
description: この関数は、ホスト管理またはデバイス管理が可能なエネルギーソースに関する識別情報を返します。
ms.assetid: E1589FD0-5D03-42EF-8078-0AE53CFB1ACA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 655fa98a8906617af6c9c4db92a2d7563078366c
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851336"
---
# <a name="get-energy-source-identification-function-index-3"></a>動力源 ID の取得 (関数インデックス 3)


この関数は、ホスト管理またはデバイス管理が可能なエネルギーソースに関する識別情報を返します。

> [!NOTE]
> スター () でマークされたすべてのレジスタ \* は、バイトアドレッシング可能なエネルギーバッキングインターフェイスの仕様で定義されているレジスタです。



## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>代入


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

[なし] :

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>Output


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">バイト長</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状態</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>にアクセスしてください。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>エネルギーソースポリシー</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>モジュールでサポートされているエネルギーソースポリシーに関する情報。</p>
<p>* バイト0– <em>ENERGY_SOURCE_POLICY</em> (0, 0x14)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>デバイスで管理されている Id</strong></td>
<td align="left">11</td>
<td align="left">5</td>
<td align="left">&gt; [!Note]<br/><p>&gt;このフィールドに有効なデータが含まれるのは、現在の ES ポリシーがデバイスで管理されている場合のみです (つまり、SET_ES_POLICY_STATUS のビット 2 (0, 0x70) が設定されています)。 その他の ES ポリシーでは、このフィールドは0になります。</p>

<p>詳細については、デバイスで管理されている Id を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ホストによって管理される ES Id</strong></td>
<td align="left">3</td>
<td align="left">16</td>
<td align="left">&gt; [!Note]<br/><p>&gt;このフィールドに有効なデータが含まれるのは、現在の ES ポリシーがホストで管理されている場合のみです (つまり、SET_ES_POLICY_STATUS のビット 3 (0, 0x70) が設定されています)。 その他の ES ポリシーでは、このフィールドは0になります。</p>

<p>詳細については、「ホスト側で管理される Id」を参照してください。</p></td>
</tr>
</tbody>
</table>



### <a name="span-iddevice_managed_es_identificationspanspan-iddevice_managed_es_identificationspanspan-iddevice_managed_es_identificationspandevice-managed-es-identification"></a><span id="Device_Managed_ES_Identification"></span><span id="device_managed_es_identification"></span><span id="DEVICE_MANAGED_ES_IDENTIFICATION"></span>デバイスで管理されている Id

ES ポリシーの値が0の場合、デバイスによって管理される ES Id フィールドは有効で、次のフィールドがあります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">バイト長</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ES ハードウェアリビジョン</strong></td>
<td align="left">2</td>
<td align="left">5</td>
<td align="left"><p>ES ハードウェアリビジョン。</p>
<p><em>バイト0– <em>ES_HWREV</em> (1, 0x04)</p>
<p>バイト 1-予約済み。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES ファームウェアのリビジョン</strong></td>
<td align="left">2</td>
<td align="left">7</td>
<td align="left"><p>ES ファームウェアのリビジョン。</p>
<p></em>バイト0– <em>ES_FWREV0</em> (1, 0x06)</p>
<p><em>バイト1– <em>ES_FWREV1</em> (1, 0x07)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 正常性チェックの頻度</strong></td>
<td align="left">1</td>
<td align="left">9</td>
<td align="left"><p>モジュールの正常性評価の現在の頻度。</p>
<p></em>バイト0– <em>AUTO_ES_HEALTH_CHECK_FREQUENCY</em> (0, 0xa9)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>課金のタイムアウト</strong></td>
<td align="left">2</td>
<td align="left">10</td>
<td align="left"><p>最悪の場合の請求時間 (秒)。 値は0より大きくなければなりません。</p>
<p><em>バイト0– <em>ES_CHARGE_TIMEOUT0</em> (1, 0x10)</p>
<p></em>バイト1– <em>ES_CHARGE_TIMEOUT1</em> (1, 0x11)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 最小動作温度</strong></td>
<td align="left">1</td>
<td align="left">12</td>
<td align="left"><p>ES の最小の動作温度 (摂氏)。 サポートされる最小値は0です。</p>
<p><em>バイト0– <em>MIN_ES_OPERATING_TEMP</em> (1, 0x12)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最大の動作温度</strong></td>
<td align="left">1</td>
<td align="left">13</td>
<td align="left"><p>ES の最大の動作温度 (摂氏)。</p>
<p></em>バイト0– <em>MAX_ES_OPERATING_TEMP</em> (1, 0x13)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 属性</strong></td>
<td align="left">1</td>
<td align="left">14</td>
<td align="left"><p>ES に関する属性。</p>
<p><em>バイト0– <em>ES_ATTRIBUTES</em> (1, 0x14)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES テクノロジ</strong></td>
<td align="left">1</td>
<td align="left">15</td>
<td align="left"><p>ES で使用されるテクノロジ。</p>
<p></em>バイト0– <em>ES_TECH</em> (1, 0x15)</p></td>
</tr>
</tbody>
</table>



### <a name="span-idhost_managed_es_identificationspanspan-idhost_managed_es_identificationspanspan-idhost_managed_es_identificationspanhost-managed-es-identification"></a><span id="Host_Managed_ES_Identification"></span><span id="host_managed_es_identification"></span><span id="HOST_MANAGED_ES_IDENTIFICATION"></span>ホストによって管理される ES Id

ES ポリシーの値が1の場合、ホストによって管理される ES 識別フィールドは有効で、次のフィールドがあります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">バイト長</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ES 正常性チェックの頻度</strong></td>
<td align="left">1</td>
<td align="left">16</td>
<td align="left"><p>プラットフォームの正常性評価の現在の頻度。</p>
<p><em>バイト0– <em>AUTO_ES_HEALTH_FREQUENCY</em> (0, 0xa9)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 属性</strong></td>
<td align="left">1</td>
<td align="left">17</td>
<td align="left"><p>ホスト側管理のエネルギー供給元の属性。</p>
<p></em>バイト0– <em>HOST_MANAGED_ES_ATTRIBUTES</em> (2, 0x82)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES テクノロジ</strong></td>
<td align="left">1</td>
<td align="left">18</td>
<td align="left"><p>ビットマップ</p>
<ul>
<li><p>[0]: 定義されていません</p></li>
<li><p>[1]: スーパーコンデンサー</p></li>
<li><p>[2]: バッテリ</p></li>
<li><p>[3]: ハイブリッドコンデンサー</p></li>
<li><p>[7:4] 予約済み</p></li>
</ul></td>
</tr>
</tbody>
</table>



## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)










