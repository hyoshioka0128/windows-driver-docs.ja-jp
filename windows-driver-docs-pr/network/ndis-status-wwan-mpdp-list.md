---
title: NDIS_STATUS_WWAN_MPDP_LIST
description: MB サービスに前回 OID_WWAN_MPDP クエリ要求の完了を通知するためにモバイル ブロード バンド ミニポート ドライバーによって NDIS_STATUS_WWAN_MPDP_LIST 通知が送信されます。
ms.assetid: 20D66ECE-A0F8-4902-BC91-3A3D385DA939
keywords:
- NDIS_STATUS_WWAN_MPDP_LIST、ネットワーク ドライバーが Windows Vista 以降
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
ms.openlocfilehash: e1ac1879c8ea04b76c8947aaf8f24ab03a9c6501
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580092"
---
# <a name="ndisstatuswwanmpdplist"></a>NDIS_STATUS_WWAN_MPDP_LIST

**NDIS_STATUS_WWAN_MPDP_LIST** MB サービスに前回の完了を通知するためにモバイル ブロード バンド ミニポート ドライバーによって通知が送信される[OID_WWAN_MPDP](oid-wwan-mpdp.md)クエリ要求。

この通知は、要請していないイベントとしては送信されません。

この通知を使用して、 [ **NDIS_WWAN_MPDP_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)構造体。

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1809 |
| Header | Ndis.h |
