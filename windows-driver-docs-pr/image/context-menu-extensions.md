---
title: コンテキスト メニューの拡張
description: コンテキスト メニューの拡張
ms.assetid: 6c52dd43-7f47-476e-acbc-15269d23ea71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8c3ed0b12339a922e786dbfa30f15e66d5281d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368550"
---
# <a name="context-menu-extensions"></a>コンテキスト メニューの拡張





スキャナーとカメラのコントロール パネル の両方でデバイス (ルート項目) と、マイ コンピューター フォルダーでは、フォルダー、ユーザーはそのコンテキスト メニューで公開されているアクションに基づいて、選択した項目に対して実行するさまざまなアクションを選択できます。 これらのアクションを検索するには、ユーザーは縮小表示または指定したイメージのアイコンを右クリックします。

コンテキスト メニューの アクションを追加する方法を実装するためには、 **IContextMenu**インターフェイス (Microsoft Windows SDK のドキュメントを参照してください)。 実装するプロセスでサーバーを提供できるは、ベンダー、 **IContextMenu**のためのインターフェイス**IWiaItem**デバイスを提供する項目を (Windows SDK のドキュメントを参照してください)。 WIA がイメージのコンテキスト メニューのクエリを実行するたびに、UI のベンダーから提供された拡張機能はさらに呼び出し**IContextMenu::QueryContextMenu**イメージング デバイスの登録されたハンドラーから。 呼び出す**IContextMenu::InvokeCommand**の適切なベンダーから提供された拡張機能を有効にする項目の既定値で渡される UI では処理されません。

 

 




