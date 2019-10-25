---
title: KSK メソッド\_BDA\_チェック\_変更
description: クライアントは KSK メソッド\_BDA\_使用して\_の変更をチェックし、要求された変更の一覧が機能するかどうかを判断します。
ms.assetid: 00a2d0ca-0ede-4ae5-ab2a-95d19143ea7c
keywords:
- KSMETHOD_BDA_CHECK_CHANGES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_CHECK_CHANGES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0579adf7ddda38b0294aa4f90a4e4d427f9794a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838863"
---
# <a name="ksmethod_bda_check_changes"></a>KSK メソッド\_BDA\_チェック\_変更


クライアントは KSK メソッド\_BDA\_使用して\_の変更をチェックし、要求された変更の一覧が機能するかどうかを判断します。

## <span id="ddk_ksmethod_bda_check_changes_ks"></span><span id="DDK_KSMETHOD_BDA_CHECK_CHANGES_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>このメソッドの指定

**フラグ**メンバーが ksk メソッドに設定されている ksk メソッド\_型\_NONE。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>メソッドデータ

なし

<a name="remarks"></a>注釈
-------

変更の一覧をコミットする前に、ネットワークプロバイダーによって KSK メソッド\_BDA\_チェックされ、要求された変更が機能するかどうかを判断するための\_変更要求が作成されます。 ミニドライバーは、リソースが使用可能であることを保証するために、この要求が行われたときにリソースを予約することがあります。

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


[**BdaCheckChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacheckchanges)

[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))

 

 






