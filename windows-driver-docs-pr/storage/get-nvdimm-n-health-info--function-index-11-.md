---
title: NVDIMM-N の正常性に関する情報の取得 (関数インデックス 11)
description: この関数は、NVDIMM-N のモジュールの正常性に関する情報を返します。
ms.assetid: E0FCC4C6-31CB-4D46-ADCE-99EBA2BFF798
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ddadffd117fad3f731e3cd2f64f56c1ad11a397d
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348810"
---
# <a name="span-idstoragegetnvdimm-nhealthinfofunctionindex11spanget-nvdimm-n-health-info-function-index-11"></a><span id="storage.get_nvdimm-n_health_info__function_index_11_"></span>NVDIMM-N の正常性の情報 (関数インデックス 11) を取得します。


この関数は、NVDIMM-N のモジュールの正常性に関する情報を返します。

&gt; \[!注\]    &gt;、星が付いたマークされているすべてのレジスタ (\*) バイト アドレス指定可能なエネルギー バックアップ インターフェイス仕様で定義されているレジスタします。

 

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
<td align="left"><strong>モジュールの正常性</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>NVDIMM-N モジュールの正常性に関する詳細を取得します。</p>
<p><em>バイト 0 – <em>MODULE_HEALTH_STATUS0</em> (0, 0xA1)</p>
<p></em>1 – バイト<em>MODULE_HEALTH_STATUS1</em> (0, 0xA2)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>モジュールの現在の気温</strong></td>
<td align="left">2</td>
<td align="left">6</td>
<td align="left"><p>モジュールの温度を摂氏でします。 最小値は 0 です。</p>
.
<p>この情報は、NVDIMM-N のシリアル プレゼンスを検出 EEPROM の温度センサーから取得されます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>エラーしきい値の状態</strong></td>
<td align="left">1</td>
<td align="left">8</td>
<td align="left"><p>NVDIMM-N モジュールでエラーのしきい値に関する状態。</p>
<p><em>Byte 0 – <em>ERROR_THRESHOLD_STATUS</em> (0, 0xA5)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>警告しきい値の状態</strong></td>
<td align="left">1</td>
<td align="left">9</td>
<td align="left"><p>NVDIMM-N モジュールで警告しきい値に関する状態。</p>
<p></em>Byte 0 – <em>WARNING_THRESHOLD_STATUS</em> (0, 0xA7)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>NVM の有効期間</strong></td>
<td align="left">1</td>
<td align="left">10</td>
<td align="left"><p>最後の既知の非揮発性メモリの有効期間のパーセント値。</p>
<p><em>バイト 0 – <em>NVM_LIFETIME</em> (0, 0xC0)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>DRAM ECC 修正不可能なエラーの数</strong></td>
<td align="left">1</td>
<td align="left">11</td>
<td align="left"><p>NVDIMM-N モジュールから、プラットフォームによって検出不可能の ECC エラーの数。</p>
<p></em>バイト 0 – <em>DRAM_ECC_ERROR_COUNT</em> (2, 0x80)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>DRAM 修正可能な ECC エラーしきい値イベントの数</strong></td>
<td align="left">1</td>
<td align="left">12</td>
<td align="left"><p>修正可能な ECC しきい値を超えましたイベント数、NVDIMM-N のモジュールから、プラットフォームによって検出されました。</p>
<p>* バイト 0 – <em>DRAM_THRESHOLD_ECC_COUNT</em> (2, 0x81)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[重要な正常性の情報 (関数インデックス 10) を取得します。](get-critical-health-info--function-index-10-.md)

[エネルギー ソース ヘルス情報 (関数インデックス 12) を取得します。](get-energy-source-health-info--function-index-12-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






