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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325282"
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
<th>値</th>
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

 

<a name="requirements"></a>必要条件
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

 

 





