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
ms.openlocfilehash: a726e74ca35d381bceeac0fa9eb74a6748cdedda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388783"
---
# <a name="wiaipaitemname"></a>WIA\_IPA\_項目\_名


WIA\_IPA\_項目\_NAME プロパティには、WIA 項目の名前が含まれています。

## <span id="ddk_wia_ipa_item_name_si"></span><span id="DDK_WIA_IPA_ITEM_NAME_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

*項目名*への呼び出しで指定されている項目の名前と同じ、 [ **wiasCreateDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549160)サービス ユーティリティ関数。

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


[**IWiaMiniDrvTransferCallback::GetNextStream**](https://msdn.microsoft.com/library/windows/hardware/jj151551)

[**wiasCreateDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549160)

 

 






