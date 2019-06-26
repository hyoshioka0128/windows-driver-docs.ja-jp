---
title: Windows フィルタリング プラットフォーム アーキテクチャの概要
description: Windows フィルタリング プラットフォーム アーキテクチャの概要
ms.assetid: a20efbe1-f98c-452d-a134-9f65eb6dbc04
keywords:
- Windows フィルタ リング プラットフォーム アーキテクチャ WDK
- WDK Windows フィルタ リング プラットフォームのアーキテクチャ
- フィルター エンジン WDK Windows フィルタ リング プラットフォーム
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム、プラットフォームのアーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e203b72114861da712eafcbd45ca66520221a6e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370580"
---
# <a name="windows-filtering-platform-architecture-overview"></a>Windows フィルタリング プラットフォーム アーキテクチャの概要


このセクションでは、Windows フィルタ リング プラットフォーム アーキテクチャの概要を提供します。 Windows フィルタ リング プラットフォーム アーキテクチャの詳細については、次を参照してください。、 [Windows フィルタ リング プラットフォーム](https://go.microsoft.com/fwlink/p/?linkid=90220)Microsoft Windows SDK のドキュメント。

次の図は、Windows フィルタ リング プラットフォームの基本的なアーキテクチャを示します。

![windows フィルタ リング プラットフォームの基本的なアーキテクチャを示す図](images/wfparch.png)

[フィルター エンジン](filter-engine.md)Windows フィルタ リング プラットフォームのコアです。 フィルター エンジンは、TCP ベースのネットワーク データでのすべてのフィルター操作を実行します。 TCP/IP スタックの重要なポイントでは[レイヤーをフィルタ リング](filtering-layer.md)ネットワーク データが処理するためのフィルター エンジンに渡されます。 フィルター レイヤーのフィルターのフィルター条件がすべて当てはまる場合は、フィルター エンジンは、フィルターのアクションを適用します。

[コールアウト ドライバー](callout-driver.md) 1 つまたは複数を登録することによって追加のフィルター処理機能を提供[コールアウト](callout.md)フィルター エンジン。 [フィルター](filter.md)フィルターでは、エンジンがフィルターのアクションの引き出し線を指定できます。 この場合、フィルター エンジンは、追加の処理の指定した吹き出しをネットワーク データを渡します。

Windows フィルタ リング プラットフォームには、いくつかの組み込みのコールアウトが含まれています。 参照してください[組み込みコールアウト識別子](https://docs.microsoft.com/windows-hardware/drivers/network/built-in-callout-identifiers)のこれらのコールアウトのそれぞれの説明。

 

 





