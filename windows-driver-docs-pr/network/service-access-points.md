---
title: サービス アクセス ポイント
description: サービス アクセス ポイント
ms.assetid: a6fab686-6adb-4d77-8f0d-2b48e2e49f1f
keywords:
- 着信呼び出し WDK いる CoNDIS
- 接続指向 NDIS WDK、サービス アクセス ポイント
- いる CoNDIS の WDK は、ネットワーク サービス アクセス ポイント
- WDK いる CoNDIS のサービス アクセス ポイントします。
- SAPs WDK いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b23a35d0aa405d4ba2b413e76b854e8f9e60827c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553910"
---
# <a name="service-access-points"></a>サービス アクセス ポイント





A*サービス アクセス ポイント*(SAP) は、関心のある接続指向のクライアントへの着信呼び出しの特性を識別します。 SAP を登録するには、コール マネージャーまたは MCM ドライバーと、クライアントは、コール マネージャーまたは MCM のドライバーがその SAP 宛てのすべての着信呼び出しのクライアントを通知する必要がありますを示します。

クライアントは常に登録されません、SAP では、たとえば、着信呼び出しが処理しない場合。 クライアントは、コール マネージャーまたは MCM のドライバーを複数の SAPs を登録できます。

SAPs の詳細については、次を参照してください。[登録 SAP](registering-a-sap.md)と[SAP の登録を解除](deregistering-a-sap.md)します。

 

 





