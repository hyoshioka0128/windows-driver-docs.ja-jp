---
title: フレームワーク キュー オブジェクト
description: フレームワーク キュー オブジェクト
ms.assetid: 42736e2d-2482-46b4-bf52-4efe369db40b
keywords:
- I/o 要求 WDK KMDF、キューオブジェクト
- I/o キュー WDK KMDF
- キューオブジェクト WDK KMDF
- I/o キューオブジェクト WDK KMDF
- 要求処理 WDK KMDF、キューオブジェクト
- キュー WDK KMDF
- キュー WDK KMDF, framework オブジェクト
- I/o キュー WDK KMDF、i/o キューについて
- コールバック関数 WDK KMDF
- イベントコールバック関数 WDK KMDF
- framework オブジェクト WDK KMDF、i/o キューオブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69da8ea24232dfc28af6626d6e7e843395090692
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845133"
---
# <a name="framework-queue-objects"></a>フレームワーク キュー オブジェクト





フレームワークキューオブジェクトは、ドライバーが受信する i/o 要求のコンテナーである*i/o キュー*を表します。 各ドライバーは、デバイスごとに1つ以上の i/o キューを作成できます。 フレームワークキューオブジェクトは、ドライバーが提供できる一連の[イベントコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/)と、ドライバーが呼び出すことのできる一連のオブジェクトメソッドを定義します。

フレームワークは、ドライバーのいずれかのデバイスに送られる i/o 要求を受信すると、要求を適切な i/o キューに配置します。 ドライバーで1つ以上の[要求ハンドラー](request-handlers.md)が登録されている場合は、i/o 要求が使用可能になるたびに、フレームワークによってドライバーに通知できます。 または、ドライバーが i/o キューをポーリングして要求を処理することもできます。

このセクションの内容:

[I/o キューの作成](creating-i-o-queues.md)

[I/o キューの削除](deleting-i-o-queues.md)

[I/o キューの管理](managing-i-o-queues.md)

[電源管理の i/o キューの使用](using-power-managed-i-o-queues.md)

[I/o 操作の進行状況を保証する](guaranteeing-forward-progress-of-i-o-operations.md)

[I/o キューの状態](i-o-queue-states.md)

[I/o キューの使用例](example-uses-of-i-o-queues.md)

 

 





