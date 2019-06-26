---
title: KSPROPERTY\_BDA\_信号\_ロック\_キャップ
description: クライアントを使用して、KSPROPERTY\_BDA\_信号\_ロック\_CAP ドライバーでは、信号をサポートするロックの種類を決定します。
ms.assetid: 753f1a3c-5308-49a6-96ee-f7d0090f021a
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCK_CAPS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_LOCK_CAPS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d1ae5b0e553f5988f04c9b33ed5b7e0b5dec968
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361130"
---
# <a name="kspropertybdasignallockcaps"></a>KSPROPERTY\_BDA\_信号\_ロック\_キャップ


クライアントを使用して、KSPROPERTY\_BDA\_信号\_ロック\_CAP ドライバーでは、信号をサポートするロックの種類を決定します。

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
<td><p>32 ビットの値のビットごとの OR を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype" data-raw-source="[&lt;strong&gt;BDA_LockType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype)"> <strong>BDA_LockType</strong></a>-型指定された値</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**NodeId** KSP のメンバー\_ノードの管理ノードの識別子を指定しますまたは、暗証番号 (pin) を指定する − 1 に設定されています。

返される 32 ビット値はビットごとの OR の[ **BDA\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype)-ドライバーがサポートするロックの種類を示す値を入力します。

RF チューナーのノードには、このを示す値を提供する必要があります。

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


[**BDA\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ne-bdamedia-_bdalocktype)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

[**KSPROPERTY\_BDA\_信号\_ロック\_型**](ksproperty-bda-signal-lock-type.md)

 

 






