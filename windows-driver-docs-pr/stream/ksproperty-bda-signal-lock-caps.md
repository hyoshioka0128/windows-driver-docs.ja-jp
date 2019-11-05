---
title: KSK プロパティ\_BDA\_シグナル\_ロック\_キャップ
description: クライアントは、KSK プロパティ\_BDA\_SIGNAL\_ロック\_キャップを使用して、ドライバーがシグナルに対してサポートできるロックの種類を決定します。
ms.assetid: 753f1a3c-5308-49a6-96ee-f7d0090f021a
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCK_CAPS ストリーミングメディアデバイス
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
ms.openlocfilehash: d0e673d3e0e1c1201c27b7ed04028948be8de066
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838067"
---
# <a name="ksproperty_bda_signal_lock_caps"></a>KSK プロパティ\_BDA\_シグナル\_ロック\_キャップ


クライアントは、KSK プロパティ\_BDA\_SIGNAL\_ロック\_キャップを使用して、ドライバーがシグナルに対してサポートできるロックの種類を決定します。

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
<td><p>対応</p></td>
<td><p>X</p></td>
<td><p>ピン留めまたはフィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype" data-raw-source="[&lt;strong&gt;BDA_LockType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)"><strong>BDA_LockType</strong></a>型の値のビットごとの or を含む32ビット値</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、コントロールノードの識別子を指定します。または、pin を指定するために−1に設定されています。

返された32ビット値は、ドライバーがサポートしているロックの種類を示す[**LockType\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)型の値のビットごとの or です。

RF チューナーノードは、この表示を提供する必要があります。

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


[**BDA\_LockType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**KSK プロパティ\_BDA\_シグナル\_ロック\_型**](ksproperty-bda-signal-lock-type.md)

 

 






