---
title: アドレス ファミリと SAPs での操作
description: アドレス ファミリと SAPs での操作
ms.assetid: 0fc821bb-49a2-4631-8735-ef5217073ba9
keywords:
- 接続指向 NDIS WDK、アドレス ファミリ
- いる CoNDIS の WDK は、ネットワーク アドレス ファミリ
- 接続指向 NDIS WDK、サービス アクセス ポイント
- いる CoNDIS の WDK は、ネットワーク サービス アクセス ポイント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97a4665814121328a6fdcf0ef9ef7e971944a316
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529962"
---
# <a name="operations-on-address-families-and-saps"></a>アドレス ファミリと SAPs での操作





コール マネージャーまたは MCM のドライバーが NDIS をそのコール マネージャーのエントリ ポイントを登録し、接続指向のクライアントにそのコール マネージャー サービスを提供する必要があります。 NDIS enttry ポイントに登録する詳細については、次を参照してください。[いる CoNDIS 登録](condis-registration.md)します。

コール マネージャーまたは MCM のドライバーのコール マネージャー サービスを使用するには、接続指向のクライアントは、そのコール マネージャーまたは MCM ドライバーで、アドレス ファミリを開く必要があります。 着信呼び出しを受信するには、クライアントには、コール マネージャーやドライバーの MCM の 1 つまたは複数の Sap 登録もする必要があります。

次の接続指向の操作に関連するアドレス ファミリと SAPs:

[登録して、アドレス ファミリを開く](registering-and-opening-an-address-family.md)

[SAP の登録](registering-a-sap.md)

[SAP の登録を解除](deregistering-a-sap.md)

[アドレス ファミリを閉じる](closing-an-address-family.md)

 

 





