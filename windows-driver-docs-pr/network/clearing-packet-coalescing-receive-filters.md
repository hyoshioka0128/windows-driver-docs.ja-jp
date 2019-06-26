---
title: パケット結合受信フィルターのクリア
description: パケット結合受信フィルターのクリア
ms.assetid: 0924A494-AA4E-45FA-AFE6-65E0D105E0F2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f831576d7bdd6f02a84e60a69b89e2e53d869d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385524"
---
# <a name="clearing-packet-coalescing-receive-filters"></a>パケット結合受信フィルターのクリア


を解放するまたは*オフ*、パケットの結合をサポートしているミニポート ドライバーに対する受信フィルター、上位のドライバーがの OID セット要求を発行する[OID\_受信\_フィルター\_オフ\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_クリア\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)構造体。

プロトコルまたはフィルター ドライバーなど、上にあるドライバーを初期化します、 [ **NDIS\_受信\_フィルター\_クリア\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)構造体次のように

-   **QueueId** NDIS にメンバーを設定する必要があります\_既定\_受信\_キュー\_id。

    **注**  NDIS 6.30 以降では、フィルターが受信パケットの結合は、既定でのみサポートの受信ネットワーク アダプターのキュー。 この受信キューが識別子の NDIS\_既定\_受信\_キュー\_id。

     

-   **FilterId**メンバーする必要がありますを設定する、0 以外の識別子 (ID)、ミニポート ドライバーにクリアするフィルターの値。 上にあるドライバーの以前の OID メソッド要求から、フィルター ID を取得した[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)または[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。

    **注**  だけで受信のフィルターをパケットの結合セット上にあるドライバーがオフにします。

     

**注**  上位プロトコルまたはフィルター ドライバーがすべての基になるミニポート ドライバーの設定にフィルターを受信パケットの結合をクリアする必要があります、バインドの解除を完了するか、操作をデタッチする前にします。

 

 

 





