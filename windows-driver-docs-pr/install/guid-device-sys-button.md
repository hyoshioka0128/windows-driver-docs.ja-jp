---
title: GUID_DEVICE_SYS_BUTTON
description: GUID_DEVICE_SYS_BUTTON
ms.assetid: 6d07e015-3ea5-4951-ab2d-9c110edef1c5
keywords:
- GUID_DEVICE_SYS_BUTTON デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVICE_SYS_BUTTON
api_location:
- Poclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 202548d462b4a72dfedc52f7e2ee7fe25cbc2468
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370964"
---
# <a name="guiddevicesysbutton"></a>GUID_DEVICE_SYS_BUTTON


GUID_DEVICE_SYS_BUTTON[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)Advanced Configuration and Power Interface (ACPI) のシステムの電源ボタン デバイスに対して定義されています。

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
<td align="left"><p>GUID_DEVICE_SYS_BUTTON</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{4AFA3D53-74A7-11d0-be5e-00A0C9062857}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

システム提供[ACPI ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)オペレーティング システムとシステムの電源ボタンのデバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。 I8042prt、PS/2 形式のキーボードとマウス デバイス、システム提供のドライバーには、キーボードの場合、システムの電源ボタンをサポートするには、このクラスのインスタンスも登録します。

WDM を指定する方法については[関数ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers) ACPI デバイスでは、次を参照してください。 [ACPI のデバイスをサポートしている](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-acpi-devices)します。

PS/2 形式のキーボードとマウス デバイスについては、次を参照してください。[非 HIDClass キーボードとマウス デバイス](../hid/keyboard-and-mouse-class-drivers.md)します。

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
<td align="left">Poclass.h (Poclass.h を含む)</td>
</tr>
</tbody>
</table>

 

 





