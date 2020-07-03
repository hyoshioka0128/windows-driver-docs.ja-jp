---
title: NDIS_STATUS_WWAN_LTE_ATTACH_STATUS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 通知を使用して、前の OID_WWAN_LTE_ATTACH_STATUS クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 8A40437E-7AAC-4829-A032-0B8C933A7AC0
ms.date: 08/23/2018
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_LTE_ATTACH_STATUS
ms.localizationpriority: medium
ms.openlocfilehash: 8e6255dea6605710f1a2cd49637505dae6e1572f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916157"
---
# <a name="ndis_status_wwan_lte_attach_status"></a>NDIS_STATUS_WWAN_LTE_ATTACH_STATUS

ミニポートドライバーは、NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 通知を使用して、前の[OID_WWAN_LTE_ATTACH_STATUS](oid-wwan-lte-attach-status.md)クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。

割り当てられていないイベントは、LTE attach のコンテキストがアクティブになっている場合に送信されます。たとえば、SIM が挿入された場合などです。 この場合、ミニポートドライバーは、ホスト OS にこの通知を送信する必要があります。

この状態通知では、 [**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)構造が使用されます。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1703**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB LTE アタッチ操作](mb-lte-attach-operations.md)

[OID_WWAN_LTE_ATTACH_STATUS](oid-wwan-lte-attach-status.md)

[**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)
