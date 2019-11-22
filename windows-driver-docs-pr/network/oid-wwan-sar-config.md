---
title: OID_WWAN_SAR_CONFIG
description: OID_WWAN_SAR_CONFIG、モバイルブロードバンド (MB) デバイスの特定の吸収率 (SAR) のバックオフモードとレベルに関する情報を取得または設定します。
ms.assetid: 78B049E0-A80E-42AA-9D81-D45BBCF84FCB
ms.date: 08/17/2018
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_SAR_CONFIG
ms.localizationpriority: medium
ms.openlocfilehash: 6154a4915f092a476710aa8d3162a55318d6ad56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843797"
---
# <a name="oid_wwan_sar_config"></a>OID_WWAN_SAR_CONFIG

OID_WWAN_SAR_CONFIG、モバイルブロードバンド (MB) デバイスの特定の吸収率 (SAR) のバックオフモードとレベルに関する情報を取得または設定します。 

ミニポートドライバーは、クエリ要求を非同期的に処理し、その後、現在の SAR 構成を記述する[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)構造を含む[NDIS_STATUS_WWAN_SAR_CONFIG](ndis-status-wwan-sar-config.md)状態通知を送信する前に、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に返す必要があります。

セット要求の場合、この OID のペイロードには、モデムの新しい SAR 構成を指定する[**NDIS_WWAN_SET_SAR_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_config)構造が含まれます。

## <a name="remarks"></a>注釈

各クエリまたは設定要求の後に、ミニポートドライバーは、モバイルブロードバンドに関連付けられているデバイス上のすべてのアンテナに関する情報を含む[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)構造を返します。

この OID の使用方法の詳細については、「 [MBIM_CID_MS_SAR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support#mbimcidmssarconfig)」を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[NDIS_STATUS_WWAN_SAR_CONFIG](ndis-status-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)

[**NDIS_WWAN_SET_SAR_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_config)
