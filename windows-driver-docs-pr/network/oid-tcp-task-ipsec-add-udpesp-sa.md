---
title: OID_TCP_TASK_IPSEC_ADD_UDPESP_SA
description: このトピックでは、OID_TCP_TASK_IPSEC_ADD_UDPESP_SA オブジェクト識別子 (OID) について説明します。
ms.assetid: 022db6dd-1099-4069-81af-7f919d91464e
keywords:
- OID_TCP_TASK_IPSEC_ADD_UDPESP_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9f043615b7b57c66d2541fb26e5e33e3e90f536
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843895"
---
# <a name="oid_tcp_task_ipsec_add_udpesp_sa"></a>OID_TCP_TASK_IPSEC_ADD_UDPESP_SA

トランスポートプロトコルは、UDP カプセル化された ESP パケットの1つ以上のセキュリティアソシエーション (SAs) を NIC に追加するようにミニポートドライバーを要求するように、OID_TCP_TASK_IPSEC_ADD_UDPESP_SA を設定します。

各 SA の情報は、 [OFFLOAD_IPSEC_ADD_UDPESP_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_ipsec_add_udpesp_sa)構造体として書式設定されます。 この構造体は、 [OID_TCP_TASK_IPSEC_ADD_SA](oid-tcp-task-ipsec-add-sa.md)要求で使用される[OFFLOAD_IPSEC_ADD_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_ipsec_add_sa)構造体とほぼ同じであることに注意してください。 唯一の違いは、OFFLOAD_IPSEC_ADD_UDPESP_SA 構造体には**Encaptypeentry**と**Encaptypeentryoffldhandle**メンバーが含まれていることです。

OFFLOAD_IPSEC_ADD_UDPESP_SA 構造体の最初の7つのメンバー (**Srcaddr**、 **SrcMask**、 **destaddr**、 **destaddr**、 **Protocol**、 **srcaddr**、および**destaddr**) は、SAs が適用されるソースと宛先、および IP プロトコル。 このフィルターは、トランスポートモード接続 (つまり、2つのホスト間のエンドツーエンド接続) に関連しています。 指定された接続がトンネルを介して確立される場合、トンネルの送信元アドレスと宛先アドレスは、それぞれ**SrcTunnelAddr**と**DestTunnelAddr**によって指定されます。

フィルターパラメーターが0に設定されている場合、そのパラメーターは、指定された SAs のパケットをフィルター処理するために使用されません。 たとえば、 **Srcaddr**が0に設定されている場合、指定された SAs は任意の発信元アドレスを含むパケットに適用できます。 これを極端なものにするために、すべてのフィルターパラメーターがゼロに設定されている場合、指定された SAs は任意の種類のパケットを任意の送信先ホストに送信するすべてのソースホストに適用されます。

TCP/IP トランスポートは、指定された SAs が指定されたプロトコルの種類のパケットにのみ適用されることを示すために、**プロトコル**メンバーに ip プロトコルを指定できます。 **Protocol**が0に設定されている場合、指定された SAs は、指定された転送元から指定された宛先に送信されるすべてのパケットに適用されます。

## <a name="offload_security_association-structure"></a>OFFLOAD_SECURITY_ASSOCIATION 構造体

[OFFLOAD_SECURITY_ASSOCIATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_security_association)構造体は、1つのセキュリティアソシエーション (SA) を指定します。 OFFLOAD_SECURITY_ASSOCIATION 構造体は、 **Secassoc**可変長配列内の要素です。 **Secassoc**には、1つまたは2つの OFFLOAD_SECURITY_ASSOCIATION 構造体が含まれています。

認証ヘッダー (AH) の処理に使用するように指定された SA は、**操作の種類**が authentication で、 **IntegrityAlgo** (整合性アルゴリズム) が設定されます。 SA には、 **ConfAlgo** (機密性アルゴリズム) はありません。 この場合、 **ConfAlgo**にはゼロが含まれます。

カプセル化セキュリティペイロード (ESPs) で使用するように指定された SA は、操作の種類が**ENCRYPT**であり、 **IntegrityAlgo** (整合性アルゴリズム) または**ConfAlgo** (機密性アルゴリズム) がある場合があります。

## <a name="offload_algo_info-structure"></a>OFFLOAD_ALGO_INFO 構造体

[OFFLOAD_SECURITY_ASSOCIATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_security_association)構造体のメンバーである[OFFLOAD_ALGO_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_algo_info)構造体は、セキュリティアソシエーション (SA) に使用されるアルゴリズムを指定します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

