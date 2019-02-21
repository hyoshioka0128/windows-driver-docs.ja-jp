---
title: WIA\_DPA\_CONNECT\_状態
description: WIA\_DPA\_CONNECT\_STATUS プロパティには、デバイスの現在の接続状態が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 524fb89a-47a0-44a7-8f21-36e0abcfdd5c
keywords:
- WIA_DPA_CONNECT_STATUS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPA_CONNECT_STATUS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1f078ced043e3662b24ddfc7a896938aecea40e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528593"
---
# <a name="wiadpaconnectstatus"></a>WIA\_DPA\_CONNECT\_状態


WIA\_DPA\_CONNECT\_STATUS プロパティには、デバイスの現在の接続状態が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dpa_connect_status_si"></span><span id="DDK_WIA_DPA_CONNECT_STATUS_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

次の表では、使用可能な値を示します、wia\_DPA\_CONNECT\_STATUS プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DEVICE_NOT_CONNECTED</p></td>
<td><p>デバイスが接続されていません。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DEVICE_CONNECTED</p></td>
<td><p>デバイスは、接続されていると運用面です。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





