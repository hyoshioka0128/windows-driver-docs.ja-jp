---
title: OID_GEN_HARDWARE_STATUS
description: クエリとして OID_GEN_HARDWARE_STATUS OID は基になる NIC の現在のハードウェアの状態を指定します
ms.assetid: beab6f7a-b064-446f-8008-ef8db9d7c080
ms.date: 08/08/2017
keywords: -OID_GEN_HARDWARE_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: de190f8dd238d047a9ccc9653321edd9b439df5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381346"
---
# <a name="oidgenhardwarestatus"></a>OID\_GEN\_ハードウェア\_状態


クエリ、OID として\_GEN\_ハードウェア\_状態 OID を基になる NIC の現在のハードウェアの状態を指定します

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
使われていません。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

OID\_GEN\_ハードウェア\_状態 OID NDIS が次の 1 つとして、基になる NIC の現在のハードウェアの状態を指定する\_ハードウェア\_状態型の値。

<a href="" id="ndishardwarestatusready"></a>**NdisHardwareStatusReady**  
使用可能で、ネットワーク経由でデータを送受信できます。

<a href="" id="ndishardwarestatusinitializing"></a>**NdisHardwareStatusInitializing**  
初期化

<a href="" id="ndishardwarestatusreset"></a>**NdisHardwareStatusReset**  
リセットします。

<a href="" id="ndishardwarestatusclosing"></a>**NdisHardwareStatusClosing**  
閉じる

<a href="" id="ndishardwarestatusnotready"></a>**NdisHardwareStatusNotReady**  
準備ができていません

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

 

 




