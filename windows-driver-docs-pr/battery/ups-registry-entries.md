---
title: UPS レジストリ エントリ
description: UPS レジストリ エントリ
ms.assetid: d0d4ef8f-9df1-48a3-b0fc-cea4eb3cdf40
keywords:
- UPS のミニドライバー WDK、レジストリ エントリ
- UPS の WDK のレジストリ エントリ
- レジストリ WDK UPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 494ef69cc0c7b632e5fa9f5fdaf9fa0ff897133b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328426"
---
# <a name="ups-registry-entries"></a>UPS レジストリ エントリ


## <span id="ddk_ups_registry_entries_kg"></span><span id="DDK_UPS_REGISTRY_ENTRIES_KG"></span>


UPS レジストリ エントリでは、システムの UPS についてモデルに固有の情報を提供します。 ベンダーから提供されたの UPS ミニドライバーは、一部の UPS サービスのツリーの下に格納されているこれらのレジストリ エントリの値を指定します。

次のレジストリ キーは、UPS サービス ツリーのルートを示します。

**HKEY\_LOCAL\_MACHINE**\\**SYSTEM**\\**CurrentControlSet**\\**Services**\\**UPS**

次の 4 つのキーの下では、UPS のレジストリ エントリが構成されています。

-   **UPS** --サービス コントロール マネージャ エントリ、および Windows NT 4.0 UPS サービスで使用されるエントリ

    これらのエントリは、システムでのみ使用されます。 ベンダーは、これらのエントリを変更する必要があります。

-   **UPS**\\**Config** --UPS サービスの構成に関連する情報。

    これらのエントリは、システムでのみ使用されます。 ベンダーは、これらのエントリを変更する必要があります。

-   [UPS\\状態レジストリ エントリ](ups-status-registry-entries.md)--状態情報。

    これらのエントリはベンダーとシステムを使用します。 仕入先を作成し、必要に応じて、これらのエントリを変更する場合**電源オプション**に表示されます。

-   [UPS\\ServiceProviders レジストリ エントリ](ups-serviceproviders-registry-entries.md)-さまざまなベンダーと UPS デバイスをモデルのエントリ。

    これらのエントリはベンダーとシステムを使用します。 ベンダーは、中にこれらのエントリを作成する必要があります[UPS ミニドライバーをインストールする](installing-ups-minidrivers.md)します。 システムの UPS サービスでは、管理者が使用するため、UPS モデルを選択した後に、他のシステム管理の対象のレジストリの場所に UPS モデル固有の値をコピーします。

 

 




