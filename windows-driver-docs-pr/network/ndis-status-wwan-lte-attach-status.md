---
title: NDIS_STATUS_WWAN_LTE_ATTACH_STATUS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 通知を使用して、以前の OID_WWAN_LTE_ATTACH_STATUS クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 8A40437E-7AAC-4829-A032-0B8C933A7AC0
ms.date: 08/23/2018
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_LTE_ATTACH_STATUS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: a4537cd67001823e7d99551b5114668de0fcd915
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843279"
---
# <a name="ndis_status_wwan_lte_attach_status"></a>NDIS_STATUS_WWAN_LTE_ATTACH_STATUS

ミニポートドライバーは、NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 通知を使用して、以前の[OID_WWAN_LTE_ATTACH_STATUS](oid-wwan-lte-attach-status.md)クエリ要求の完了をモバイルブロードバンド (MB) サービスに通知します。

割り当てられていないイベントは、LTE attach のコンテキストがアクティブになっている場合に送信されます。たとえば、SIM が挿入された場合などです。 この場合、ミニポートドライバーは、ホスト OS にこの通知を送信する必要があります。

この状態通知では、 [**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)構造体が使用されます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1703 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB LTE アタッチ操作](mb-lte-attach-operations.md)

[OID_WWAN_LTE_ATTACH_STATUS](oid-wwan-lte-attach-status.md)

[**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)
