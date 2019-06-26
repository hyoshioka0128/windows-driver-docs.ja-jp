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
ms.openlocfilehash: 97475d631dbb907376886052fa8ea1fb564717f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385010"
---
# <a name="device-dedicated-threads"></a>デバイス専用スレッド





低速のデバイスまたは (フロッピー コント ローラー) などはめったに使用するデバイスのドライバーは、デバイス専用のシステム スレッドを作成する多くの「待機中」の問題を解決できます。 さらに、ほとんどのファイル システム ドライバーはシステム ワーカー スレッドを使用して、ワーカー スレッド コールバック ルーチンを指定します。

デバイス ドライバーは、独自のスレッド コンテキストまたはシステム スレッド コンテキストで実行されて、デバイス専用のスレッドまたはワーカー スレッド コールバック ルーチンの最上位レベルのドライバーの同期できるは、ディスパッチャー オブジェクトでの操作など、[イベント オブジェクト](event-objects.md)または[セマフォ オブジェクト](semaphore-objects.md)ドライバーのデバイスの拡張機能の共有の通信のリージョンにします。 たとえば、デバイス専用のスレッドできますお待ち、共有のディスパッチャー オブジェクトで、スレッドのデバイスが使用されていない、呼び出すことによって[ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)セマフォの。 (この時点で、セマフォに設定シグナルされた状態)、I/O 操作を実行するデバイス ドライバーが呼び出されるまでの待機中のスレッドを CPU 時間使用しません。

ドライバーが呼び出せる[ **PsCreateSystemThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)ドライバーまたはデバイス専用のスレッドを作成し、呼び出す[ **KeSetBasePriorityThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kesetbaseprioritythread)スレッドの基本優先順位を設定します。 ドライバーを回避する優先度の値を指定する必要があります*実行時の優先順位の逆転*SMP マシンでします。 高すぎるドライバーが作成したスレッドの基本優先順位の設定は、ドライバーの I/O 要求を送信する優先順位の低いスレッドの実行に遅延に作成します。

スレッド オブジェクトは、dispatcher オブジェクトの型自体であるため、スレッドが完了する別のスレッドの待機できます。 スレッドに関連付けられているスレッド オブジェクト ポインターを取得するには、ドライバーを呼び出すことができます[ **ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)から受信したスレッド ハンドルを渡して、 **PsCreateSystemThread**.

スレッドを呼び出すことができます[ **KeDelayExecutionThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kedelayexecutionthread)完全なタイム スライスの可能性がある、一定期間待機する以上。 粒度、 **KeDelayExecutionThread**間隔は約 10 ミリ秒です。 **KeDelayExecutionThread**タイマー駆動日常的なその間隔の粒度が若干高速またはプラットフォームによって、10 ミリ秒より遅くなります。

 

 




