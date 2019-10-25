---
title: NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG
description: ミニポートドライバーは、NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG 通知を使用して、以前の OID_WWAN_LTE_ATTACH_CONFIG クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 866BCD4F-85A1-46C8-9FE2-8C5A8ADCD3CA
ms.date: 08/22/2018
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 770716891d1830866ce122869cf8c5adb81134ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843023"
---
# <a name="ndis_status_wwan_lte_attach_config"></a>NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG

ミニポートドライバーは、NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG 通知を使用して、以前の[OID_WWAN_LTE_ATTACH_CONFIG](oid-wwan-lte-attach-config.md)クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。

既定の LTE アタッチコンテキストが無線またはショートメッセージサービス (SMS) のいずれかでネットワークによって更新された場合、要請されていないイベントが送信されます。 この場合、ミニポートドライバーは、既定の LTE アタッチコンテキストを更新し、更新された一覧を使用してこの通知をホスト OS に送信する必要があります。

この状態通知では、 [**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)構造体が使用されます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1703 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB LTE アタッチ操作](mb-lte-attach-operations.md)

[OID_WWAN_LTE_ATTACH_CONFIG](oid-wwan-lte-attach-config.md)

[**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)
