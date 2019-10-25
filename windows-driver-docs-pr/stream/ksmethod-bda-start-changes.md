---
title: KSK メソッド\_BDA\_\_の変更を開始します
description: クライアントは、\_BDA メソッドを使用して、変更リストをリセットするための変更\_開始\_開始します。
ms.assetid: 657fb89d-f216-4352-87d8-3d2d933cc8a5
keywords:
- KSMETHOD_BDA_START_CHANGES ストリーミングメディアデバイス
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
ms.openlocfilehash: 8d056b527c1d60447cfd2fe01514c46d0bc4b757
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842416"
---
# <a name="ksmethod_bda_start_changes"></a>KSK メソッド\_BDA\_\_の変更を開始します


クライアントは、\_BDA メソッドを使用して、変更リストをリセットするための変更\_開始\_開始します。

## <span id="ddk_ksmethod_bda_start_changes_ks"></span><span id="DDK_KSMETHOD_BDA_START_CHANGES_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>このメソッドの指定

**フラグ**メンバーが ksk メソッドに設定されている ksk メソッド\_型\_NONE。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>メソッドデータ

なし

<a name="remarks"></a>注釈
-------

ネットワークプロバイダーが変更を開始する前に、KSK メソッド\_BDA\_開始\_変更要求によって開始されます。これによって、コミットされていない既存の変更リストが破棄され、フィルターのピンとノードに対して保持が開始されます。新しい変更のセットを追跡します。 次に、ネットワークプロバイダーは、フィルターまたはそのピンで必要なインターフェイスメソッドを呼び出しますが、メソッドは実際には呼び出されません。 ネットワークプロバイダーによって変更が動作しないと判断された場合、このメソッドを呼び出して一覧をクリアできます。

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


[**BdaStartChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdastartchanges)

[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))

 

 






