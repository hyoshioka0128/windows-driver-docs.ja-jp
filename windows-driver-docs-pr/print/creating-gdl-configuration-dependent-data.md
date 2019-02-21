---
title: GDL 構成に依存するデータを作成します。
description: GDL 構成に依存するデータを作成します。
ms.assetid: 5b00903c-a637-4f83-96b8-92fe850d309e
keywords:
- GDL WDK の構成
- WDK GDL、構成に依存するデータの作成の構成
- WDK GDL 構成に依存するデータを作成します。
- GDL WDK、データを整理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9fd2f7d1ffc03a87164a47776dc77830b6db3d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552689"
---
# <a name="creating-gdl-configuration-dependent-data"></a>GDL 構成に依存するデータを作成します。


GDL 言語では、値が 1 つまたは複数のパラメーターに依存するデータを定義することができます。 GDL クライアントは、パラメーターのデータの依存関係を知っているか、気付いて、データがパラメーターに依存する必要はありません。 GDL クライアントは、各パラメーターに割り当てられる値のみを把握する必要がありますし、GDL は作成して、スナップショットが、指定されたパラメーター値を適切なすべてのデータ。

構成に依存するデータ (CDD) は、1 つまたは複数のパラメーターに依存するデータです。 さまざまな条件または構成対象のデータの同じセットにアクセスする必要があるクライアントは、構成に依存するデータのコンシューマーが最適です。 たとえば、ユーザー指定の場所に常に日付の気象条件を表示するアプリケーションには、(たとえば、毎日の降雨、1 日の高値と安値の温度と平均の空の状況) の同じ情報が表示されます。 場所および日のデータのスナップショットの取得に使用される構成の構築に使用されるパラメーターになります。 簡単に GDL では、構成に依存するフォームにデータを整理することができます。

GDL を使用すると、構成に依存するフォームにデータを整理して、これら 2 つの手順に従います。

1.  パラメーターを定義します。

2.  データに依存関係を追加します。

データを記述する GDL ファイルが作成された後、クライアントは必要な構成を指定し、スナップショットを要求する必要があります。

次のトピックでは、作成および構成に依存するデータを整理する手順について説明します。

[構成に依存するデータのパラメーターを定義します。](defining-the-configuration-dependent-data-parameters.md)

[構成に依存するデータへの依存関係の追加](adding-dependencies-to-the-configuration-dependent-data.md)

[GDL スナップショットの作成](creating-gdl-snapshots.md)

 

 




