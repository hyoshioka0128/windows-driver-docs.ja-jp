---
title: 標準 GDL 解析
description: 標準 GDL 解析
ms.assetid: 089bba58-e29f-428a-ab54-4413edca1d0c
keywords:
- GDL WDK、パーサー
- パーサー WDK GDL、標準的な解析
- WDK GDL データの解析
- 標準の GDL WDK の解析
- 既定の GDL WDK の解析
- 標準的なパーサー フィルター WDK GDL
- SPF の WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2544d7729d678297224c6adb0f8b3925fa577a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389473"
---
# <a name="standard-gdl-parsing"></a>標準 GDL 解析


既定値または標準のパーサー フィルター (SPF) 元のスナップショット ツリー (つまり、XML スナップショット パーサーによって生成される CDATA 要素としての生の未解析値のみが属性ノードに含めることが) を入力として受け取りし、追加のセマンティクスを実行します検証および処理します。

この処理では、SPF は、CDATA の生の値を属性ノードにバインドされていて、正しく、値を表す 1 つまたは複数の標準的な XML データ型として属性ノードで新しい XML 要素を追加します。 テンプレートで指定されているデータ型として解釈されます。 により、XML データ型の要素としての値にアクセスするクライアントは、装飾 XML スナップショット ツリーになります。

処理は、メンバーのチェックも含まれています属性値の解析、乗算の処理定義されている属性、既定初期化属性、およびその他を含む結果のツリーの XML 表現の生成。要素。 必要な場合は警告とエラー メッセージが生成されます。 実行される処理は、特定のテンプレート ディレクティブによって転送されます。

 

 




