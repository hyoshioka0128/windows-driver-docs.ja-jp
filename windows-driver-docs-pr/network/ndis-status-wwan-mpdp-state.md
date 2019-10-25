---
title: NDIS_STATUS_WWAN_MPDP_STATE
description: NDIS_STATUS_WWAN_MPDP_STATE 通知は、前の OID_WWAN_MPDP set 要求の完了を MB サービスに通知するために、モバイルブロードバンドミニポートドライバーによって送信されます。
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
ms.openlocfilehash: 0da96368e5e2fe387663ed50ac754ee0f6e0ced4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844669"
---
# <a name="ndis_status_wwan_mpdp_state"></a>NDIS_STATUS_WWAN_MPDP_STATE

**NDIS_STATUS_WWAN_MPDP_STATE**通知は、前の[OID_WWAN_MPDP](oid-wwan-mpdp.md) set 要求の完了を MB サービスに通知するために、モバイルブロードバンドミニポートドライバーによって送信されます。

この通知は、要請されていないイベントとして送信されません。

この通知では、 [**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)構造体が使用されます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1809 |
| Header | Ndis. h |
