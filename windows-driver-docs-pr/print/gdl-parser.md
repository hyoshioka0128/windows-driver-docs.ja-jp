---
title: GDL パーサー
description: GDL パーサー
ms.assetid: abb0e9b7-db98-4f8c-af15-83cd1841e5c2
keywords:
- GDL WDK、パーサー
- パーサー WDK GDL, 概要
- プリンター ドライバー WDK、データを XML に変換します。
- WDK GDL の XML データを変換します。
- XML の WDK GDL にデータを変換します。
- WDK GDL データの解析
- WDK GDL、GDL パーサーのスナップショット
- WDK GDL パーサー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deb6613783927531d6e86a94a013a31795e4dfda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353243"
---
# <a name="gdl-parser"></a>GDL パーサー


GDL パーサーでは、GDL データが、スナップショットを XML に変換します。 パーサーの制御に関する詳細については、次を参照してください。 [IPrintCoreHelperUni](details-of-the-iprintcorehelperuni-interface.md)インターフェイス。

GDL 提供[標準解析](standard-gdl-parsing.md)と[テンプレート ベースの解析](gdl-template-structure.md)します。

パーサー フィルターが認識のさまざまな*データ型のプリミティブ*します。 これらのデータ型は属性の値として表示されと同等の XML のスナップショットで、最も近い XML にマップされます。 さらに、パーサーのフィルターは、プリミティブ データ型から作成した複合データ型を認識します。 データの種類のテンプレートを使用して、データ型を定義し、  **\*ValueType**ディレクティブを使用して、属性のテンプレートを使用したデータ型のテンプレートを関連付けます。

標準解析の詳細については、次を参照してください。[標準 GDL 解析](standard-gdl-parsing.md)します。

テンプレートのデータ型の詳細については、次を参照してください。 [GDL テンプレートのデータ型](gdl-template-data-types.md)します。

解析の概要情報をトラブルシューティングするには、次を参照してください。[トラブルシューティング GDL 解析](troubleshooting-gdl-parsing.md)します。

 

 




