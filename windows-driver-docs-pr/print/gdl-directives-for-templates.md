---
title: テンプレートの GDL ディレクティブ
description: テンプレートの GDL ディレクティブ
ms.assetid: c68650ae-d6ee-4ae3-afa2-655f2bcad916
keywords:
- WDK GDL、テンプレートのディレクティブのディレクティブ
- ソース ファイル WDK GDL、テンプレートのディレクティブ
- テンプレート ディレクティブ WDK GDL
- パーサー WDK GDL、ディレクティブ
- Template ディレクティブ WDK GDL
- Name ディレクティブ WDK GDL
- Inherits ディレクティブ WDK GDL
- メンバーのディレクティブ WDK GDL
- Type ディレクティブ WDK GDL
- 実稼働ディレクティブ WDK GDL
- メンバーのディレクティブ WDK GDL
- WDK GDL ディレクティブに発生します
- 加法ディレクティブ WDK GDL
- ValueType ディレクティブ WDK GDL
- データ型のディレクティブ WDK GDL
- ElementType ディレクティブ WDK GDL
- ArrayLabel ディレクティブ WDK GDL
- ElementTags ディレクティブ WDK GDL
- WDK GDL、ディレクティブのテンプレート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02b2993665291d4adfeae159930adb2af54f6b87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574400"
---
# <a name="gdl-directives-for-templates"></a>テンプレートの GDL ディレクティブ


GDL には、テンプレートを使用して、GDL スキーマを定義するテンプレートのディレクティブがあります。

GDL には、次のテンプレート ディレクティブが含まれています。

-   **\*テンプレート**テンプレート コンス トラクターを定義します。

その他のいくつかのディレクティブは、定義を完了にテンプレート コンス トラクター内で使用されます。 次の一覧では、テンプレートの構造内で使用される、ディレクティブの一部について説明します。

-   **\*名前**にバインドするデータ エントリのキーワードの名前を指定します。

-   **\*継承**は指定したテンプレートのプロパティを継承します。

-   **\*メンバー**バインディング処理で指定したテンプレートのツリーを使用します。

-   **\*型**このテンプレートを定義するオブジェクトの種類です。

-   **\*実稼働**、 **\*メンバー**、および **\*Occurs**コンス トラクターを許可されているコンテンツを定義します。 注のコンテンツは、構成によって異なります。

-   **\*加法**のどのエントリの定義に表示されるスナップショットのエントリが複数定義されているかどうかについて説明します。

-   **\*ValueType**属性の値をデータ型が割り当てられます。

-   **\*DataType**、  **\*ElementType**、  **\*ArrayLabel**、および **\*ElementTags**データ型を定義します。

テンプレートのディレクティブの詳細については、次を参照してください[GDL テンプレート ディレクティブ。](gdl-template-directives.md)

 

 




