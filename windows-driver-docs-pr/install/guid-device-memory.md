---
title: GUID_DEVICE_MEMORY
description: GUID_DEVICE_MEMORY
ms.assetid: 8351585d-6538-41aa-891a-b7c1e0b75cef
keywords:
- GUID_DEVICE_MEMORY デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVICE_MEMORY
api_location:
- Poclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0f16e4bc030dc09e5e0270e14a569b50f5ccc93c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379350"
---
# <a name="guiddevicememory"></a>GUID_DEVICE_MEMORY


GUID_DEVICE_MEMORY[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)Advanced Configuration and Power Interface (ACPI) のメモリ デバイスが定義されています。

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
<td align="left"><p>GUID_DEVICE_MEMORY</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{3FD0F03D-92E0-45FB-B75C-5ED8FFB01021}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

システム提供[ACPI ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)オペレーティング システムと ACPI メモリ デバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

WDM を指定する方法については[関数ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers) ACPI デバイスでは、次を参照してください。 [ACPI のデバイスをサポートしている](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-acpi-devices)します。

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

 

 





