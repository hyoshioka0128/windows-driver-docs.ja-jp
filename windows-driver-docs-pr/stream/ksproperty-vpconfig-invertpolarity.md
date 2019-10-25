---
title: KSK プロパティ\_VPCONFIG\_INVERTPOLARITY 性
description: KSK プロパティ\_VPCONFIG\_INVERTPOLARITY プロパティは、グローバル極性フラグを切り替えて、ビデオポートを強制的に反転します。
ms.assetid: c0b69aa4-0f81-42b4-9a69-5afcf702f5f1
keywords:
- KSPROPERTY_VPCONFIG_INVERTPOLARITY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_INVERTPOLARITY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9217c78dc893e90d223b32fff1b084b3829558a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842810"
---
# <a name="ksproperty_vpconfig_invertpolarity"></a>KSK プロパティ\_VPCONFIG\_INVERTPOLARITY 性


KSK プロパティ\_VPCONFIG\_INVERTPOLARITY プロパティは、グローバル極性フラグを切り替えて、ビデオポートを強制的に反転します。

## <span id="ddk_ksproperty_vpconfig_invertpolarity_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_INVERTPOLARITY_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>Boolean</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) はブール値です。 極性を反転する**場合は TRUE**を指定します。極性を反転しないようにする場合は**FALSE**を指定します。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_VPCONFIG\_INVERTPOLARITY プロパティ要求は、正常に完了したことを示す\_状態を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

この機能はハードウェアに依存しているため、この機能を使用しないモデルは、実装さ\_れていない状態\_返す必要があります。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






