---
title: フレームワーク キュー オブジェクト
description: フレームワーク キュー オブジェクト
ms.assetid: 42736e2d-2482-46b4-bf52-4efe369db40b
keywords:
- I/O 要求の WDK KMDF、キュー オブジェクト
- WDK KMDF の I/O キュー
- WDK KMDF のキュー オブジェクト
- I/O キュー オブジェクト WDK KMDF
- 要求の WDK KMDF、キュー オブジェクトの処理
- WDK KMDF のキュー
- WDK KMDF、framework のオブジェクトのキュー
- I/O キューの I/O キュー WDK KMDF、
- WDK KMDF のコールバック関数
- WDK KMDF のイベントのコールバック関数
- フレームワークは、WDK KMDF、I/O キューのオブジェクトをオブジェクトします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c91318ab44cfd0bbb76e78e91d51a87f98b534d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384454"
---
# <a name="framework-queue-objects"></a>フレームワーク キュー オブジェクト





フレームワークのキュー オブジェクトが表す*の I/O キュー*ドライバーが受け取る要求は、I/O のコンテナー。 各ドライバーでは、デバイスごとに 1 つまたは複数の I/O キューを作成できます。 フレームワークのキュー オブジェクトのセットを定義する[イベント コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/)ドライバーを提供して、ドライバーを呼び出すことができるオブジェクトのメソッドのセット。

フレームワークでは、送信先、ドライバーのデバイスの 1 つの I/O 要求を受け取る、フレームワークは、適切な I/O キューに要求を配置します。 ドライバーは、1 つまたは複数を登録します。 場合[要求ハンドラー](request-handlers.md)、フレームワーク通知には、ドライバー、I/O 要求があるたびにことができます。 または、ドライバーは、要求の I/O キューをポーリングできます。

このセクションの内容:

[I/O キューの作成](creating-i-o-queues.md)

[I/O キューの削除](deleting-i-o-queues.md)

[I/O キューを管理します。](managing-i-o-queues.md)

[電源管理対象の I/O キューを使用します。](using-power-managed-i-o-queues.md)

[I/O 操作の進行を保証します。](guaranteeing-forward-progress-of-i-o-operations.md)

[I/O キューの状態](i-o-queue-states.md)

[I/O キューの使用例](example-uses-of-i-o-queues.md)

 

 





