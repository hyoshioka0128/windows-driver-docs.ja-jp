---
title: フィルター モジュール OID 要求
description: フィルター モジュール OID 要求
ms.assetid: 6de5ec1c-8e12-4f50-8708-ec136cafd9c2
keywords:
- フィルター モジュールの WDK ネットワーク、OID 要求
- フィルター ドライバー WDK ネットワーク、OID 要求
- NDIS フィルター ドライバー WDK、OID 要求
- Oid WDK ネットワー キング、フィルター ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6790c6a0d69d52131f50747b0ab3e800d1fed5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363405"
---
# <a name="filter-module-oid-requests"></a>フィルター モジュール OID 要求





NDIS は、アダプターのパラメーターは、デバイスの特性、構成可能な設定、および統計情報などのパラメーターを含めるを識別するためにオブジェクト識別子 (OID) の値を定義します。 Oid の詳細については、次を参照してください。 [NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

フィルター ドライバーは、クエリまたは基になるドライバーの動作のパラメーターを設定またはドライバーを後続の OID 要求をフィルター処理できます。

NDIS も用意されています。、 [NDIS 6.1 の OID 要求インターフェイスを直接](direct-oid-request-interface-in-ndis-6-1.md)とドライバーを後でフィルター処理します。 *OID の直接の要求パス*クエリを実行したり、頻繁に設定されている OID 要求をサポートします。 IPsec のバージョン 2 (IPsecv2) オフロードなどのインターフェイスを提供、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)直接 OID 要求の OID。 直接の OID 要求インターフェイスは、NDIS ドライバーでは省略可能。

NDIS 6.81 と以降のフィルター ドライバーは、NDIS の提供、[同期 OID 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)します。 *同期 OID 要求パス*同期が必要な Oid またはする必要がありますいないによるキューにフィルター ドライバーなどの Oid をサポートしている[RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) Oid。 同期 OID 要求インターフェイスは、NDIS ドライバーのオプションですが、フィルター ドライバー RSSv2 のサポートをアドバタイズする場合は必須です。

フィルター ドライバーの OID 要求の詳細については、以下のトピックです。

[NDIS フィルター ドライバーの OID 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)

[NDIS フィルター ドライバーから OID 要求を生成します。](generating-oid-requests-from-an-ndis-filter-driver.md)

[モジュールの直接の OID 要求をフィルター処理します。](filter-module-direct-oid-requests.md)

[モジュールの OID を同期要求をフィルター処理します。](filter-module-synchronous-oid-requests.md)

 

 





