---
title: GUID_DEVICE_LID
description: GUID_DEVICE_LID
ms.assetid: e879b1bf-3f5f-4b6d-956b-006091377194
keywords:
- GUID_DEVICE_LID デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVICE_LID
api_location:
- Poclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: afbd859844c1483beb7b30cf5b09475309acaf4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370983"
---
# <a name="guiddevicelid"></a>GUID_DEVICE_LID


GUID_DEVICE_LID[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)Advanced Configuration and Power Interface (ACPI) カバー デバイス用に定義されます。

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
<td align="left"><p>GUID_DEVICE_LID</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{4AFA3D52-74A7-11d0-be5e-00A0C9062857}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

システム提供[ACPI ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)オペレーティング システムと ACPI カバーのデバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

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

 

 





