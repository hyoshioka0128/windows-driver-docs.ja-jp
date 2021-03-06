---
title: IRP のキャンセル
description: IRP のキャンセル
ms.assetid: da199435-f6c3-44f4-b1ed-0280f39ee452
keywords:
- Irp WDK のカーネルのキャンセル
- Irp のキャンセル
- キャンセル ルーチン
- I/O 要求の WDK カーネルのユーザーによって取り消されました
- Irp WDK カーネルでは、キャンセル Irp の完了
- 未処理の IRP 欠航 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3091e174735710be3129c363a8df019ad193259f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383363"
---
# <a name="canceling-irps"></a>IRP のキャンセル





ドライバーは Irp が残る可能性があります (そのため、ユーザーは、以前に送信された I/O 要求をキャンセルでした) は無限の間隔が 1 つ以上がある必要キューイング[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ユーザーによって取り消されました I/O 完了ルーチン要求します。 たとえば、キーボード、マウス、パラレル、シリアル ポート、およびサウンド デバイス ドライバー (またはドライバーの上層にあること)、ファイル システム ドライバーが*キャンセル*ルーチン。

Microsoft Windows XP およびそれ以降のオペレーティング システム用のドライバーを使用できる[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md)独自の実装ではなく*キャンセル*ルーチン。

「IRP をキャンセル」には、システムの整合性を維持しながら、IRP をできるだけ早く完了することを示します。 IRP の完了の概要については、次を参照してください。 [Irp の完了](completing-irps.md)します。

キャンセルは、まず、システムまたはドライバーのいずれかを呼び出すと[ **IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocancelirp)します。 このルーチンは、まだ完全に完了しているスレッドに関連付けられている各 IRP に呼び出されます。 システムは、I/O 要求を開始したスレッドが終了した場合、未処理の Irp をキャンセルします。 ドライバーは、作成した Irp だけをキャンセルできます (を参照してください[下位レベルのドライバーの作成の Irp](creating-irps-for-lower-level-drivers.md))。

IRP が 5 分以内で完了していない場合、I/O マネージャーは IRP がタイムアウトしたかを検討します。スレッドからこのような Irp の関連付けが解除され、IRP を所有しているデバイスのエラーが記録されます。 ドライバーの完了に時間がかかる可能性があるすべての要求がキャンセル可能なことを確認してください。 可能性のある長い要求はキャンセル可能なことに、使用することができます[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md)または[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)ドライバーの開発者からのキャンセルを抽象化します。

このセクションでは、次のトピックでは。

[キャンセル ルーチンの概要](introduction-to-cancel-routines.md)

[キャンセル ルーチンを登録します。](registering-a-cancel-routine.md)

[IRP のキャンセルを同期します。](synchronizing-irp-cancellation.md)

[キャンセル ルーチンを実装します。](implementing-a-cancel-routine.md)

[Irp をキャンセルするときに考慮すべき点](points-to-consider-when-canceling-irps.md)

 

 




