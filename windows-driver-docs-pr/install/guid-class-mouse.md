---
title: GUID_CLASS_MOUSE
description: GUID_CLASS_MOUSE
ms.assetid: 3b6578c7-0462-4fff-bd09-b9c768676ceb
keywords:
- GUID_CLASS_MOUSE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_CLASS_MOUSE
api_location:
- Ntddmou.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da83a0bb1fa8cc162be74dc1869c60023b9109cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378046"
---
# <a name="guidclassmouse"></a>GUID_CLASS_MOUSE


GUID_CLASS_MOUSE は古い形式の識別子、[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)マウス デバイス。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_MOUSE** ](guid-devinterface-mouse.md)このクラスの新しいインスタンスのクラス識別子。

<a name="remarks"></a>注釈
-------

WDK に用意されている HID サンプルには、マウス クラス ドライバーが含まれます。 マウスのクラス ドライバーは GUID_CLASS_MOUSE を使用して、このデバイスのインターフェイス クラスのインスタンスを登録します。

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
<td align="left"><p>使われていません。 Windows 2000 以降、GUID_DEVINTERFACE_MOUSE を代わりに使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddmou.h (Ntddmou.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)

 

 






