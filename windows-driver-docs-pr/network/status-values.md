---
title: 状態の値
description: 状態の値
ms.assetid: 1d5cce4a-9830-4e2e-af90-fc1fecfb0fc9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60af504f094a74bee4c1a5b59f6235b6e5b9ecf2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340920"
---
# <a name="status-values"></a>状態の値





リモートの NDIS 状態値はで、Microsoft Windows 2000 Driver Development Kit (DDK) が定義されている 32 ビットの状態の値とほぼ同等です。 この仕様で使用される特定のリモート NDIS 状態値が以下に示す、他のユーザーは、Windows 2000 DDK またはオンライン ドキュメントから推論することができます。 デバイスは、意味的に正しくリモート NDIS 状態値を返す可能性があります、*状態*生成されるメッセージのフィールド。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態の識別子</th>
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_SUCCESS</p></td>
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>成功</p></td>
</tr>
<tr class="even">
<td align="left"><p>RNDIS_STATUS_FAILURE</p></td>
<td align="left"><p>0xC00000001</p></td>
<td align="left"><p>特定できないエラー (STATUS_UNSUCCESSFUL に相当)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_INVALID_DATA</p></td>
<td align="left"><p>0xC0010015</p></td>
<td align="left"><p>無効なデータのエラー</p></td>
</tr>
<tr class="even">
<td align="left"><p>RNDIS_STATUS_NOT_SUPPORTED</p></td>
<td align="left"><p>0xC00000BB</p></td>
<td align="left"><p>サポートされていない要求エラー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_MEDIA_CONNECT</p></td>
<td align="left"><p>0x4001000B</p></td>
<td align="left"><p>ネットワーク メディア (Windows 2000 DDK から NDIS_STATUS_MEDIA_CONNECT と同じ) にデバイスが接続されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RNDIS_STATUS_MEDIA_DISCONNECT</p></td>
<td align="left"><p>0x4001000C</p></td>
<td align="left"><p>デバイスがネットワークのメディア (Windows 2000 DDK から NDIS_STATUS_MEDIA_DISCONNECT と同じ) から切断されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RNDIS_STATUS_Xxx</p></td>
<td align="left"><p>...</p></td>
<td align="left"><p>Windows 2000 DDK またはオンライン ドキュメントで定義された NDIS_STATUS_Xxx 値に等しい</p></td>
</tr>
</tbody>
</table>

 

 

 





