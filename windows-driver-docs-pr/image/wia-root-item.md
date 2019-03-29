---
title: WIA ルート項目
description: WIA ルート項目
ms.assetid: cf4d1056-3437-4ba7-8a87-421e91afd02a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 414ba5d4bf0d4c72d16eeadfd6ebc708a186f605
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570084"
---
# <a name="wia-root-item"></a>WIA ルート項目





WIA ルート項目は、デバイス自体を表すフォルダー アイテムです。 WIA ルート項目が付いた**WiaItemTypeRoot**と**WiaItemTypeDevice**などのデバイスの属性が含まれています。

-   製造元の名前

-   デバイス名

-   ドライバーの属性 (ドライバーのバージョンと、ユーザー インターフェイスの CLSID を含む)

イメージング アプリケーションが呼び出すことで、WIA 項目のツリーで、ルート項目を取得、 **IWiaDevMgr::CreateDevice**メソッド (Microsoft Windows SDK のドキュメントで説明)。 その後、アプリケーションでは、ルート項目を使用して、ツリーで、個々 の子項目へのアクセスを得ようを列挙します。

 

 




