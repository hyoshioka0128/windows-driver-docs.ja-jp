---
title: データ型のラッパー
description: データ型のラッパー
ms.assetid: 8c88002b-4d0a-4e81-b50d-f765caa7cf80
keywords:
- スナップショット WDK GDL、構造体
- GDL WDK、列挙型
- WDK GDL 列挙型
- データ型の WDK GDL
- GDL WDK、データ型
- パーサー WDK GDL、データ型のラッパー
- WDK GDL、スナップショットのデータ型 wrapers
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cea285f931f3f5c7ac190fea891e102af3eca303
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529876"
---
# <a name="data-type-wrappers"></a>データ型のラッパー


GDL パーサーでは、実際のスナップショットに表示される XML 属性に適切な宣言を含む別のデータ型の各テンプレートで定義されたデータ型をラップします。 XSD スキーマがスキーマ検証エラーとして要素の開始タグ内に表示される宣言されていない XML 属性を処理するため、この追加のデータ型が必要です。 また、この追加のデータ型はパーサーによって内部的に使用される属性を理解する必要がなくなり、テンプレート、スナップショットの将来の変更からの影響を受けないようにします。

 

 




