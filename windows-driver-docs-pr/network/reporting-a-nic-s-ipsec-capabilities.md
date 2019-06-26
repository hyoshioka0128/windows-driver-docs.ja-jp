---
title: NIC の IPsec 機能のレポート
description: NIC の IPsec 機能のレポート
ms.assetid: 6ed02d4a-9b5e-4245-a3f9-f0b5fc8366a7
keywords:
- タスクのオフロード WDK TCP/IP トランスポート、IPsec タスク
- IPsec オフロード WDK TCP/IP トランスポート、機能
- IPsec オフロード WDK TCP/IP トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d015fd344ec4e515cf7e67218f4f65f32ebbb54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373275"
---
# <a name="reporting-a-nics-ipsec-capabilities"></a>NIC の IPsec 機能のレポート

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




NDIS ミニポート ドライバーが、インターネット プロトコル セキュリティ (IPsec) オフロードの現在の構成では、NIC を指定します、 [ **NDIS\_IPSEC\_オフロード\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)構造体。ミニポート ドライバーで現在 IPsec オフロードの構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数を[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数を渡す、NDIS 情報\_ミニポート\_アダプター\_オフロード\_属性。

ミニポート ドライバーが存在する場合、変更、IPsec でオフロード機能を報告する必要がありますで、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態を示す値。

クエリに対する応答で[OID\_TCP\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)、NDIS には、NDIS が含まれています\_IPSEC\_オフロード\_V1構造体、 [ **NDIS\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload) NDIS を表す構造体、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

ミニポート ドライバーは、NDIS で次の情報を示す\_IPSEC\_オフロード\_V1 構造体。

-   カプセル化の設定で、**カプセル化**メンバー。 このメンバーの詳細については、「解説」セクションを参照してください。 [ **NDIS\_IPSEC\_オフロード\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)します。

-   NIC が実行できるかどうかを組み合わせて、パケットに IPsec 操作は、NIC は、認証ヘッダー (AH) と、カプセル化セキュリティ ペイロード (ESP) で、次の形式のパケットの両方を含むパケットを処理できるかどうか。

    \[IP\]\[AH\]\[ESP\]\[パケットの残りの部分\]

-   かどうか、NIC は IP セキュリティのトランスポート モードの部分と送信のトンネル モードの部分の両方で処理を実行し、パケットを受信できます。 パケットのトランスポート モードの部分に関連するエンド ツー エンドのセキュリティ アソシエーションとパケットのトンネル モードの部分は、トンネルのセキュリティ アソシエーションに関連します。

-   かどうか、NIC は、パケットの IP ヘッダーには、IP のオプションが含まれている場合、パケット上の IP セキュリティ操作を実行できます。

ミニポート ドライバーでは、AH ペイロードおよび認証情報の暗号化チェックサムを検証 (または計算および検証) または計算の NIC を次の機能を指定します。

-   NIC を使用できる整合性アルゴリズム (MD5 または SHA 1)

-   かどうか、NIC には、AH セキュリティのペイロードを処理できます。
    -   パケットのトランスポート モードの部分
    -   パケットのトンネル モードの部分
    -   パケットを送信します。
    -   パケットを受信します。

ミニポート ドライバーでは、ESP ペイロードを処理する NIC の次の機能を指定します。

-   NIC を使用できる機密性アルゴリズム (DES、triple DES、またはその両方)

-   NIC が null 暗号化 (つまり、ESP ペイロードと認証ハッシュが、暗号化なし) をサポートするかどうか

-   かどうか、NIC には、ESP の処理を実行できます。
    -   パケットのトランスポート モードの部分
    -   パケットのトンネル モードの部分
    -   パケットを送信します。
    -   パケットを受信します。

## <a name="related-topics"></a>関連トピック


[タスクのオフロード機能を判断します。](determining-task-offload-capabilities.md)

 

 






