---
title: OID_TCP_TASK_IPSEC_ADD_UDPESP_SA
description: このトピックでは、OID_TCP_TASK_IPSEC_ADD_UDPESP_SA オブジェクト識別子 (OID) について説明します。
ms.assetid: 022db6dd-1099-4069-81af-7f919d91464e
keywords:
- OID_TCP_TASK_IPSEC_ADD_UDPESP_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bb8cc120c20030db5a6cb06b6661c7edf745f45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386954"
---
# <a name="oidtcptaskipsecaddudpespsa"></a>OID_TCP_TASK_IPSEC_ADD_UDPESP_SA

トランスポート プロトコル設定 OID_TCP_TASK_IPSEC_ADD_UDPESP_SA ESP の UDP カプセル化パケットを NIC に 1 つまたは複数のセキュリティ アソシエーション (Sa) を追加するミニポート ドライバーを要求するには

各 SA の情報として書式設定、 [OFFLOAD_IPSEC_ADD_UDPESP_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_offload_ipsec_add_udpesp_sa)構造体。 この構造体とほぼ同じことに注意してください、 [OFFLOAD_IPSEC_ADD_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_offload_ipsec_add_sa)で使用される構造、 [OID_TCP_TASK_IPSEC_ADD_SA](oid-tcp-task-ipsec-add-sa.md)要求。 唯一の違いは OFFLOAD_IPSEC_ADD_UDPESP_SA 構造が含まれている、 **EncapTypeEntry**と**EncapTypeEntryOffldHandle**メンバー。

OFFLOAD_IPSEC_ADD_UDPESP_SA 構造体の最初の 7 つのメンバー (**SrcAddr**、**注釈**、 **DestAddr**、 **DestMask**、 **プロトコル**、**任意**、および**DestPort**)、ソースと変換先、だけでなく、SAs を適用する、IP プロトコルを指定するフィルターを構成します。 このフィルターは、2 つのホスト間で、エンド ツー エンド接続は、- トランスポート モード接続に関連します。 トンネルのソースおよび宛先のアドレスがで指定されたトンネルを通じて指定された接続が行われた場合**SrcTunnelAddr**と**DestTunnelAddr**、それぞれします。

Filter パラメーターが 0 に設定されている場合、指定された SAs のパケットをフィルター処理するパラメーターは使用されません。 たとえば場合、 **SrcAddr** 0 の場合、指定された SAs に設定されている任意のソース アドレスを含むパケットに適用できます。 実行するはすべてのフィルター パラメーターがゼロに設定されている場合など、極端な場合に、指定された SAs は、任意の宛先ホストに任意の種類のパケットを送信する任意のソース ホストに適用されます。

TCP/IP トランスポートは、IP プロトコルを指定できます、**プロトコル**メンバーを示す、指定された SAs が指定したプロトコルの種類のパケットにのみ適用されます。 場合**プロトコル**0 の場合、指定された SAs に設定されている、指定したソースから指定したコピー先に送信されるすべてのパケットに適用されます。

## <a name="offloadsecurityassociation-structure"></a>OFFLOAD_SECURITY_ASSOCIATION 構造体

[OFFLOAD_SECURITY_ASSOCIATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_offload_security_association)構造体が 1 つのセキュリティ アソシエーション (SA) を指定します。 OFFLOAD_SECURITY_ASSOCIATION 構造内の要素は、 **SecAssoc**可変長の配列。 **SecAssoc** 1 つまたは 2 つの OFFLOAD_SECURITY_ASSOCIATION 構造が含まれています。

認証ヘッダー (AH) の処理に使用しての操作の種類を指定することを指定された SA**認証**であり、 **IntegrityAlgo** (整合性アルゴリズム)。 SA はありませんが、 **ConfAlgo** (機密性アルゴリズム)。 この場合、 **ConfAlgo**はゼロを含みます。

操作の種類を指定することがカプセル化セキュリティ ペイロード (Esp) の処理に使用して指定された SA **ENCRYPT**とがあります、 **IntegrityAlgo** (整合性アルゴリズム) および**ConfAlgo** (機密性アルゴリズム)。

## <a name="offloadalgoinfo-structure"></a>OFFLOAD_ALGO_INFO 構造体

[OFFLOAD_ALGO_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_offload_algo_info)メンバーである構造体の[OFFLOAD_SECURITY_ASSOCIATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_offload_security_association)構造体をセキュリティ アソシエーション (SA) を使用するアルゴリズムを指定します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

