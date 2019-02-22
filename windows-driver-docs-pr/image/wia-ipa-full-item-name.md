---
title: WIA\_IPA\_完全\_項目\_名
description: WIA\_IPA\_完全\_項目\_NAME プロパティには、完全な項目名 (パス情報を含む項目名) が含まれています。
ms.assetid: ba034507-264a-4960-80ab-d5cb0daa5c1a
keywords:
- WIA_IPA_FULL_ITEM_NAME イメージング デバイス
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
ms.openlocfilehash: 7a01404a4936b11b24b3cb40e0b4c28de9aea1ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557378"
---
# <a name="wiaipafullitemname"></a>WIA\_IPA\_完全\_項目\_名


WIA\_IPA\_完全\_項目\_NAME プロパティには、完全な項目名 (パス情報を含む項目名) が含まれています。

## <span id="ddk_wia_ipa_full_item_name_si"></span><span id="DDK_WIA_IPA_FULL_ITEM_NAME_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

*完全な項目名*と同じ、 *bstrFullItemName*のパラメーター、 [ **wiasCreateDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549160)ユーティリティ関数をサービスします。 アプリケーションの読み取り、WIA\_IPA\_完全な\_項目\_する項目のことを確認する名前のプロパティが現在使用して、WIA 項目のツリーでそのアイテムはどこにあります。 各項目には、一意の名前を必要があります。 通常、アプリケーションは、WIA 項目のツリー内の項目を検索する完全な項目の名前を使用します。 WIA サービスを作成して維持 WIA\_IPA\_完全\_項目\_名。

アプリケーションは、WIA を読み取ります\_IPA\_完全\_項目\_まもなく受信するには、イメージの形式を特定の名前。 アプリケーションでは、書式を設定するには、このプロパティを書き込みます。 WIA\_IPA\_完全\_項目\_名前によって異なります、 [ **WIA\_IPA\_TYMED** ](wia-ipa-tymed.md)プロパティ。 WIA ミニドライバーを作成し、維持 WIA\_IPA\_完全\_項目\_名。

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
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IWiaMiniDrvTransferCallback::GetNextStream**](https://msdn.microsoft.com/library/windows/hardware/jj151551)

[**WIA\_IPA\_TYMED**](wia-ipa-tymed.md)

[**wiasCreateDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549160)

 

 






