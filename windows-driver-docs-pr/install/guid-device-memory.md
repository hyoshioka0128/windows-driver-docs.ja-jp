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
ms.openlocfilehash: 4ef020f21adbbaf01b4b96ba0c3c62b433c7a01c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572150"
---
# <a name="guiddevicememory"></a>GUID_DEVICE_MEMORY


GUID_DEVICE_MEMORY[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)Advanced Configuration and Power Interface (ACPI) のメモリ デバイスが定義されています。

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

システム提供[ACPI ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540493)オペレーティング システムと ACPI メモリ デバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

WDM を指定する方法については[関数ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff546516) ACPI デバイスでは、[ACPI のデバイスをサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff536161)を参照してください。

<a name="requirements"></a>必要条件
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

 

 





