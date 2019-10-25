---
title: KSK メソッド\_BDA\_コミット\_の変更
description: クライアントは、KSK メソッド\_BDA\_コミット\_変更を使用して、要求された変更の一覧をコミットします。
ms.assetid: f6572a4e-2328-4157-80f7-110e0fe58a4f
keywords:
- KSMETHOD_BDA_COMMIT_CHANGES ストリーミングメディアデバイス
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
ms.openlocfilehash: ab1034a16c59a519b7d45fffad1fdd8220674eca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842426"
---
# <a name="ksmethod_bda_commit_changes"></a>KSK メソッド\_BDA\_コミット\_の変更


クライアントは、KSK メソッド\_BDA\_コミット\_変更を使用して、要求された変更の一覧をコミットします。

## <span id="ddk_ksmethod_bda_commit_changes_ks"></span><span id="DDK_KSMETHOD_BDA_COMMIT_CHANGES_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>このメソッドの指定

**フラグ**メンバーが ksk メソッドに設定されている ksk メソッド\_型\_NONE。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>メソッドデータ

なし

<a name="remarks"></a>注釈
-------

ネットワークプロバイダーが KSK メソッド\_BDA\_コミット\_変更要求を行うと、基になるフィルターで変更の一覧がコミットされます。この時点で、フィルターは状態をリセットし、新しいサイクルを開始できます。

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


[**BdaCommitChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacommitchanges)

[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))

 

 






