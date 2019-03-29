---
title: NDIS_STATUS_WWAN_SAR_CONFIG
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_SAR_CONFIG クエリまたは一連の要求の完了を通知するために、NDIS_STATUS_WWAN_SAR_CONFIG 通知を使用します。
ms.assetid: 50DAEFAB-E86A-41EA-A237-802AD8F83BB2
ms.date: 08/17/2018
keywords: -NDIS_STATUS_WWAN_SAR_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5c4932270c9831ef9ecfd379c04e2278f1200db0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580095"
---
# <a name="ndisstatuswwansarconfig"></a>NDIS_STATUS_WWAN_SAR_CONFIG

ミニポート ドライバーを使用して、 **NDIS_STATUS_WWAN_SAR_CONFIG**モバイル ブロード バンド (MB) のサービスに前回の完了を通知するために通知[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)クエリまたは要求を設定します。

要請されていないイベントは適用されません。

この通知を使用して、 [ **NDIS_WWAN_SAR_CONFIG_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)構造体。

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)
