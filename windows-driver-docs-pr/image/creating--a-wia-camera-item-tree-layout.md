---
title: WIA カメラ項目のツリー レイアウトを作成します。
description: WIA カメラ項目のツリー レイアウトを作成します。
ms.assetid: 83b496dc-8c47-46fb-b703-837eb536cb66
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11bf5496941d34ac84e1c2bca748e7cca915d184
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538399"
---
# <a name="creating-a-wia-camera-item-tree-layout"></a>WIA カメラ項目のツリー レイアウトを作成します。





Microsoft Windows Me、および Windows XP で WIA カメラの項目のツリーは、ルート項目、およびイメージとカメラのデバイスに格納されているフォルダーを表す子項目で構成されます。 参照してください[WIA ミニドライバーの初期化](initializing-the-wia-minidriver.md)項目ツリーを作成する方法の例についてはします。 次の図は、Windows XP と Windows Me、項目のツリーを示します。

![windows 用の wia カメラの項目を示すダイアグラムがツリー me および windows xp](images/camera-tree.png)

Windows Vista 以降のオペレーティング システムでカメラのツリーの図では、次を参照してください。 [WIA 項目フラグの使用状況の例とカテゴリ](example-usage-of-wia-item-flags-and-categories.md)します。

カメラの項目のツリーのルート項目には、すべての標準的な WIA ミニドライバー情報およびカメラ固有のプロパティが含まれています。 カメラに固有のプロパティには、撮影した画像の数とその他のカメラ コントロールのプロパティが含まれます。

カメラの項目のツリーの子項目は、イメージまたはデバイスに格納されているフォルダーを表します。 ミニドライバーが任意の不要なレベルの譲渡の項目に簡単にアクセスできるようにフォルダーを除去することをお勧めします。 これによってアクセス WIA 項目にアプリケーションで簡単になり、ユーザーの実際のイメージを取得するフォルダー構造の詳細を移動することを防ぎます。

ミニドライバー ライターがファイルを与えることができますおよびフォルダーは、どの名前をそのユーザーの要望を項目します。 ただし、WIA 項目のツリー内の各項目は、カメラの物理的なデータ項目を表すし、カメラの実際のデータ項目の候補を示す名前を指定する必要があります。

データ項目が追加またはカメラから削除されたときに、カメラの内容とその WIA 項目のツリーを同期する WIA ミニドライバーの責任になります。 これを行う方法の例は、次を参照してください。 [WIA 項目のツリー構造を変更する](changing-the-wia-item-tree-structure.md)します。

WIA サービスを介して、アプリケーションは、次の操作を実行できます。

-   カメラの機能のクエリを実行します。

-   デバイスのカメラのプロパティを設定します。

-   データ転送を要求します。

 

 




