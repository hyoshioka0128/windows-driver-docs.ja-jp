---
title: モジュールの OID 要求をフィルター処理します。
description: モジュールの OID 要求をフィルター処理します。
ms.assetid: 6de5ec1c-8e12-4f50-8708-ec136cafd9c2
keywords:
- フィルター モジュールの WDK ネットワーク、OID 要求
- フィルター ドライバー WDK ネットワーク、OID 要求
- NDIS フィルター ドライバー WDK、OID 要求
- Oid WDK ネットワー キング、フィルター ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77b384ad25b00c26b864e82ea7bb4776fa5b7b9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553415"
---
# <a name="filter-module-oid-requests"></a>モジュールの OID 要求をフィルター処理します。





NDIS は、アダプターのパラメーターは、デバイスの特性、構成可能な設定、および統計情報などのパラメーターを含めるを識別するためにオブジェクト識別子 (OID) の値を定義します。 Oid の詳細については、[NDIS Oid](https://msdn.microsoft.com/library/windows/hardware/ff566707)を参照してください。

フィルター ドライバーは、クエリまたは基になるドライバーの動作のパラメーターを設定またはドライバーを後続の OID 要求をフィルター処理できます。

NDIS も用意されています。、 [NDIS 6.1 の OID 要求インターフェイスを直接](direct-oid-request-interface-in-ndis-6-1.md)とドライバーを後でフィルター処理します。 *OID の直接の要求パス*クエリを実行したり、頻繁に設定されている OID 要求をサポートします。 IPsec のバージョン 2 (IPsecv2) オフロードなどのインターフェイスを提供、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812)直接 OID 要求の OID。 直接の OID 要求インターフェイスは、NDIS ドライバーでは省略可能。

NDIS 6.81 と以降のフィルター ドライバーは、NDIS の提供、[同期 OID 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)します。 *同期 OID 要求パス*同期が必要な Oid またはする必要がありますいないによるキューにフィルター ドライバーなどの Oid をサポートしている[RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) Oid。 同期 OID 要求インターフェイスは、NDIS ドライバーのオプションですが、フィルター ドライバー RSSv2 のサポートをアドバタイズする場合は必須です。

フィルター ドライバーの OID 要求の詳細については、以下のトピックです。

[NDIS フィルター ドライバーの OID 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)

[NDIS フィルター ドライバーから OID 要求を生成します。](generating-oid-requests-from-an-ndis-filter-driver.md)

[モジュールの直接の OID 要求をフィルター処理します。](filter-module-direct-oid-requests.md)

[モジュールの OID を同期要求をフィルター処理します。](filter-module-synchronous-oid-requests.md)

 

 





