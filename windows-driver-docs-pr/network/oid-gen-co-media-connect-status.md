---
title: OID_GEN_CO_MEDIA_CONNECT_STATUS
description: このトピックでは、OID_GEN_CO_MEDIA_CONNECT_STATUS オブジェクト識別子 (OID) について説明します。
ms.assetid: d49ebdfb-1c41-40dc-86bf-01db50a73607
keywords:
- OID_GEN_CO_MEDIA_CONNECT_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c88cda4dc1b2dd3b438c6ff73b4ae18e05e8fc43
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361176"
---
# <a name="oidgencomediaconnectstatus"></a>OID_GEN_CO_MEDIA_CONNECT_STATUS

OID_GEN_CO_MEDIA_CONNECT_STATUS OID は、次のシステム定義の値の 1 つとして、ネットワーク上、NIC の接続の状態を返すミニポート ドライバーを要求します。

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

ミニポート ドライバーでは、ネットワーク接続が失われたことを検知、ときに呼び出す必要が[NdisMCoIndicateStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex) NDIS_STATUS_MEDIA_DISCONNECT とします。 接続が復元されると、NDIS_STATUS_MEDIA_CONNECT で NdisMCoIndicateStatus を呼び出すことが必要があります。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

