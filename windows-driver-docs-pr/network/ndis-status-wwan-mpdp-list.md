---
title: NDIS_STATUS_WWAN_MPDP_LIST
description: NDIS_STATUS_WWAN_MPDP_LIST 通知は、前の OID_WWAN_MPDP クエリ要求の完了を MB サービスに通知するために、モバイルブロードバンドミニポートドライバーによって送信されます。
ms.assetid: 20D66ECE-A0F8-4902-BC91-3A3D385DA939
keywords:
- NDIS_STATUS_WWAN_MPDP_LIST、Windows Vista 以降のネットワークドライバー
topic_type:
- apiref
api_name:
- NDIS_STATUS_WWAN_MPDP_LIST
api_location:
- ndis.h
api_type:
- HeaderDef
ms.date: 10/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 12f5e9b451c01db66b4e2a6c404704e4c1a28012
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838887"
---
# <a name="ndis_status_wwan_mpdp_list"></a>NDIS_STATUS_WWAN_MPDP_LIST

**NDIS_STATUS_WWAN_MPDP_LIST**通知は、前の[OID_WWAN_MPDP](oid-wwan-mpdp.md)クエリ要求の完了を MB サービスに通知するために、モバイルブロードバンドミニポートドライバーによって送信されます。

この通知は、要請されていないイベントとして送信されません。

この通知では、 [**NDIS_WWAN_MPDP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)構造体が使用されます。

## <a name="requirements"></a>前提条件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン1809 |
| ヘッダー | Ndis. h |
