---
title: GUID_DEVINTERFACE_KEYBOARD
description: GUID_DEVINTERFACE_KEYBOARD
ms.assetid: ae434c45-07f6-4aa1-b9d3-e4ceca8cc81c
keywords:
- GUID_DEVINTERFACE_KEYBOARD デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_KEYBOARD
api_location:
- Ntddkbd.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2d5c2db5b637df53b94ca267207e29019069dd7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372702"
---
# <a name="guiddevinterfacekeyboard"></a>GUID_DEVINTERFACE_KEYBOARD


GUID_DEVINTERFACE_KEYBOARD[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)キーボード デバイス用に定義されます。

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
<td align="left"><p>GUID_DEVINTERFACE_KEYBOARD</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{884b96c3-56ef-11d1-bc8c-00a0c91405dd}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

キーボード デバイス用のドライバーでは、システムとキーボード デバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

システム提供[キーボード クラス ドライバー](../hid/keyboard-and-mouse-class-drivers.md)キーボード デバイスに対するこのデバイスのインターフェイス クラスのインスタンスを登録します。 キーボード クラス ドライバーでサポートされている I/O インターフェイスを使用してこのデバイスのインターフェイス クラスのインスタンスにアクセスします。

キーボード デバイスのサポートについては、次を参照してください。 [HID アーキテクチャ](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85))と[Kbdclass と Mouclass ドライバーの機能](../hid/keyboard-and-mouse-class-drivers.md)します。

WDK には、システム提供のキーボード クラス ドライバーのサンプル コードが含まれています。 キーボード クラス ドライバーが古い形式の識別子を使用して[ **GUID_CLASS_KEYBOARD** ](guid-class-keyboard.md)のこのインスタンスを登録する[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)します。

マウス デバイスに対するデバイスのインターフェイス クラスについては、次を参照してください。 [ **GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)します。

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
<td align="left">Ntddkbd.h (include Ntddkbd.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_CLASS_KEYBOARD**](guid-class-keyboard.md)

[**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)

 

 






