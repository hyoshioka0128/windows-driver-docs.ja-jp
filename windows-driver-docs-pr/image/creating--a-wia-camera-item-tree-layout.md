---
title: WIA カメラの項目ツリーレイアウトの作成
description: WIA カメラの項目ツリーレイアウトの作成
ms.assetid: 83b496dc-8c47-46fb-b703-837eb536cb66
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8dc530a8be4917c77e36ebf229719509176d1402
ms.sourcegitcommit: 88f6e7355de9e0714057020557dc8c7831e90e7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84638425"
---
# <a name="creating-a-wia-camera-item-tree-layout"></a>WIA カメラの項目ツリーレイアウトの作成

Microsoft Windows Me と Windows XP の WIA カメラ項目ツリーは、ルート項目と、カメラデバイスに格納されているイメージとフォルダーを表す子項目で構成されています。 項目ツリーを作成する方法の例については[、「WIA ミニドライバーの初期化](initializing-the-wia-minidriver.md)」を参照してください。 次の図は、Windows Me と Windows XP の項目ツリーを示しています。

![windows me と windows xp の wia カメラ項目ツリーを示す図](images/camera-tree.png)

Windows Vista 以降のオペレーティングシステムのカメラツリーの図については、「 [WIA 項目のフラグとカテゴリの使用例](example-usage-of-wia-item-flags-and-categories.md)」を参照してください。

カメラ項目ツリーのルート項目には、すべての標準的な WIA ミニドライバー情報とカメラ固有のプロパティが含まれています。 カメラ固有のプロパティには、撮影された画像の数とその他のカメラコントロールのプロパティが含まれます。

カメラ項目ツリーの子項目は、デバイスに格納されているイメージまたはフォルダーを表します。 ミニドライバーでは、転送可能な項目へのアクセスを容易にするために、不要なレベルのフォルダーを排除することをお勧めします。 これにより、アプリケーションによって WIA 項目へのアクセスが容易になり、ユーザーはフォルダー構造に移動して実際のイメージを取得する必要がなくなります。

ミニドライバー開発者は、必要な名前を持つファイルとフォルダーを指定できます。 ただし、WIA 項目ツリー内の各項目は、カメラ上の物理的なデータ項目を表し、カメラ内の実際のデータ項目を示す名前を付ける必要があります。

カメラにデータ項目を追加または削除した場合、その WIA 項目ツリーをカメラの内容と同期するのは、WIA ミニドライバーの役割です。 これを行う方法の例については、「 [WIA 項目ツリー構造の変更](changing-the-wia-item-tree-structure.md)」を参照してください。

アプリケーションでは、WIA サービスを使用して次の操作を実行できます。

- カメラの機能を照会する

- カメラデバイスのプロパティを設定する

- データ転送を要求する
