---
title: KSMETHOD\_BDA\_開始\_の変更
description: クライアントを使用して、KSMETHOD\_BDA\_開始\_変更リストをリセットする変更。
ms.assetid: 657fb89d-f216-4352-87d8-3d2d933cc8a5
keywords:
- KSMETHOD_BDA_START_CHANGES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_START_CHANGES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48610f58ce6d345e0b0c676e198ec75630b5067e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370394"
---
# <a name="ksmethodbdastartchanges"></a>KSMETHOD\_BDA\_開始\_の変更


クライアントを使用して、KSMETHOD\_BDA\_開始\_変更リストをリセットする変更。

## <span id="ddk_ksmethod_bda_start_changes_ks"></span><span id="DDK_KSMETHOD_BDA_START_CHANGES_KS"></span>


### <a name="span-idspecifyingthismethodspanspan-idspecifyingthismethodspanspan-idspecifyingthismethodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>この方法を指定します。

KSMETHOD**フラグ**メンバーに KSMETHOD 設定\_型\_NONE。

### <a name="span-idmethoddataspanspan-idmethoddataspanspan-idmethoddataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>メソッドのデータ

なし

<a name="remarks"></a>注釈
-------

変更を加えるネットワーク プロバイダーが開始する前に、KSMETHOD になります\_BDA\_開始\_変更要求は、破棄されるコミットされていない既存の変更一覧を原因し、フィルターのピンに通知し、一連の変更の追跡を開始するノード。 ネットワーク プロバイダーは、フィルターやその pin に必要なインターフェイス メソッドを呼び出しますが、メソッドが実際に呼び出されないまだ。 任意の時点では、ネットワーク プロバイダーは、変更は動作しないことを判断した場合は、リストをクリアするには、このメソッドを呼び出すことができます。

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


[**BdaStartChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdastartchanges)

[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))

 

 






