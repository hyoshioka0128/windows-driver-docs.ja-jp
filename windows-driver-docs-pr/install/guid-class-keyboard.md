---
title: GUID_CLASS_KEYBOARD
description: GUID_CLASS_KEYBOARD
ms.assetid: 9e90d18f-5298-4234-8b05-38e9b8ec5076
keywords:
- GUID_CLASS_KEYBOARD デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_CLASS_KEYBOARD
api_location:
- Ntddkbd.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 22a86c01144dd0df3df5471bfd9809cc490702a8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373510"
---
# <a name="guidclasskeyboard"></a>GUID_CLASS_KEYBOARD


GUID_CLASS_KEYBOARD は古い形式の識別子、[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)キーボード デバイス。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_KEYBOARD** ](guid-devinterface-keyboard.md)このクラスの新しいインスタンスのクラス識別子。

<a name="remarks"></a>注釈
-------

WDK に用意されている HID サンプルには、キーボード クラス ドライバーが含まれています。 キーボード クラス ドライバーは GUID_CLASS_KEYBOARD を使用して、このデバイスのインターフェイス クラスのインスタンスを登録します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>使われていません。 Windows 2000 以降、GUID_DEVINTERFACE_KEYBOARD を代わりに使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddkbd.h (include Ntddkbd.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)

 

 






