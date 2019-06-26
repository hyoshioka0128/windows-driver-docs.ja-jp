---
title: KSPROPERTY\_BDA\_信号\_ロック
description: クライアントを使用して、KSPROPERTY\_BDA\_信号\_シグナルをロックできるかどうかを判断するロックです。
ms.assetid: 98023f83-2e90-4649-8e85-3e7b7f26b01d
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCKED ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_LOCKED
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e64f81c5d3b92712527310673bbb1ac56db4363
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361132"
---
# <a name="kspropertybdasignallocked"></a>KSPROPERTY\_BDA\_信号\_ロック


クライアントを使用して、KSPROPERTY\_BDA\_信号\_シグナルをロックできるかどうかを判断するロックです。

## <span id="ddk_ksproperty_bda_signal_locked_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_LOCKED_KS"></span>


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
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**NodeId** KSP のメンバー\_ノードの管理ノードの識別子を指定しますまたは、暗証番号 (pin) を指定する − 1 に設定されています。

返される値は、シグナルをロックできるかどうかを示します。 返します**TRUE**シグナルをロックアウトできる場合と**FALSE**それ以外の場合。

RF のチューナー ノードを返す場合**TRUE**フェーズ、ロック、ループ (PLL) ロックが通常示されます。

復調器ノードを返す場合**TRUE**20% 以上の信号の品質が示されます。

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

[**KSPROPERTY\_BDA\_信号\_品質**](ksproperty-bda-signal-quality.md)

 

 






