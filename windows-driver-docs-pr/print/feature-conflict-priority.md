---
title: 競合の優先度の機能
description: 競合の優先度の機能
ms.assetid: 1185f983-ed04-4610-8b93-684ae3e07e84
keywords:
- プリンターは、WDK Unidrv、競合の優先度を機能します。
- 競合の優先順位の WDK プリンターの機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aef16af3fd1d3b399110e941ef809c4d400a5075
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549515"
---
# <a name="feature-conflict-priority"></a>競合の優先度の機能





機能の競合の優先度が Unidrv のユーザー インターフェイスのコードを適用するとき、機能に必要とする優先順位を識別する[制約オプション](option-constraints.md)します。

GPD パーサーでは、優先順位の高いものから、次の順序での機能に競合の優先度を割り当てます。

1.  実際にインストールされているインストール可能な機能です。 (を参照してください[インストール可能な機能とオプションの処理](handling-installable-features-and-options.md))。

2.  機能と\*FeatureType はプリンターに設定\_プロパティ。

3.  機能と\* **FeatureType**ドキュメントに設定\_プロパティまたはジョブ\_プロパティ。

各機能の種類内の機能には、機能の指定された値に基づく相対的な優先順位が割り当てられている\*ConflictPriority 属性。 したがって、例では、プリンターの\_プロパティ機能を\* **ConflictPriority** 1 の属性は、DOC より高い優先順位を持つ\_プロパティ機能を\* **ConflictPriority** 3 の属性です。 機能がない、 \* **ConflictPriority**属性より優先順位の低いであります。

詳細については、 \* **FeatureType**と\* **ConflictPriority**属性を参照してください[機能属性](feature-attributes.md)します。

 

 




