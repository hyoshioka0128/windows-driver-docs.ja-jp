---
title: KSPROPERTY\_BDA\_信号\_ロック\_型
description: クライアントを使用して、KSPROPERTY\_BDA\_信号\_ロック\_シグナルの現在のロックの種類を決定する型。
ms.assetid: 2ddf49c4-f0d1-4918-b564-719c695a83ac
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCK_TYPE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_LOCK_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0233bb16d7c4e18385c675482abfd0aa7b5e5a55
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361124"
---
# <a name="kspropertybdasignallocktype"></a>KSPROPERTY\_BDA\_信号\_ロック\_型


クライアントを使用して、KSPROPERTY\_BDA\_信号\_ロック\_シグナルの現在のロックの種類を決定する型。

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
<td><p>X</p></td>
<td><p>Pin またはフィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype" data-raw-source="[&lt;strong&gt;BDA_LockType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype)"><strong>BDA_LockType</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**NodeId** KSP のメンバー\_ノードの管理ノードの識別子を指定しますまたは、暗証番号 (pin) を指定する − 1 に設定されています。

返された[ **BDA\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype)-型指定された値が現在のロックの種類を識別します。

RF チューナーのノードには、このを示す値を提供する必要があります。

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


[**BDA\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

[**KSPROPERTY\_BDA\_信号\_ロック\_キャップ**](ksproperty-bda-signal-lock-caps.md)

 

 






