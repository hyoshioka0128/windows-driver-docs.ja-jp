---
title: ミニポート アダプター OID 要求
description: ミニポート アダプター OID 要求
ms.assetid: c3769b1e-c84a-499d-9f93-17a31441a477
keywords:
- Oid WDK ネットワーク、ミニポートアダプター要求
- ミニポートアダプター WDK ネットワーク、OID 要求
- WDK ネットワークのアダプター、OID 要求
- オブジェクト識別子 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d08ba32725bf073f7640336b582b9bf30c14cc2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844249"
---
# <a name="miniport-adapter-oid-requests"></a>ミニポート アダプター OID 要求





NDIS は、ミニポートアダプターのパラメーターを識別するオブジェクト識別子 (OID) の値を定義します。これには、デバイスの特性、構成可能な設定、統計などの操作パラメーターが含まれます。 Oid の詳細については、「 [NDIS oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

NDIS 6.1 以降のミニポートドライバーの場合、NDIS は[直接 OID 要求インターフェイス](direct-oid-request-interface-in-ndis-6-1.md)を提供します。 *直接 oid 要求パス*は、クエリまたは頻繁に設定される oid 要求をサポートしています。 直接 OID 要求インターフェイスは、NDIS ドライバーでは省略可能です。

NDIS 6.80 以降のミニポートドライバーの場合、NDIS は[同期 OID 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)を提供します。 同期*OID 要求パス*では、 [RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) oid などのフィルタードライバーによってキューに登録されていない同期または oid を必要とする oid がサポートされます。 同期 OID 要求インターフェイスは、NDIS ドライバーでは省略可能ですが、ミニポートドライバーが RSSv2 のサポートをアドバタイズする場合は必須です。

次のトピックでは、ミニポートドライバー OID 要求の詳細について説明します。

[ミニポートアダプターでの OID 要求の処理](handling-oid-requests-in-a-miniport-adapter.md)

[ミニポートアダプター OID 要求のシリアル化](miniport-adapter-oid-request-serialization.md)

[ミニポートアダプターの直接 OID 要求](miniport-adapter-direct-oid-requests.md)

[ミニポートアダプターの同期 OID 要求](miniport-adapter-synchronous-oid-requests.md)
