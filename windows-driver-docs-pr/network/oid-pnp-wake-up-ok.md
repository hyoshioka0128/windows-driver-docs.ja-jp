---
title: OID_PNP_WAKE_UP_OK
description: OID_PNP_WAKE_UP_OK
ms.assetid: 93389bfe-11b9-4433-8eca-4446f05d01c0
ms.date: 08/08/2017
keywords: -OID_PNP_WAKE_UP_OK ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ff15bbc04b762a40323f52d90a05394572ca840a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581031"
---
# <a name="oidpnpwakeupok"></a>OID\_PNP\_WAKE\_を\_OK





省略可能な OID\_PNP\_WAKE\_を\_OK OID は、ミニポート ドライバーの NIC がシグナル状態になる有効なのウェイク アップの数を示します 有効なウェイク アップには、NIC が有効なパターン一致またはマジック パケットに応答してでシステムをスリープ解除時に発生します。

この OID のデータ型は、ULONG 値です。

上端がこの OID 要求を受信する中間のドライバーは、Ndis (Co) 要求を呼び出すことによって、基になるミニポート ドライバーに要求を伝達する必要があります常にします。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 5.1、および NDIS 6.0 以降がサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

 

 




