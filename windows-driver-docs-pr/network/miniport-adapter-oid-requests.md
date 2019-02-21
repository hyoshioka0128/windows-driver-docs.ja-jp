---
title: ミニポート アダプタの OID 要求
description: ミニポート アダプタの OID 要求
ms.assetid: c3769b1e-c84a-499d-9f93-17a31441a477
keywords:
- Oid WDK ネットワーク、ミニポート アダプターの要求
- ミニポート アダプタの WDK ネットワーク、OID 要求
- アダプターの WDK ネットワーク、OID 要求
- オブジェクト識別子の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8aaa235a875f479dae951da3f5ec63c23e971b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550239"
---
# <a name="miniport-adapter-oid-requests"></a>ミニポート アダプタの OID 要求





NDIS は、デバイスの特性、構成可能な設定、および統計情報などのパラメーターを含めるミニポート アダプターのパラメーターを識別するためにオブジェクト識別子 (OID) の値を定義します。 Oid の詳細については、次を参照してください。 [NDIS Oid](https://msdn.microsoft.com/library/windows/hardware/ff566707)します。

NDIS 6.1 と以降のミニポート ドライバーでは、NDIS の提供、 [OID 要求インターフェイスを直接](direct-oid-request-interface-in-ndis-6-1.md)します。 *直接 OID 要求パス*クエリを実行したり、頻繁に設定されている OID 要求をサポートします。 直接 OID 要求インターフェイスでは、NDIS ドライバーの省略可能です。

NDIS 6.80 と以降のミニポート ドライバーでは、NDIS の提供、[同期 OID 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)します。 *同期 OID 要求パス*同期が必要な Oid またはする必要がありますいないによるキューにフィルター ドライバーなどの Oid をサポートしている[RSSv2](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) Oid。 同期 OID 要求インターフェイスは、NDIS ドライバーのオプションですが、ミニポート ドライバー RSSv2 のサポートをアドバタイズする場合は必須です。

ミニポート ドライバー OID 要求の詳細については、以下のトピックです。

[ミニポート アダプタの OID 要求の処理](handling-oid-requests-in-a-miniport-adapter.md)

[ミニポート アダプタ OID 要求のシリアル化](miniport-adapter-oid-request-serialization.md)

[ミニポート アダプタの直接の OID 要求](miniport-adapter-direct-oid-requests.md)

[ミニポート アダプタの同期の OID 要求](miniport-adapter-synchronous-oid-requests.md)
