---
title: NDIS_STATUS_WWAN_MPDP_STATE
description: MB サービスに以前 OID_WWAN_MPDP セットの要求の完了を通知するためにモバイル ブロード バンド ミニポート ドライバーによって NDIS_STATUS_WWAN_MPDP_STATE 通知が送信されます。
ms.assetid: 59B8D9A0-FB22-4252-A24B-A9E58B068C4E
keywords:
- NDIS_STATUS_WWAN_MPDP_STATE、ネットワーク ドライバーが Windows Vista 以降
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
ms.openlocfilehash: f756200c7f49dbcf77a24e2f72903f58570a40bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369895"
---
# <a name="ndisstatuswwanmpdpstate"></a>NDIS_STATUS_WWAN_MPDP_STATE

**NDIS_STATUS_WWAN_MPDP_STATE** MB サービスに前回の完了を通知するためにモバイル ブロード バンド ミニポート ドライバーによって通知が送信される[OID_WWAN_MPDP](oid-wwan-mpdp.md)セットの要求。

この通知は、要請していないイベントとしては送信されません。

この通知を使用して、 [ **NDIS_WWAN_MPDP_STATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)構造体。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1809 |
| Header | Ndis.h |
