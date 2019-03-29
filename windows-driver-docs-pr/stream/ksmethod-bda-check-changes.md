---
title: KSMETHOD\_BDA\_確認\_の変更
description: クライアントを使用して、KSMETHOD\_BDA\_確認\_変更要求された変更の一覧は作業になっているかどうかを判別します。
ms.assetid: 00a2d0ca-0ede-4ae5-ab2a-95d19143ea7c
keywords:
- KSMETHOD_BDA_CHECK_CHANGES ストリーミング メディア デバイス
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
ms.openlocfilehash: e0bd12054bc7370d39965d9f34323f6c0e588956
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578381"
---
# <a name="ksmethodbdacheckchanges"></a>KSMETHOD\_BDA\_確認\_の変更


クライアントを使用して、KSMETHOD\_BDA\_確認\_変更要求された変更の一覧は作業になっているかどうかを判別します。

## <span id="ddk_ksmethod_bda_check_changes_ks"></span><span id="DDK_KSMETHOD_BDA_CHECK_CHANGES_KS"></span>


### <a name="span-idspecifyingthismethodspanspan-idspecifyingthismethodspanspan-idspecifyingthismethodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>この方法を指定します。

KSMETHOD**フラグ**メンバーに KSMETHOD 設定\_型\_NONE。

### <a name="span-idmethoddataspanspan-idmethoddataspanspan-idmethoddataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>メソッドのデータ

なし

<a name="remarks"></a>コメント
-------

変更の一覧をコミットする前に、ネットワーク プロバイダーを KSMETHOD\_BDA\_確認\_要求された変更が作業になっているかどうかを判別要求を変更します。 ミニドライバーは、リソースが使用できることを保証するために、この要求が行われたときにリソースを確保することができます。

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


[**BdaCheckChanges**](https://msdn.microsoft.com/library/windows/hardware/ff556433)

[**KSMETHOD**](https://msdn.microsoft.com/library/windows/hardware/ff563398)

 

 






