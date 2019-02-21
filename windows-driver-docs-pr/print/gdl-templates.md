---
title: GDL テンプレート
description: GDL テンプレート
ms.assetid: 9cce885d-395e-4f8d-8076-951d75d82410
keywords:
- GDL WDK、テンプレート
- WDK GDL テンプレート
- GDL エントリ WDK GDL を検証しています
- GDL WDK、エントリを検証しています
- WDK GDL、テンプレートでの属性
- テンプレートで WDK の GDL を構築します。
- WDK GDL の継承
- WDK GDL、継承に基づくスキーマのスキーマ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0e61d5c5b20dc6c72f9103f0ad5ff8b29e20fe3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548893"
---
# <a name="gdl-templates"></a>GDL テンプレート


*GDL テンプレート*GDL エントリを検証するためにパーサーの方法を提供します。 各エントリは、特定のテンプレートを関連付けることができます。

GDL には、新しいテンプレートを追加することで拡張可能な標準テンプレートが提供されます。 標準のテンプレートは、すべての定義、[属性](gdl-attributes.md)と[構築](gdl-constructs.md)知られるオペレーティング システム。

テンプレート間のリレーションシップによって定義されます[継承](gdl-template-inheritance.md)します。

GDL パーサーでは、テンプレートを使用した GDL ファイル内のすべてのデータ エントリを関連付けます。 テンプレートでは、間接的な方法で指定データ エントリが、コンス トラクターの場合は、すべてのメンバーは、その構成要素内に表示されます。 この関連付けでは、再帰的に適用はあるため、すべてのデータ エントリが関連付けられているテンプレートを持つことができます。 テンプレートを使用して、特定[条件](criteria-for-associating-gdl-templates-with-keywords.md)、データ、および特定のテンプレートの関連を定義する[データ型](gdl-template-data-types.md)テンプレート用に使用されます。

GDL を使用して特定[ディレクティブ](gdl-template-directives.md)テンプレート。

 

 




