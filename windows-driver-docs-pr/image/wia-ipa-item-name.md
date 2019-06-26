---
title: WIA\_IPA\_項目\_名
description: WIA\_IPA\_項目\_NAME プロパティには、WIA 項目の名前が含まれています。
ms.assetid: becdd9c6-8202-4c0e-a530-043c1b8421fa
keywords:
- WIA_IPA_ITEM_NAME イメージング デバイス
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
ms.openlocfilehash: 347f435f84c53163bddb27dd7da89c81504edaaa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377312"
---
# <a name="wiaipaitemname"></a>WIA\_IPA\_項目\_名


WIA\_IPA\_項目\_NAME プロパティには、WIA 項目の名前が含まれています。

## <span id="ddk_wia_ipa_item_name_si"></span><span id="DDK_WIA_IPA_ITEM_NAME_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

*項目名*への呼び出しで指定されている項目の名前と同じ、 [ **wiasCreateDrvItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem)サービス ユーティリティ関数。

アプリケーションの読み取り、WIA\_IPA\_項目\_する項目のことを確認する名前プロパティは現在使用されています。 各項目には、一意の名前が必要です。 WIA サービスを作成して維持 WIA\_IPA\_項目\_名。

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
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IWiaMiniDrvTransferCallback::GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream)

[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem)

 

 






