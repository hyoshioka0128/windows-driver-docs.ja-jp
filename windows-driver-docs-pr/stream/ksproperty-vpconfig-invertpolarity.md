---
title: KSPROPERTY\_VPCONFIG\_INVERTPOLARITY
description: KSPROPERTY\_VPCONFIG\_INVERTPOLARITY プロパティを反転させるビデオ ポートを強制する、グローバル極性フラグを切り替えます。
ms.assetid: c0b69aa4-0f81-42b4-9a69-5afcf702f5f1
keywords:
- KSPROPERTY_VPCONFIG_INVERTPOLARITY ストリーミング メディア デバイス
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
ms.openlocfilehash: abbe2f20956b3d68b70570f37b97bd7c0bd234e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572770"
---
# <a name="kspropertyvpconfiginvertpolarity"></a>KSPROPERTY\_VPCONFIG\_INVERTPOLARITY


KSPROPERTY\_VPCONFIG\_INVERTPOLARITY プロパティを反転させるビデオ ポートを強制する、グローバル極性フラグを切り替えます。

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
<th>取得</th>
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>ブール値</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ブール値です。 指定**TRUE** 、極性を反転するかを指定する**FALSE**極性を反転するようにします。

<a name="remarks"></a>コメント
-------

KSPROPERTY\_VPCONFIG\_INVERTPOLARITY プロパティ要求が状態を返す\_を正常に完了を示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

この機能を使用しないモデルが状態を返す必要がありますので、この機能は、ハードウェアに依存する、\_いない\_実装されていません。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






