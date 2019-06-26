---
title: VMQ フィルターのクリア
description: VMQ フィルターのクリア
ms.assetid: 34efeb28-dcd6-4a8b-89d2-6065830e03ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcbd3b5d390aad74ea176d6e3acec983706506cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385535"
---
# <a name="clearing-a-vmq-filter"></a>VMQ フィルターのクリア





上にある、ドライバーの問題を受信キューにフィルターを解放する、 [OID\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter) OID 要求のセット。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_クリア\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)構造体。

プロトコル ドライバーでは、フィルターの識別子を取得、以前から[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)メソッド要求の OID。 フィルターの設定の詳細については、次を参照してください。 [VMQ フィルター設定](setting-a-vmq-filter.md)します。

プロトコル ドライバーには、設定されると、キューを解放する前に、キューのすべてのフィルターをクリアする必要があります。 プロトコル ドライバーも設定されると、ネットワーク アダプターには、そのバインドが閉じる前に、既定のキューのすべてのフィルターをオフにする必要があります。

OID が完了しなかった場合、ミニポート ドライバーは既定以外のキューでパケットを示していませんする必要があります\_受信\_フィルター\_オフ\_フィルター OID 要求キューの最後のフィルターをクリアまたは、が完了したかどうか[OID\_受信\_フィルター\_FREE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue) OID 要求キューを解放します。

 

 





