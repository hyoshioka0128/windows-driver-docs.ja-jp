---
title: KSK メソッド\_BDA\_\_トポロジを作成します
description: クライアントは、KSK メソッド\_BDA\_使用して\_トポロジを作成し、フィルター内の既知の接続を反映するトポロジ構造をリング3に作成します。
ms.assetid: 3f34c7cc-d711-478b-a017-ad2c46545a9b
keywords:
- KSMETHOD_BDA_CREATE_TOPOLOGY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_CREATE_TOPOLOGY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72a9609f50607d6922f8f06cef01c095b2494a63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842422"
---
# <a name="ksmethod_bda_create_topology"></a>KSK メソッド\_BDA\_\_トポロジを作成します


クライアントは、KSK メソッド\_BDA\_使用して\_トポロジを作成し、フィルター内の既知の接続を反映するトポロジ構造をリング3に作成します。

## <span id="ddk_ksmethod_bda_create_topology_ks"></span><span id="DDK_KSMETHOD_BDA_CREATE_TOPOLOGY_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>このメソッドの指定

**フラグ**メンバーが ksk メソッドに設定されている ksk メソッド\_TYPE\_WRITE です。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>メソッドデータ

KSMULTIPLE\_ITEM 構造体。これは、トポロジ情報の一覧のヘッダーです。

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


[**BdaMethodCreateTopology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdamethodcreatetopology)

[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))

[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

 

 






