---
title: COM サブセットに基づく UMDF
description: COM サブセットに基づく UMDF
ms.assetid: 918459a9-a6a2-40b8-8b97-3aabe3e49bfb
keywords:
- UMDF オブジェクト WDK、COM サブセット
- フレームワークオブジェクト WDK UMDF、COM サブセット
- COM WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a55744eb6acd64f800751fd610cd922f84b39c5b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210256"
---
# <a name="umdf-based-on-com-subset"></a>COM サブセットに基づく UMDF


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

フレームワークオブジェクトとインターフェイスは、次の理由により、コンポーネントオブジェクトモデル (COM) に基づいています。

-   COM は多くのアプリケーションプログラマになじみがあります。

-   C++は、COM アプリケーションのプログラミングに適した言語です。

-   COM インターフェイスを使用すると、デバイスドライバーインターフェイス (DDI) を簡単に理解してナビゲートできるように、関数の論理的なグループ化が可能になります。

-   COM を使用すると、既存のドライバー Dll を再コンパイルしなくても、DDI を拡張および進化させることができます。

-   Microsoft Visual Studio や active template library (ATL) などの多くのツールでは、COM ベースのアプリケーションとオブジェクトがサポートされています。

フレームワークは COM の小さなサブセットのみを使用します。COM インフラストラクチャとランタイムライブラリ全体に依存しません。 代わりに、フレームワークはクエリインターフェイスと参照カウント機能のみを使用します。 すべてのフレームワークインターフェイスは**IUnknown**から派生しているため、既定では**QueryInterface**、 **AddRef**、および**Release**メソッドをサポートしています。 **AddRef**メソッドと**Release**メソッドは、オブジェクトの有効期間を管理します。 **QueryInterface**メソッドを使用すると、他のコンポーネントで、ドライバーがサポートするインターフェイスを特定できます。

 

 





