---
title: WIA\_IPA\_完全\_項目\_名
description: WIA\_IPA\_FULL\_ITEM\_NAME プロパティには、完全な項目名 (項目名とパス情報) が含まれています。
ms.assetid: ba034507-264a-4960-80ab-d5cb0daa5c1a
keywords:
- WIA_IPA_FULL_ITEM_NAME イメージングデバイス
topic_type:
- apiref
api_name:
- WIA_IPA_FULL_ITEM_NAME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce543f670529d6e89f384eea3411826ad7504d61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840697"
---
# <a name="wia_ipa_full_item_name"></a>WIA\_IPA\_完全\_項目\_名


WIA\_IPA\_FULL\_ITEM\_NAME プロパティには、完全な項目名 (項目名とパス情報) が含まれています。

## <span id="ddk_wia_ipa_full_item_name_si"></span><span id="DDK_WIA_IPA_FULL_ITEM_NAME_SI"></span>


プロパティの型: VT\_BSTR

有効な値: WIA\_PROP\_NONE

アクセス権: 読み取り専用

<a name="remarks"></a>注釈
-------

*完全な項目名*は、 [**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem) Service ユーティリティ関数の*bstrFullItemName*パラメーターと同じです。 アプリケーションは、WIA\_IPA\_完全な\_項目\_NAME プロパティを読み取って、現在使用している項目と、その項目が WIA 項目ツリー内のどこにあるかを判断します。 各項目には一意の名前を付ける必要があります。 アプリケーションでは、通常、完全な項目名を使用して、WIA 項目ツリー内の項目を検索します。 WIA サービスは、WIA\_IPA\_完全\_項目\_名を作成し、管理します。

アプリケーションは、WIA\_IPA\_完全\_項目\_名を読み取り、受信するイメージの形式を決定します。 アプリケーションは、このプロパティを書き込み、形式を設定します。 WIA\_IPA\_FULL\_ITEM\_NAME は、 [**wia\_IPA\_TYMED**](wia-ipa-tymed.md)プロパティに依存します。 WIA ミニドライバーは、WIA\_IPA\_完全\_項目\_名を作成して管理します。

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

[**WIA\_IPA\_TYMED**](wia-ipa-tymed.md)

[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)

 

 






