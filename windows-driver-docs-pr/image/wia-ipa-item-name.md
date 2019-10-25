---
title: WIA\_IPA\_項目\_名
description: WIA\_IPA\_ITEM\_NAME プロパティには、WIA 項目の名前が含まれています。
ms.assetid: becdd9c6-8202-4c0e-a530-043c1b8421fa
keywords:
- WIA_IPA_ITEM_NAME イメージングデバイス
topic_type:
- apiref
api_name:
- WIA_IPA_ITEM_NAME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3676bed9c12651fecb2fcc29a7036417951814e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840691"
---
# <a name="wia_ipa_item_name"></a>WIA\_IPA\_項目\_名


WIA\_IPA\_ITEM\_NAME プロパティには、WIA 項目の名前が含まれています。

## <span id="ddk_wia_ipa_item_name_si"></span><span id="DDK_WIA_IPA_ITEM_NAME_SI"></span>


プロパティの型: VT\_BSTR

有効な値: WIA\_PROP\_NONE

アクセス権: 読み取り専用

<a name="remarks"></a>注釈
-------

*項目名*は、 [**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem) service ユーティリティ関数の呼び出しで指定されている項目名と同じです。

アプリケーションは、WIA\_IPA\_ITEM\_NAME プロパティを読み取って、現在どの項目を使用しているかを判断します。 各項目には一意の名前を付ける必要があります。 WIA サービスは、WIA\_IPA\_項目\_名を作成し、管理します。

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
<td>Wiadef (Wiadef を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IWiaMiniDrvTransferCallback:: GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream)

[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)

 

 






