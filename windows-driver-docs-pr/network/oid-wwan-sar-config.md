---
title: OID_WWAN_SAR_CONFIG
description: OID_WWAN_SAR_CONFIG を取得または情報について、モバイル ブロード バンド (MB) デバイスの特定吸収レート (行政区) バックオフ モードとレベルを設定します。
ms.assetid: 78B049E0-A80E-42AA-9D81-D45BBCF84FCB
ms.date: 08/17/2018
keywords: -OID_WWAN_SAR_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bbeb8edcb8140c506cdcedb96d867c0488a35a43
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368254"
---
# <a name="oidwwansarconfig"></a>OID_WWAN_SAR_CONFIG

OID_WWAN_SAR_CONFIG を取得または情報について、モバイル ブロード バンド (MB) デバイスの特定吸収レート (行政区) バックオフ モードとレベルを設定します。 

ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_SAR_CONFIG](ndis-status-wwan-sar-config.md)状態の通知含む、 [ **NDIS_WWAN_SAR_CONFIG_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)行政区の現在の構成を記述する構造体。

この OID のペイロードを含む、一連の要求について、 [ **NDIS_WWAN_SET_SAR_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_config)モデムの新しい SAR 構成を指定する構造体。

## <a name="remarks"></a>注釈

各クエリまたは一連の要求後に、ミニポート ドライバーを返す必要があります、 [ **NDIS_WWAN_SAR_CONFIG_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)モバイル ブロード バンドに関連付けられているデバイス上のすべてのアンテナの情報を含む構造体.

この OID の使用状況に関する詳細については、次を参照してください。 [MBIM_CID_MS_SAR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support#mbimcidmssarconfig)します。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[NDIS_STATUS_WWAN_SAR_CONFIG](ndis-status-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)

[**NDIS_WWAN_SET_SAR_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_config)
