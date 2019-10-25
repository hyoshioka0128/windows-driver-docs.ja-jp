---
title: フィルターモジュール OID 要求
description: フィルターモジュール OID 要求
ms.assetid: 6de5ec1c-8e12-4f50-8708-ec136cafd9c2
keywords:
- フィルターモジュール WDK ネットワーク, OID 要求
- フィルタードライバー WDK ネットワーク, OID 要求
- NDIS フィルタードライバー WDK、OID 要求
- Oid WDK ネットワーク, フィルタードライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55201de35367dd2b92b525e01b037ec0aff53314
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834681"
---
# <a name="filter-module-oid-requests"></a>フィルターモジュール OID 要求





NDIS は、デバイスの特性、構成可能な設定、統計などの操作パラメーターを含む、アダプターのパラメーターを識別するオブジェクト識別子 (OID) の値を定義します。 Oid の詳細については、「 [NDIS oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

フィルタードライバーは、基になるドライバーの操作パラメーターを照会または設定したり、それ以降のドライバーの OID 要求をフィルター処理したりすることができます。

NDIS では、 [ndis 6.1 以降のフィルタードライバーの直接 OID 要求インターフェイス](direct-oid-request-interface-in-ndis-6-1.md)も提供しています。 *直接 oid 要求パス*は、クエリまたは頻繁に設定される oid 要求をサポートしています。 たとえば、IPsec オフロードバージョン 2 (IPsecv2) インターフェイスでは、 [ipsec\_オフロード\_V2\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa) 、直接 oid 要求の\_SA OID を追加する\_の、TCP\_タスク\_OID が提供されます。 直接 OID 要求インターフェイスは、NDIS ドライバーでは省略可能です。

NDIS 6.81 以降のフィルタードライバーの場合、NDIS は[同期 OID 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)を提供します。 同期*OID 要求パス*では、 [RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) oid などのフィルタードライバーによってキューに登録されていない同期または oid を必要とする oid がサポートされます。 同期 OID 要求インターフェイスは、NDIS ドライバーでは省略可能ですが、フィルタードライバーが RSSv2 のサポートをアドバタイズする場合は必須です。

次のトピックでは、フィルタードライバー OID 要求の詳細について説明します。

[NDIS フィルタードライバーでの OID 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)

[NDIS フィルタードライバーからの OID 要求の生成](generating-oid-requests-from-an-ndis-filter-driver.md)

[フィルターモジュール直接 OID 要求](filter-module-direct-oid-requests.md)

[フィルターモジュールの同期 OID 要求](filter-module-synchronous-oid-requests.md)

 

 





