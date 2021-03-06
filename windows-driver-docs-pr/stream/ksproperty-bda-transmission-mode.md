---
title: KSPROPERTY\_BDA\_伝送\_モード
description: クライアントを使用して、KSPROPERTY\_BDA\_伝送\_復調器ノード シグナルの送信ブロードキャストする方法の設定を制御するモード。
ms.assetid: 8d49a45f-031f-445f-ae2e-d98223a7d524
keywords:
- KSPROPERTY_BDA_TRANSMISSION_MODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_TRANSMISSION_MODE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b65a0bce233dbf0a618d74fcc3efa60ca5303a8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355416"
---
# <a name="kspropertybdatransmissionmode"></a>KSPROPERTY\_BDA\_伝送\_モード


クライアントを使用して、KSPROPERTY\_BDA\_伝送\_復調器ノード シグナルの送信ブロードキャストする方法の設定を制御するモード。

## <span id="ddk_ksproperty_bda_transmission_mode_ks"></span><span id="DDK_KSPROPERTY_BDA_TRANSMISSION_MODE_KS"></span>


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
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>TransmissionMode</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

TransmissionMode 列挙型から返される値は、シグナルの送信ブロードキャストする方法の設定を指定します。

**NodeId** KSP のメンバー\_ノード復調器ノードの識別子を指定します。

<a name="requirements"></a>必要条件
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


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

[**TransmissionMode**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/transmissionmode)

 

 






