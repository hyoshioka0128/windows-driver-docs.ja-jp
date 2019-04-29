---
title: フィルター内のノードの結合
description: フィルター内のノードの結合
ms.assetid: ebceb42a-966d-4c03-b4f5-8666284fc871
keywords:
- WDK BDA のノードを制御します。
- WDK BDA ノード
- 結合フィルター WDK BDA 内のノード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0853494988f4e05c653b504c6b7e179a820e58c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329927"
---
# <a name="combining-nodes-in-a-filter"></a>フィルター内のノードの結合





DirectShow フィルター グラフの例の次の図は、制御ノードがフィルターのグラフのフィルターとして表すことが、1 つの方法を示します。 ネットワーク プロバイダーは、常に、その他のすべてのフィルターの前に独自のフィルターです。 このサンプルでがチューナーと復調器のノードが同じ回線カードに結合されますので、1 つのフィルターとして表示されます。 キャプチャ フィルターでは、チューナー/復調器フィルターに従います。 これらのフィルターをこれまでにすべてのフィルターで実際に内部および外部接続は制御ノードと一致します。 ダウン ストリームの次のフィルターは、図に示すように、パケットの識別子 (PID) フィルターを公開する 1 つのフィルターで表される mpeg-2 トランスポート ストリーム デマルチプレクサー、[制御ノード](control-nodes.md)セクション。 実際の mpeg-2 トランスポート ストリーム デマルチプレクサーのフィルターは、基本のすべてのストリームを処理するために必要な回数だけ、トポロジを再現します。

![チューナーと 1 つのフィルターを組み合わせて復調器 directshow フィルター グラフを示す図](images/smpdshw1.png)

 

 




