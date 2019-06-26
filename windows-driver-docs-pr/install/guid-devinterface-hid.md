---
title: GUID_DEVINTERFACE_HID
description: GUID_DEVINTERFACE_HID
ms.assetid: af2ebdaf-b7e9-4f79-abb6-60f1fb954b55
keywords:
- GUID_DEVINTERFACE_HID デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_HID
api_location:
- Hidclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 78668560a88fb8e926544e28471b559f485cb120
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391542"
---
# <a name="guiddevinterfacehid"></a>GUID_DEVINTERFACE_HID


GUID_DEVINTERFACE_HID[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている[HID コレクション](https://docs.microsoft.com/windows-hardware/drivers/hid/hid-collections)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>GUID_DEVINTERFACE_HID</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{4D1E55B2-F16F-11CF-88CB-001111000030}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

HID コレクション用のドライバーでは、オペレーティング システムと HID コレクションの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

システム提供[HID クラス ドライバー](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85)) HID コレクションにこのデバイスのインターフェイス クラスのインスタンスを登録します。 たとえば、HID クラス ドライバーは、USB キーボードまたはマウス デバイスのインターフェイスを登録します。 HID クラス ドライバーでサポートされている I/O インターフェイスを使用して、HID コレクションへのアクセスします。

HID デバイスとドライバーについては、次を参照してください。 [HIDClass デバイス](../hid/binding-minidrivers-to-the-hid-class.md)します。

キーボード デバイスに対するデバイスのインターフェイス クラスについては、次を参照してください。 [ **GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)します。

マウス デバイスに対するデバイスのインターフェイス クラスについては、次を参照してください。 [ **GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)します。

[ **GUID_CLASS_INPUT** ](guid-class-input.md)このデバイスの古い形式の識別子は、インターフェイス クラス。 GUID_DEVINTERFACE_HID を代わりに使用します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Hidclass.h (Hidclass.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_CLASS_INPUT**](guid-class-input.md)

[**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)

[**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)

 

 






