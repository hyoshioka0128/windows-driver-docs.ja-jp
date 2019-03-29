---
title: 動力源 ID の取得 (関数インデックス 3)
description: この関数は、管理されているホストまたはデバイス管理について、エネルギー ソース (ES) などの識別情報を返します。
ms.assetid: E1589FD0-5D03-42EF-8078-0AE53CFB1ACA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5c76bff652d9cad466c66907bc26828a0395c435
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348933"
---
# <a name="get-energy-source-identification-function-index-3"></a>動力源 ID の取得 (関数インデックス 3)


この関数は、管理されているホストまたはデバイス管理について、エネルギー ソース (ES) などの識別情報を返します。

&gt; \[!注\]   
&gt;すべてのレジスタを星が付いたマークされている (\*) バイト アドレス指定可能なエネルギー バックアップ インターフェイス仕様で定義されているレジスタします。



## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>入力


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

なし。

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>出力


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
<th align="left">バイトの長さ</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ステータス</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>について。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>エネルギーの元のポリシー</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>モジュールでサポートされているエネルギーの元のポリシーに関する情報です。</p>
<p>* バイト 0 – <em>ENERGY_SOURCE_POLICY</em> (0, 0x14)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES のデバイス管理の識別</strong></td>
<td align="left">11</td>
<td align="left">5</td>
<td align="left">&amp;gt; [!Note]<br/><p>&amp;gt;ES の現在のポリシーがデバイス管理されている場合にのみこのフィールドに有効なデータが含まれます (つまりビット SET_ES_POLICY_STATUS (0, 0x70 です) の第 2 に設定されている)。 他のすべての ES ポリシーでは、このフィールドは 0 になります。</p>

<p>については、Device-Managed ES の識別情報を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES の管理されているホストの識別</strong></td>
<td align="left">3</td>
<td align="left">16</td>
<td align="left">&amp;gt; [!Note]<br/><p>&amp;gt;ES の現在のポリシーが管理されているホストの場合にのみこのフィールドに有効なデータが含まれます (つまりビット SET_ES_POLICY_STATUS (0, 0x70 です) の 3 が設定されます)。 他のすべての ES ポリシーでは、このフィールドは 0 になります。</p>

<p>については、Host-Managed ES の識別情報を参照してください。</p></td>
</tr>
</tbody>
</table>



### <a name="span-iddevicemanagedesidentificationspanspan-iddevicemanagedesidentificationspanspan-iddevicemanagedesidentificationspandevice-managed-es-identification"></a><span id="Device_Managed_ES_Identification"></span><span id="device_managed_es_identification"></span><span id="DEVICE_MANAGED_ES_IDENTIFICATION"></span>ES のデバイス管理の識別

ES のポリシーの値が 0 と Device-Managed ES 識別フィールドは有効な次のフィールドがあります。

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
<th align="left">バイトの長さ</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ES のハードウェアのリビジョン</strong></td>
<td align="left">2</td>
<td align="left">5</td>
<td align="left"><p>ES ハードウェア リビジョン。</p>
<p><em>バイト 0 – <em>ES_HWREV</em> (1, 0x04)</p>
<p>1 - バイトに予約されています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES のファームウェアのリビジョン</strong></td>
<td align="left">2</td>
<td align="left">7</td>
<td align="left"><p>ES ファームウェアのリビジョン。</p>
<p></em>バイト 0 – <em>ES_FWREV0</em> (1, 0x06)</p>
<p><em>1 – バイト<em>ES_FWREV1</em> (1, 0x07)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES の正常性チェックの頻度</strong></td>
<td align="left">1</td>
<td align="left">9</td>
<td align="left"><p>現在のモジュールの ES の正常性評価の頻度。</p>
<p></em>バイト 0 – <em>AUTO_ES_HEALTH_CHECK_FREQUENCY</em> (0, 0xA9)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES の料金のタイムアウト</strong></td>
<td align="left">2</td>
<td align="left">10</td>
<td align="left"><p>最悪のケース (秒) を ES では、時間が課金されます。 値は 0 より大きくなければものとします。</p>
<p><em>バイト 0 – <em>ES_CHARGE_TIMEOUT0</em> (1, 0x10)</p>
<p></em>1 – バイト<em>ES_CHARGE_TIMEOUT1</em> (1, パターン)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES の最小オペレーティング温度</strong></td>
<td align="left">1</td>
<td align="left">12</td>
<td align="left"><p>動作温度 (摂氏)、ES の最小値。 サポートされる最小値は 0 になります。</p>
<p><em>Byte 0 – <em>MIN_ES_OPERATING_TEMP</em> (1, 0x12)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES の最大オペレーティング温度</strong></td>
<td align="left">1</td>
<td align="left">13</td>
<td align="left"><p>動作温度 (摂氏)、ES の最大値。</p>
<p></em>バイト 0 – <em>MAX_ES_OPERATING_TEMP</em> (1, 0x13)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 属性</strong></td>
<td align="left">1</td>
<td align="left">14</td>
<td align="left"><p>ES に関する属性。</p>
<p><em>バイト 0 – <em>ES_ATTRIBUTES</em> (1, 0x14)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES テクノロジ</strong></td>
<td align="left">1</td>
<td align="left">15</td>
<td align="left"><p>ES で使用されるテクノロジです。</p>
<p></em>バイト 0 – <em>ES_TECH</em> (1, 0x15)</p></td>
</tr>
</tbody>
</table>



### <a name="span-idhostmanagedesidentificationspanspan-idhostmanagedesidentificationspanspan-idhostmanagedesidentificationspanhost-managed-es-identification"></a><span id="Host_Managed_ES_Identification"></span><span id="host_managed_es_identification"></span><span id="HOST_MANAGED_ES_IDENTIFICATION"></span>ES の管理されているホストの識別

ES ポリシーの値が 1 と Host-Managed ES 識別フィールドは有効な次のフィールドがあります。

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
<th align="left">バイトの長さ</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ES の正常性チェックの頻度</strong></td>
<td align="left">1</td>
<td align="left">16</td>
<td align="left"><p>現在、プラットフォームの ES の正常性評価の頻度です。</p>
<p><em>バイト 0 – <em>AUTO_ES_HEALTH_FREQUENCY</em> (0, 0xA9)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 属性</strong></td>
<td align="left">1</td>
<td align="left">17</td>
<td align="left"><p>エネルギーのホストで管理されたソースの属性。</p>
<p></em>バイト 0 – <em>HOST_MANAGED_ES_ATTRIBUTES</em> (2, 0x82)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES テクノロジ</strong></td>
<td align="left">1</td>
<td align="left">18</td>
<td align="left"><p>ビットマスク。</p>
<ul>
<li><p>[0] :未定義</p></li>
<li><p>[1] :Supercapacitor</p></li>
<li><p>[2] :バッテリー</p></li>
<li><p>[3] :ハイブリッド コンデンサー</p></li>
<li><p>7:4 の予約済み</p></li>
</ul></td>
</tr>
</tbody>
</table>



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)










