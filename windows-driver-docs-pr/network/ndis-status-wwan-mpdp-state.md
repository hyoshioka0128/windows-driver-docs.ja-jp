---
title: NDIS_STATUS_WWAN_MPDP_STATE
description: NDIS_STATUS_WWAN_MPDP_STATE 通知は、前の OID_WWAN_MPDP セット要求の完了を MB サービスに通知するために、モバイルブロードバンドミニポートドライバーによって送信されます。
ms.assetid: 59B8D9A0-FB22-4252-A24B-A9E58B068C4E
keywords:
- NDIS_STATUS_WWAN_MPDP_STATE、Windows Vista 以降のネットワークドライバー
topic_type:
- apiref
api_name:
- NDIS_STATUS_WWAN_MPDP_STATE
api_location:
- ndis.h
api_type:
- HeaderDef
ms.date: 10/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8004b4d1d8e1f5387d99a824f701d0172472f38d
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968535"
---
# <a name="ndis_status_wwan_mpdp_state"></a>NDIS_STATUS_WWAN_MPDP_STATE

**NDIS_STATUS_WWAN_MPDP_STATE**通知は、前の[OID_WWAN_MPDP](oid-wwan-mpdp.md)セット要求の完了を MB サービスに通知するために、モバイルブロードバンドミニポートドライバーによって送信されます。

この通知は、要請されていないイベントとして送信されません。

この通知では、 [**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)構造を使用します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン1809

**ヘッダー**: Ndis. h

