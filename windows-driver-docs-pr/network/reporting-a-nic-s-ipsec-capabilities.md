---
title: NIC の IPsec 機能のレポート
description: NIC の IPsec 機能のレポート
ms.assetid: 6ed02d4a-9b5e-4245-a3f9-f0b5fc8366a7
keywords:
- タスクオフロード WDK TCP/IP トランスポート、IPsec タスク
- IPsec オフロード WDK TCP/IP トランスポート、機能
- IPsec オフロード WDK TCP/IP トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 156a121ab89f450c6ecf169cd618ab63f761e232
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842058"
---
# <a name="reporting-a-nics-ipsec-capabilities"></a>NIC の IPsec 機能のレポート

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




NDIS ミニポートドライバーは、 [**ndis\_ipsec\_オフロード\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)構造の NIC の NIC の現在のインターネットプロトコルセキュリティ (ipsec) オフロード構成を指定します。ミニポートドライバーには、 [**NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)構造の現在の IPsec オフロード構成が含まれている必要があります。 ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、NDIS\_ミニポート\_アダプター\_オフロード\_属性の情報を渡します。

ミニポートドライバーでは、 [**NDIS\_status\_タスク\_オフロード\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状態の表示で、IPsec オフロード機能の変更を報告する必要があります。

[現在の\_CONFIG\_の OID\_TCP\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)のクエリに応答して、ndis では、ndis によって返される NDIS\_[**オフ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)ロード構造に、NDIS\_IPSEC\_オフロード\_V1 構造が含まれています。[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバー。 NDIS は、ミニポートドライバーによって提供された情報を使用します。

ミニポートドライバーは、NDIS\_IPSEC\_オフロード\_V1 構造体の次の情報を示します。

-   カプセル化の設定 (**カプセル化**メンバー内)。 このメンバーの詳細については、「 [**NDIS\_IPSEC\_OFFLOAD\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)」の「解説」セクションを参照してください。

-   NIC がパケットに対して IPsec 操作を組み合わせて実行できるかどうか。つまり、NIC が、次の形式のパケットに認証ヘッダー (AH) とカプセル化セキュリティペイロード (ESP) の両方を含むパケットを処理できるかどうかを示します。

    \[IP\]\[AH\]\[ESP\]\[パケットの残り\]

-   送信パケットと受信パケットの両方で、NIC がトランスポートモード部分とトンネルモード部分の両方で IP セキュリティ処理を実行できるかどうか。 パケットのトランスポートモード部分は、エンドツーエンドのセキュリティアソシエーションに関連し、パケットのトンネルモード部分はトンネルセキュリティの関連付けに関連します。

-   パケットの IP ヘッダーに IP オプションが含まれている場合に、NIC がパケットに対して IP セキュリティ操作を実行できるかどうか。

ミニポートドライバーは、AH ペイロードと認証情報の暗号化されたチェックサムを計算または検証 (または計算および検証) する NIC の次の機能を指定します。

-   NIC が使用できる整合性アルゴリズム (MD5 または SHA 1)

-   NIC が次の場合に AH セキュリティペイロードを処理できるかどうか。
    -   パケットのトランスポートモード部分
    -   パケットのトンネルモード部分
    -   パケットの送信
    -   パケットの受信

ミニポートドライバーは、ESP ペイロードを処理するために、NIC の次の機能を指定します。

-   NIC が使用できる機密性アルゴリズム (DES、トリプル DES、またはその両方)

-   NIC が null 暗号化をサポートしているかどうか (つまり、暗号化されていないが認証ハッシュを使用する ESP ペイロード)

-   NIC が次の場合に ESP 処理を実行できるかどうか。
    -   パケットのトランスポートモード部分
    -   パケットのトンネルモード部分
    -   パケットの送信
    -   パケットの受信

## <a name="related-topics"></a>関連トピック


[タスクオフロード機能の決定](determining-task-offload-capabilities.md)

 

 






