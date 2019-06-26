---
title: ミニポート アダプター OID 要求
description: ミニポート アダプター OID 要求
ms.assetid: c3769b1e-c84a-499d-9f93-17a31441a477
keywords:
- Oid WDK ネットワーク、ミニポート アダプターの要求
- ミニポート アダプタの WDK ネットワーク、OID 要求
- アダプターの WDK ネットワーク、OID 要求
- オブジェクト識別子の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a442f4eb223c43108279df4ba2d8c77aec267972
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373947"
---
# <a name="miniport-adapter-oid-requests"></a>ミニポート アダプター OID 要求





NDIS は、デバイスの特性、構成可能な設定、および統計情報などのパラメーターを含めるミニポート アダプターのパラメーターを識別するためにオブジェクト識別子 (OID) の値を定義します。 Oid の詳細については、次を参照してください。 [NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

NDIS 6.1 と以降のミニポート ドライバーでは、NDIS の提供、 [OID 要求インターフェイスを直接](direct-oid-request-interface-in-ndis-6-1.md)します。 *直接 OID 要求パス*クエリを実行したり、頻繁に設定されている OID 要求をサポートします。 直接 OID 要求インターフェイスでは、NDIS ドライバーの省略可能です。

NDIS 6.80 と以降のミニポート ドライバーでは、NDIS の提供、[同期 OID 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)します。 *同期 OID 要求パス*同期が必要な Oid またはする必要がありますいないによるキューにフィルター ドライバーなどの Oid をサポートしている[RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) Oid。 同期 OID 要求インターフェイスは、NDIS ドライバーのオプションですが、ミニポート ドライバー RSSv2 のサポートをアドバタイズする場合は必須です。

ミニポート ドライバー OID 要求の詳細については、以下のトピックです。

[ミニポート アダプタの OID 要求の処理](handling-oid-requests-in-a-miniport-adapter.md)

[ミニポート アダプタ OID 要求のシリアル化](miniport-adapter-oid-request-serialization.md)

[ミニポート アダプタの直接の OID 要求](miniport-adapter-direct-oid-requests.md)

[ミニポート アダプタの同期の OID 要求](miniport-adapter-synchronous-oid-requests.md)
