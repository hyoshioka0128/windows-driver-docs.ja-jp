---
title: KSMETHOD\_BDA\_コミット\_の変更
description: クライアントを使用して、KSMETHOD\_BDA\_コミット\_の一覧をコミットする変更は、変更を要求します。
ms.assetid: f6572a4e-2328-4157-80f7-110e0fe58a4f
keywords:
- KSMETHOD_BDA_COMMIT_CHANGES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_COMMIT_CHANGES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eee13b9cb218b938f96e2f3f9ac384fc16ef9b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376910"
---
# <a name="ksmethodbdacommitchanges"></a>KSMETHOD\_BDA\_コミット\_の変更


クライアントを使用して、KSMETHOD\_BDA\_コミット\_の一覧をコミットする変更は、変更を要求します。

## <span id="ddk_ksmethod_bda_commit_changes_ks"></span><span id="DDK_KSMETHOD_BDA_COMMIT_CHANGES_KS"></span>


### <a name="span-idspecifyingthismethodspanspan-idspecifyingthismethodspanspan-idspecifyingthismethodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>この方法を指定します。

KSMETHOD**フラグ**メンバーに KSMETHOD 設定\_型\_NONE。

### <a name="span-idmethoddataspanspan-idmethoddataspanspan-idmethoddataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>メソッドのデータ

なし

<a name="remarks"></a>注釈
-------

ネットワーク プロバイダーが、KSMETHOD をにより、\_BDA\_コミット\_変更要求、変更の一覧は、基になるフィルターでコミットされた、この時点で、フィルターには、その状態がリセットされます。 新しいサイクルを開始できます。

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


[**BdaCommitChanges**](https://msdn.microsoft.com/library/windows/hardware/ff556435)

[**KSMETHOD**](https://msdn.microsoft.com/library/windows/hardware/ff563398)

 

 






