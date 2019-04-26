---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA
description: TCP/IP トランスポートは、セットとして、ミニポート ドライバーが NIC に指定されたセキュリティ アソシエーション (Sa) を更新することを要求する OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA OID を使用してください。
ms.assetid: 22849103-9148-4621-b78f-b9f34f2c7ac1
ms.date: 08/08/2017
keywords: -OID_TCP_TASK_IPSEC_OFFLOAD_V2_UPDATE_SA ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e841825a7b13c740cbf979088ee2ba9e06d4d0bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350912"
---
# <a name="oidtcptaskipsecoffloadv2updatesa"></a>OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_UPDATE\_SA


\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]

TCP/IP トランスポートが、OID を使用して、セットとして\_TCP\_タスク\_IPSEC\_オフロード\_V2\_更新\_SA OID ミニポート ドライバーが、指定したセキュリティを更新することを要求するにはNIC のアソシエーション (Sa)

**注**  NDIS OID 要求インターフェイスを直接この OID をサポートしています。 直接の OID 要求インターフェイスの詳細については、次を参照してください。 [NDIS 6.1 Direct OID 要求インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff564736)します。

 

<a name="remarks"></a>注釈
-------

IPsec をサポートするすべての NDIS 6.1 ミニポート ドライバーでは、バージョン 2 (IPsecOV2) は、この OID をサポートする必要がありますをオフロードします。

ミニポート ドライバーでは、この要求を受信したときに、ドライバーが NIC で指定された SAs を更新する必要があります。 ミニポート ドライバーが、SA が見つからないか、ESN はサポートされていない場合、この要求が失敗することができます。 この場合、返されるステータスは NDIS をする必要があります\_状態\_無効な\_パラメーター。

ミニポート ドライバーが、受信、 [ **IPSEC\_オフロード\_V2\_更新\_SA** ](https://msdn.microsoft.com/library/windows/hardware/ff556990)更新プログラムに関する情報を含む構造体と、[次へ] の IPSEC へのポインター\_オフロード\_V2\_UPDATE\_リンク リストで SA 構造体。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.1 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IPSEC\_オフロード\_V2\_UPDATE\_SA**](https://msdn.microsoft.com/library/windows/hardware/ff556990)

 

 




