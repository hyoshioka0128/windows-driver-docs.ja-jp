---
title: GUID_DEVINTERFACE_MOUSE
description: GUID_DEVINTERFACE_MOUSE
ms.assetid: c5aff960-a78d-4429-ba3f-f2f91d9a56fa
keywords:
- GUID_DEVINTERFACE_MOUSE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_MOUSE
api_location:
- Ntddmou.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5fa3bb8af6d7171074c8a235a4d59621cfcb7789
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538793"
---
# <a name="guiddevinterfacemouse"></a>GUID_DEVINTERFACE_MOUSE


GUID_DEVINTERFACE_MOUSE[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)マウス デバイス用に定義されます。

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
<td align="left"><p>GUID_DEVINTERFACE_MOUSE</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{378DE44C-56EF-11D1-BC8C-00A0C91405DD}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

マウス デバイスのドライバーでは、オペレーティング システムとマウス デバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

システム提供[マウス クラス ドライバー](../hid/keyboard-and-mouse-class-drivers.md)マウス デバイスにこのデバイスのインターフェイス クラスのインスタンスを登録します。 マウスのクラス ドライバーでサポートされる I/O インターフェイスを使用してこのデバイスのインターフェイス クラスのインスタンスにアクセスします。

マウス デバイスのサポートについては、次を参照してください。 [HID アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/jj126193)と[Kbdclass と Mouclass ドライバーの機能](../hid/keyboard-and-mouse-class-drivers.md)します。

WDK には、システム提供のマウス クラス ドライバーのサンプル コードが含まれています。 マウスのクラス ドライバーが古い形式の識別子を使用して[ **GUID_CLASS_MOUSE** ](guid-class-mouse.md)のこのインスタンスを登録する[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

キーボード デバイスに対するデバイスのインターフェイス クラスについては、次を参照してください。 [ **GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)します。

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
<td align="left"><p>Microsoft Windows 2000 および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddmou.h (Ntddmou.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_CLASS_MOUSE**](guid-class-mouse.md)

[**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)

 

 






