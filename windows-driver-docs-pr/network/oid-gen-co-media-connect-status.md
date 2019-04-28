---
title: OID_GEN_CO_MEDIA_CONNECT_STATUS
description: このトピックでは、OID_GEN_CO_MEDIA_CONNECT_STATUS オブジェクト識別子 (OID) について説明します。
ms.assetid: d49ebdfb-1c41-40dc-86bf-01db50a73607
keywords:
- OID_GEN_CO_MEDIA_CONNECT_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: a623db5f5dcd4c07f0ac66ad8953114c8059d36d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379178"
---
# <a name="oidgencomediaconnectstatus"></a>OID_GEN_CO_MEDIA_CONNECT_STATUS

OID_GEN_CO_MEDIA_CONNECT_STATUS OID は、次のシステム定義の値の 1 つとして、ネットワーク上、NIC の接続の状態を返すミニポート ドライバーを要求します。

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

ミニポート ドライバーでは、ネットワーク接続が失われたことを検知、ときに呼び出す必要が[NdisMCoIndicateStatus](https://msdn.microsoft.com/library/windows/hardware/ff563562) NDIS_STATUS_MEDIA_DISCONNECT とします。 接続が復元されると、NDIS_STATUS_MEDIA_CONNECT で NdisMCoIndicateStatus を呼び出すことが必要があります。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

