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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356001"
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

WDM を指定する方法については[関数ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff546516) ACPI デバイスでは、次を参照してください。 [ACPI のデバイスをサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff536161)します。

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

 

 





