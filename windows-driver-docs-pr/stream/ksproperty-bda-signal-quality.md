---
title: KSK プロパティ\_BDA\_シグナル\_品質
description: クライアントは、KSK プロパティ\_BDA\_SIGNAL\_QUALITY を使用して、信号から正常に抽出されたデータの量をパーセントで判断します。
ms.assetid: 8967400d-3a10-475a-997a-d756837c3438
keywords:
- KSPROPERTY_BDA_SIGNAL_QUALITY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_QUALITY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1bbafdb5bd5c60b1dfd1025b841f250d11d433a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843605"
---
# <a name="ksproperty_bda_signal_quality"></a>KSK プロパティ\_BDA\_シグナル\_品質


クライアントは、KSK プロパティ\_BDA\_SIGNAL\_QUALITY を使用して、信号から正常に抽出されたデータの量をパーセントで判断します。

## <span id="ddk_ksproperty_bda_signal_quality_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_QUALITY_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>ピン留めまたはフィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、コントロールノードの識別子を指定します。または、pin を指定するために−1に設定されています。

戻り値は、シグナルから抽出されるデータをパーセントで指定します。

Demodulation ノードは、通常、シグナルの品質を報告します。これは、元のデータをシグナルから抽出できる量を表したものです。

アナログ信号の場合、この割合は、水平方向の同期 (HSync) と垂直方向の同期 (垂直同期) のタイミング、および水平非表示 (HBlanking) と垂直非表示 (VBlanking) に含まれている情報を調べることによって計算できます。不定期.

デジタル信号の場合、次のようにパケット巡回冗長検査 (CRC) と前方エラー修正 (FEC) の信頼度値を調べることによって、この割合を計算できます。

-   100% が理想的です。

-   95% は、表示されたときにほとんど実体的の成果物を表示します。

-   90% には、簡単に表示できるように十分な数のアーティファクトが含まれています。

-   80% は、表示可能な最小レベルです。

-   60% は、電子番組ガイド (EPG) の受信など、データサービスを使用するための最小レベルです。

-   20% は、適切に変調された信号が存在するが、有用なデータを生成できないことを demodulator が認識していることを示します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 






