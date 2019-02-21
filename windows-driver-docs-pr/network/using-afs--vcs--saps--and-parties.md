---
title: AFs、VCs、Sap、およびパーティの使用
description: AFs、VCs、Sap、およびパーティの使用
ms.assetid: 4bf736a9-1236-4322-85f0-5d3ab7b8c549
keywords:
- 接続指向 NDIS WDK、エンティティの作成
- ネットワークを作成したエンティティいる CoNDIS WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e1eec5a3be271ce55b994dd2d8d39e8d5643ed8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553780"
---
# <a name="using-afs-vcs-saps-and-parties"></a>AFs、VCs、Sap、およびパーティの使用





ドライバーの接続指向では、作成し、アドレス ファミリ (AFs)、仮想接続 (VCs)、サービス アクセス ポイント (Sap)、および関係者を含むエンティティを使用します。

接続指向のドライバーは、AF を登録します。 または、VC、SAP、パーティを作成し、ローカル コンテキストの NDIS にそのエンティティのエリアにポインターを渡します。 NDIS は、ドライバー (およびその他の適切な接続指向ドライバー) ハンドルが返されますを新しく登録された AF、新しく作成された VC、SAP、またはパーティを表します。

次のトピックでは、接続指向のドライバーを作成して使用するエンティティについて説明します。

[アドレス ファミリ](address-families.md)

[仮想接続](virtual-connections.md)

[サービス アクセス ポイント](service-access-points.md)

[パーティ](parties.md)

 

 





