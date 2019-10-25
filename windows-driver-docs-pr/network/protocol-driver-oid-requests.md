---
title: プロトコル ドライバー OID 要求
description: プロトコル ドライバー OID 要求
ms.assetid: ab664e75-d17d-4664-8c37-91fd651d23c2
keywords:
- プロトコルドライバー WDK ネットワーク, OID 要求
- Oid WDK ネットワーク, プロトコルドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc74ad8034123b3c7a52378eaf073b17f624b27e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844911"
---
# <a name="protocol-driver-oid-requests"></a>プロトコル ドライバー OID 要求





NDIS は、デバイスの特性、構成可能な設定、統計などの操作パラメーターを含むアダプターパラメーターを識別するために、オブジェクト識別子 (OID) の値を定義します。 Oid の詳細については、「 [NDIS oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

プロトコルドライバーは、基になるドライバーの操作パラメーターを照会または設定できます。

NDIS では、 [ndis 6.1 以降のプロトコルドライバー用の直接 OID 要求インターフェイス](direct-oid-request-interface-in-ndis-6-1.md)も提供しています。 *直接 oid 要求パス*は、クエリまたは頻繁に設定される oid 要求をサポートしています。 たとえば、IPsec オフロードバージョン 2 (IPsecv2) インターフェイスでは、 [ipsec\_オフロード\_V2\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa) 、直接 oid 要求の\_SA OID を追加する\_の、TCP\_タスク\_OID が提供されます。 直接 OID 要求インターフェイスは、NDIS ドライバーでは省略可能です。

次のトピックでは、プロトコルドライバー OID 要求の詳細について説明します。

[NDIS プロトコルドライバーからの OID 要求の生成](generating-oid-requests-from-an-ndis-protocol-driver.md)

[プロトコルドライバーの直接 OID 要求](protocol-driver-direct-oid-requests.md)

[プロトコルドライバー同期 OID 要求](protocol-driver-synchronous-oid-requests.md)

 

 





