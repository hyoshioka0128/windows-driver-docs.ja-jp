---
title: 仮想ポートでの受信フィルターのクリア
description: 仮想ポートでの受信フィルターのクリア
ms.assetid: 8431322B-2BF0-4F82-AAAE-0E0396BBC857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a755b2c83118b43cb7e6388c9c1a098f0f7bca8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382772"
---
# <a name="clearing-a-receive-filter-on-a-virtual-port"></a>仮想ポートでの受信フィルターのクリア


オブジェクト識別子 (OID) セット要求を発行している上位のドライバー NIC スイッチ上の仮想ポート (VPort) からの受信フィルターをクリアする[OID\_受信\_フィルター\_オフ\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter). **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_クリア\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)構造体。

ドライバーの問題を遮断する前に、 [OID\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)要求と、それを初期化する必要があります、 [ **NDIS\_受信\_フィルター\_クリア\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)構造体であり、メンバーを次のように設定します。

-   **QueueId** NDIS にメンバーを設定する必要があります\_既定\_受信\_キュー\_id。

-   **FilterId**メンバーは、ドライバーが、以前から取得したフィルター id の値に設定する必要があります[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)メソッド要求の OID。 設定する方法の詳細については、フィルターの受信を参照してください[仮想ポートで受信フィルターを設定](setting-a-receive-filter-on-a-virtual-port.md)します。

上位のドライバーには、すべての VPort を解放する前に、VPort の設定にフィルターを消去する必要があります。 上にある、ドライバーでは、すべてそのバインディングを閉じる前に、VPort の既定の設定またはネットワーク アダプターからデタッチされるフィルターのクリアする必要がありますもします。

 

 





