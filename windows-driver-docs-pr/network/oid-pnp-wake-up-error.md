---
title: OID_PNP_WAKE_UP_ERROR
description: OID_PNP_WAKE_UP_ERROR
ms.assetid: e6386a35-7077-45b3-bc0c-164477168a55
ms.date: 08/08/2017
keywords: -OID_PNP_WAKE_UP_ERROR ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 49e020892478c0c86c55a916ce53e836801b8bd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569696"
---
# <a name="oidpnpwakeuperror"></a>OID\_PNP\_WAKE\_を\_エラー





省略可能な OID\_PNP\_WAKE\_を\_エラー OID は、ミニポート ドライバーのネットワーク アダプターによって通知が false のウェイク アップ ups の数を示します。 False のウェイク アップには、ネットワーク アダプターが正しくない場合にシステムをスリープ解除時に発生します。 たとえば、ネットワーク アダプターでした誤ってウェイク アップ、不正確なパターン マッチによりシステム。

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

 

 




