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
ms.openlocfilehash: 07c78de8a238b97a5a706af8369a529079ab913c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580936"
---
# <a name="guidclasskeyboard"></a>GUID_CLASS_KEYBOARD


GUID_CLASS_KEYBOARD は古い形式の識別子、[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)キーボード デバイス。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_KEYBOARD** ](guid-devinterface-keyboard.md)このクラスの新しいインスタンスのクラス識別子。

<a name="remarks"></a>コメント
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

 

 






