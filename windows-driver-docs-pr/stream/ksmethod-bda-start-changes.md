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
ms.openlocfilehash: 6b8fda6b76d06d3b2ee71e4455814f2b5cc2be63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578382"
---
# <a name="ksmethodbdastartchanges"></a>KSMETHOD\_BDA\_開始\_の変更


クライアントを使用して、KSMETHOD\_BDA\_開始\_変更リストをリセットする変更。

## <span id="ddk_ksmethod_bda_start_changes_ks"></span><span id="DDK_KSMETHOD_BDA_START_CHANGES_KS"></span>


### <a name="span-idspecifyingthismethodspanspan-idspecifyingthismethodspanspan-idspecifyingthismethodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>この方法を指定します。

KSMETHOD**フラグ**メンバーに KSMETHOD 設定\_型\_NONE。

### <a name="span-idmethoddataspanspan-idmethoddataspanspan-idmethoddataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>メソッドのデータ

なし

<a name="remarks"></a>コメント
-------

変更を加えるネットワーク プロバイダーが開始する前に、KSMETHOD になります\_BDA\_開始\_変更要求は、破棄されるコミットされていない既存の変更一覧を原因し、フィルターのピンに通知し、一連の変更の追跡を開始するノード。 ネットワーク プロバイダーは、フィルターやその pin に必要なインターフェイス メソッドを呼び出しますが、メソッドが実際に呼び出されないまだ。 任意の時点では、ネットワーク プロバイダーは、変更は動作しないことを判断した場合は、リストをクリアするには、このメソッドを呼び出すことができます。

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


[**BdaStartChanges**](https://msdn.microsoft.com/library/windows/hardware/ff556507)

[**KSMETHOD**](https://msdn.microsoft.com/library/windows/hardware/ff563398)

 

 






