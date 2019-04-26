---
title: KSPROPERTY\_BDA\_信号\_品質
description: クライアントを使用して、KSPROPERTY\_BDA\_信号\_割合で示した信号から正常に抽出されたデータの量を決定する品質。
ms.assetid: 8967400d-3a10-475a-997a-d756837c3438
keywords:
- KSPROPERTY_BDA_SIGNAL_QUALITY ストリーミング メディア デバイス
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
ms.openlocfilehash: 216aa48c1c0a35f54dae4c20979723b58eba10a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348128"
---
# <a name="kspropertybdasignalquality"></a>KSPROPERTY\_BDA\_信号\_品質


クライアントを使用して、KSPROPERTY\_BDA\_信号\_割合で示した信号から正常に抽出されたデータの量を決定する品質。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>Pin またはフィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**NodeId** KSP のメンバー\_ノードの管理ノードの識別子を指定しますまたは、暗証番号 (pin) を指定する − 1 に設定されています。

返される値は、割合としての信号から抽出されたデータを指定します。

復調ノードは、通常信号の品質は、元のデータの量でしたから抽出される信号の表現を報告します。

水平方向の同期 (水平同期) と垂直方向の同期 (垂直) のタイミングを調べることによって (HBlanking) で水平方向の空白と垂直ブランキング ・ (VBlanking) に含まれる情報を見る場合は、アナログ信号は、この割合を計算することができます。間隔。

デジタル信号の場合は、この割合は、パケットの巡回冗長検査 (CRC) を調べることで計算することができ、エラー修正 (FEC) 信頼度の値を次のように転送。

-   100% は最適です。

-   95% では、ほとんどの (ほぼ見分ける) 成果物レンダリングされるときに示していません。

-   90% には、簡単に表示するか、十分なほとんどのアイテムが含まれていません。

-   80% は、表示できるように最小のレベルです。

-   60% は、動作する電子番組ガイド (EPG) の受信を含め、データ サービスを期待する最小のレベルです。

-   20% は、復調器が正しく変調された信号が存在するを使用するための十分なデータを生成できないことに注意してくださいであることを示します。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






