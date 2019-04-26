---
title: NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_LTE_ATTACH_CONFIG クエリまたは一連の要求の完了を通知するために、NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG 通知を使用します。
ms.assetid: 866BCD4F-85A1-46C8-9FE2-8C5A8ADCD3CA
ms.date: 08/22/2018
keywords: -NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 27af6dd461be18333b12119b7d5d9be8c31f05c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357242"
---
# <a name="ndisstatuswwanlteattachconfig"></a>NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG

ミニポート ドライバーでは、NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG 通知を使用して、モバイル ブロード バンド (MB) サービスに前回の完了に関する通知[OID_WWAN_LTE_ATTACH_CONFIG](oid-wwan-lte-attach-config.md)クエリまたは要求を設定します。

要請されていないイベントは、既定 LTE アタッチする場合無線 (OTA) またはショート メッセージ サービス (SMS) のいずれか、ネットワークによってコンテキストが更新が送信されます。 このケースでは、ミニポート ドライバーが既定値を更新する必要があります LTE がコンテキストにアタッチし、ホスト OS 更新の一覧にこの通知を送信します。

この状態の通知を使用して、 [ **NDIS_WWAN_LTE_ATTACH_CONTEXTS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)構造体。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB LTE アタッチの操作](mb-lte-attach-operations.md)

[OID_WWAN_LTE_ATTACH_CONFIG](oid-wwan-lte-attach-config.md)

[**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)
