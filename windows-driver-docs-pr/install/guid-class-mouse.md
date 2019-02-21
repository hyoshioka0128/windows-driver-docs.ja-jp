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
ms.openlocfilehash: f0bbd499bd7af241e178e0c6ef055aecc6a854ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528484"
---
# <a name="guidclassmouse"></a>GUID_CLASS_MOUSE


GUID_CLASS_MOUSE は古い形式の識別子、[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)マウス デバイス。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_MOUSE** ](guid-devinterface-mouse.md)このクラスの新しいインスタンスのクラス識別子。

<a name="remarks"></a>注釈
-------

WDK に用意されている HID サンプルには、マウス クラス ドライバーが含まれます。 マウスのクラス ドライバーは GUID_CLASS_MOUSE を使用して、このデバイスのインターフェイス クラスのインスタンスを登録します。

<a name="requirements"></a>要件
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

 

 






