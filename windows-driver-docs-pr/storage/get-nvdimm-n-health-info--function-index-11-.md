---
title: NVDIMM-N の正常性に関する情報の取得 (関数インデックス 11)
description: この関数は、NVDIMM モジュールの正常性に関する情報を返します。
ms.assetid: E0FCC4C6-31CB-4D46-ADCE-99EBA2BFF798
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 954b694308066bac6d57f637999458668bad3563
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851357"
---
# <a name="span-idstorageget_nvdimm-n_health_info__function_index_11_spanget-nvdimm-n-health-info-function-index-11"></a><span id="storage.get_nvdimm-n_health_info__function_index_11_"></span>NVDIMM-N の正常性に関する情報の取得 (関数インデックス 11)


この関数は、NVDIMM モジュールの正常性に関する情報を返します。

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
<td align="left"><strong>モジュールの正常性</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>NVDIMM モジュールの正常性に関する詳細情報。</p>
<p><em>バイト0– <em>MODULE_HEALTH_STATUS0</em> (0, 0xA1)</p>
<p></em>バイト1– <em>MODULE_HEALTH_STATUS1</em> (0、0xa2)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>モジュールの現在の温度</strong></td>
<td align="left">2</td>
<td align="left">6</td>
<td align="left"><p>モジュールの気温 (摂氏)。 最小値は0です。</p>
.
<p>この情報は、NVDIMM のシリアルプレゼンス検出の EEPROM の温度センサーから取得されます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>エラーしきい値の状態</strong></td>
<td align="left">1</td>
<td align="left">8</td>
<td align="left"><p>NVDIMM モジュールのエラーしきい値に関する状態。</p>
<p><em>バイト0– <em>ERROR_THRESHOLD_STATUS</em> (0, 0xa5)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>警告しきい値の状態</strong></td>
<td align="left">1</td>
<td align="left">9</td>
<td align="left"><p>NVDIMM モジュールの警告しきい値に関する状態。</p>
<p></em>バイト0– <em>WARNING_THRESHOLD_STATUS</em> (0、0xa7)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>NVM の有効期間</strong></td>
<td align="left">1</td>
<td align="left">10</td>
<td align="left"><p>最後に認識された非揮発性メモリの有効期間の割合の値。</p>
<p><em>バイト0– <em>NVM_LIFETIME</em> (0, 0xC0)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>DRAM 修正不可能な ECC エラーの数</strong></td>
<td align="left">1</td>
<td align="left">11</td>
<td align="left"><p>NVDIMM モジュールからプラットフォームによって検出された修正不可能な ECC エラーの数。</p>
<p></em>バイト0– <em>DRAM_ECC_ERROR_COUNT</em> (2, 0x80)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>しきい値イベントを超えた DRAM 修正可能 ECC エラーの数</strong></td>
<td align="left">1</td>
<td align="left">12</td>
<td align="left"><p>NVDIMM モジュールからプラットフォームによって検出された、修正可能な ECC しきい値を超えたイベントの数。</p>
<p>* バイト0– <em>DRAM_THRESHOLD_ECC_COUNT</em> (2, 0x81)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[正常性に関する重要な情報の取得 (関数インデックス 10)](get-critical-health-info--function-index-10-.md)

[電力源の正常性に関する情報の取得 (関数インデックス 12)](get-energy-source-health-info--function-index-12-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






