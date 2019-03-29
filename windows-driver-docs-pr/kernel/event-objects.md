---
title: イベント オブジェクト
description: イベント オブジェクト
ms.assetid: da9df4a2-26cf-4861-80ca-1790ca059e45
keywords:
- カーネルのディスパッチャー オブジェクト WDK、イベント オブジェクト
- ディスパッチャー オブジェクト WDK カーネル、イベント オブジェクト
- イベント オブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52e8322c55a78d97d421f7d35717858b8136c20e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573400"
---
# <a name="event-objects"></a>イベント オブジェクト





ドライバーは、次の下位ドライバーは IRP を待機しているドライバーによってセットアップの処理中に待機するイベント オブジェクトを使用できます。 ドライバーをドライバーで作成されたスレッドまたは同期 I/O 要求の完了を待機するドライバー ディスパッチ ルーチンは、スレッドやその他のドライバーのルーチンの間の操作を同期させるイベント オブジェクトを使用できますも。

このセクションでは、次のトピックについて説明します。

[イベント オブジェクトの定義と](defining-and-using-an-event-object.md)

[標準的なイベント オブジェクト](standard-event-objects.md)

 

 




