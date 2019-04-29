---
title: デバイス専用スレッド
description: デバイス専用スレッド
ms.assetid: 2e11e2c9-aefd-4b7b-8d80-7eb1da9f7cce
keywords:
- スレッド オブジェクトの WDK カーネル
- デバイス専用のスレッドの WDK カーネル
- 実行時の優先順位の逆転 WDK カーネル
- PsCreateSystemThread
- KeSetBasePriorityThread
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2220e9453ae6e3fc058a14d68097973d229e5e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388138"
---
# <a name="device-dedicated-threads"></a>デバイス専用スレッド





低速のデバイスまたは (フロッピー コント ローラー) などはめったに使用するデバイスのドライバーは、デバイス専用のシステム スレッドを作成する多くの「待機中」の問題を解決できます。 さらに、ほとんどのファイル システム ドライバーはシステム ワーカー スレッドを使用して、ワーカー スレッド コールバック ルーチンを指定します。

デバイス ドライバーは、独自のスレッド コンテキストまたはシステム スレッド コンテキストで実行されて、デバイス専用のスレッドまたはワーカー スレッド コールバック ルーチンの最上位レベルのドライバーの同期できるは、ディスパッチャー オブジェクトでの操作など、[イベント オブジェクト](event-objects.md)または[セマフォ オブジェクト](semaphore-objects.md)ドライバーのデバイスの拡張機能の共有の通信のリージョンにします。 たとえば、デバイス専用のスレッドできますお待ち、共有のディスパッチャー オブジェクトで、スレッドのデバイスが使用されていない、呼び出すことによって[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)セマフォの。 (この時点で、セマフォに設定シグナルされた状態)、I/O 操作を実行するデバイス ドライバーが呼び出されるまでの待機中のスレッドを CPU 時間使用しません。

ドライバーが呼び出せる[ **PsCreateSystemThread** ](https://msdn.microsoft.com/library/windows/hardware/ff559932)ドライバーまたはデバイス専用のスレッドを作成し、呼び出す[ **KeSetBasePriorityThread** ](https://msdn.microsoft.com/library/windows/hardware/ff553246)スレッドの基本優先順位を設定します。 ドライバーを回避する優先度の値を指定する必要があります*実行時の優先順位の逆転*SMP マシンでします。 高すぎるドライバーが作成したスレッドの基本優先順位の設定は、ドライバーの I/O 要求を送信する優先順位の低いスレッドの実行に遅延に作成します。

スレッド オブジェクトは、dispatcher オブジェクトの型自体であるため、スレッドが完了する別のスレッドの待機できます。 スレッドに関連付けられているスレッド オブジェクト ポインターを取得するには、ドライバーを呼び出すことができます[ **ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)から受信したスレッド ハンドルを渡して、 **PsCreateSystemThread**.

スレッドを呼び出すことができます[ **KeDelayExecutionThread** ](https://msdn.microsoft.com/library/windows/hardware/ff551986)完全なタイム スライスの可能性がある、一定期間待機する以上。 粒度、 **KeDelayExecutionThread**間隔は約 10 ミリ秒です。 **KeDelayExecutionThread**タイマー駆動日常的なその間隔の粒度が若干高速またはプラットフォームによって、10 ミリ秒より遅くなります。

 

 




