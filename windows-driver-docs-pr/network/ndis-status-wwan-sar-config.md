---
title: NDIS_STATUS_WWAN_SAR_CONFIG
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SAR_CONFIG 通知を使用して、以前の OID_WWAN_SAR_CONFIG クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 50DAEFAB-E86A-41EA-A237-802AD8F83BB2
ms.date: 08/17/2018
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_SAR_CONFIG
ms.localizationpriority: medium
ms.openlocfilehash: 7118d8e8050b4d1a12a7e919fd0d81bf15ca2ce2
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918018"
---
# <a name="ndis_status_wwan_sar_config"></a>NDIS_STATUS_WWAN_SAR_CONFIG

ミニポートドライバーは、 **NDIS_STATUS_WWAN_SAR_CONFIG**通知を使用して、以前の[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。

要請されていないイベントは適用できません。

この通知では、 [**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)構造を使用します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1703**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)
