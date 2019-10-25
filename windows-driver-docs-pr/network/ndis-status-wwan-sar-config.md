---
title: NDIS_STATUS_WWAN_SAR_CONFIG
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SAR_CONFIG 通知を使用して、以前の OID_WWAN_SAR_CONFIG クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 50DAEFAB-E86A-41EA-A237-802AD8F83BB2
ms.date: 08/17/2018
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_SAR_CONFIG ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 09b31cf9ef011bbaa71a340529df1f6ec0a68203
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844647"
---
# <a name="ndis_status_wwan_sar_config"></a>NDIS_STATUS_WWAN_SAR_CONFIG

ミニポートドライバーは、 **NDIS_STATUS_WWAN_SAR_CONFIG**通知を使用して、以前の[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。

要請されていないイベントは適用できません。

この通知では、 [**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)構造体が使用されます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1703 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)
