---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX
description: TCP/IP トランスポートは、セットとして、ミニポート ドライバーが NIC に指定されたセキュリティ アソシエーション (Sa) を追加することを要求する OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX OID を使用してください。
ms.assetid: 9D356CFA-3353-4E62-9B1C-0FF650DCE75C
ms.date: 08/08/2017
keywords: -OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bd82ea83e066e7e5aaf1c468a4bab99f6cc01526
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580019"
---
# <a name="oidtcptaskipsecoffloadv2addsaex"></a>OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA\_例


\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]

TCP/IP トランスポートが、OID を使用して、セットとして\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA\_ミニポート ドライバーの追加を要求する例: OID、NIC に指定されたセキュリティ アソシエーション (Sa)

**注**  NDIS OID 要求インターフェイスを直接この OID をサポートしています。 直接の OID 要求インターフェイスの詳細については、次を参照してください。 [NDIS 6.1 Direct OID 要求インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff564736)します。

 

<a name="remarks"></a>コメント
-------

IPsec をサポートするすべての NDIS 6.30 ミニポート ドライバーでは、バージョン 2 (IPsecOV2) は、この OID をサポートする必要がありますをオフロードします。

TCP/IP トランスポートは、NIC が IPsecOV2 操作を実行できることを判断、TCP/IP トランスポートは、SAs を追加するミニポート ドライバーを要求します。 トランスポートは、トランスポートは、SA を追加する前に、NIC に IPsecOV2 操作をオフロードことはできません。

ミニポート ドライバーでは、SAs の処理 IPsecOV2 の NIC を構成します。 OID に正常に設定されている\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA\_EX、ミニポート ドライバーが識別するハンドルを提供しますSA をオフロード、 **OffloadHandle**のメンバー、 [ **IPSEC\_オフロード\_V2\_追加\_SA\_EX**](https://msdn.microsoft.com/library/windows/hardware/hh463943)構造体。 (たとえば、トランスポート ハンドルを使用して、送信パスで SA を使用してをオフロードすることを示します)。 SA はオフロードされたセットの要求が成功した場合。

ミニポート ドライバーを返せる OID 要求は、エラー状態など、NIC の複数の SAs をオフロードする容量が不足している場合。 また、ミニポート ドライバーは、競合状態を回避する必要があるために、エラー状態を返す可能性があります。 この場合は、NIC の構成が変更され、特定のアルゴリズムは含まれません。

要求が失敗した場合、SAs がオフロードできません。 ミニポート ドライバーを設定する必要があります、SA の障害が発生した場合、 **OffloadHandle**メンバーに対応する IPSEC\_オフロード\_V2\_追加\_SA\_EX 構造体**NULL**します。

SAs でサポートできる NIC の最大数を報告するミニポート ドライバー、 **SaOffloadCapacity**のメンバー、 [ **NDIS\_IPSEC\_オフロード\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff565808)初期化中に構造体。 かどうか、必要に応じて TCP/IP トランスポート設定できる、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)を要求する OIDミニポート ドライバー、SA を NIC から削除します。

この OID が以前のバージョンでは、実質的に同じ[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](oid-tcp-task-ipsec-offload-v2-add-sa.md)します。 唯一の違いは、更新された[ **IPSEC\_オフロード\_V2\_追加\_SA\_EX** ](https://msdn.microsoft.com/library/windows/hardware/hh463943)構造体。

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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IPSEC\_オフロード\_V2\_追加\_SA\_例**](https://msdn.microsoft.com/library/windows/hardware/hh463943)

[**NDIS\_IPSEC\_オフロード\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff565808)

[OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA](oid-tcp-task-ipsec-offload-v2-add-sa.md)

[OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_DELETE\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)

 

 




