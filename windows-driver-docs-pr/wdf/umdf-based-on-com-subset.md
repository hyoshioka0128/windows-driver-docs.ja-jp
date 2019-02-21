---
title: COM のサブセットに基づく UMDF
description: COM のサブセットに基づく UMDF
ms.assetid: 918459a9-a6a2-40b8-8b97-3aabe3e49bfb
keywords:
- WDK の UMDF オブジェクト、COM のサブセット
- フレームワークは、WDK UMDF、COM のサブセットをオブジェクトします。
- COM の WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aef0031d9c1c71b255a185cb2c648993b33fa15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531785"
---
# <a name="umdf-based-on-com-subset"></a>COM のサブセットに基づく UMDF


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework のオブジェクトとインターフェイスは、次の理由でコンポーネント オブジェクト モデル (COM) を基づいています。

-   COM は、アプリケーションの多くのプログラマになじみです。

-   C++ では、COM アプリケーションをプログラミング言語です。

-   COM インターフェイスは、デバイス ドライバー インターフェイス (DDI) が理解し、やすいように、関数の論理的なグループを有効にします。

-   COM の使用を拡張し、既存のドライバー Dll を再コンパイルを必要とせずに、進化 DDI 有効にします。

-   Microsoft Visual Studio と active template library (ATL) を含む、多数のツールは、COM ベースのアプリケーションとオブジェクトをサポートします。

フレームワークは、COM のごく一部のみを使用します。全体の COM インフラストラクチャとランタイム ライブラリには依存しません。 代わりに、フレームワークは、クエリ インターフェイスと機能の参照カウントだけを使用します。 派生したすべての framework インターフェイス**IUnknown**し、そのためのサポート、 **QueryInterface**、 **AddRef**、および**リリース**メソッド既定では。 **AddRef**と**リリース**メソッドがオブジェクトの有効期間を管理します。 **QueryInterface**メソッドは、ドライバーがサポートするインタ フェースを判断するには、その他のコンポーネントを使用できます。

 

 





