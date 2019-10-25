---
title: IRP の完了
description: IRP の完了
ms.assetid: 4b4be95e-ebf5-4726-87fc-20c3e6c94f52
keywords:
- Irp WDK カーネル、完了
- Irp WDK カーネルを完了しています
- 完成した Irp WDK カーネル
- I/o WDK カーネル、操作が完了しました
- Irp WDK カーネルの完了、Irp の完了について
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ff55c4a8d527a88fcb357d634baba85f8ac2fd1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837068"
---
# <a name="completing-irps"></a>IRP の完了





"IRP の完了" は、"ドライバースタックのすべてのメンバーに i/o 操作を完了できるようにする" という簡潔な語句です。 IRP が完了すると、i/o マネージャーは、要求された i/o 操作が完了したことを開始アプリケーションに通知します。

ドライバーが IRP の処理を完了すると、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) (通常は[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチン内から) が呼び出されます。 これにより、i/o マネージャーは、より高いレベルのドライバーが IRP の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定しているかどうかを判断します。 その場合、チェーン内のすべての階層化ドライバーが IRP を完了するまで、各*Iocompletion*ルーチンが順番に呼び出されます。

すべてのドライバーが IRP を完了すると、i/o マネージャーは操作の元の要求元に状態を返します。 ドライバーで作成された IRP を設定する上位レベルのドライバーは、作成した IRP を解放するために*Iocompletion*ルーチンを提供する必要があることに注意してください。

このセクションでは、次のトピックについて説明します。

[IRP を完了するタイミング](when-to-complete-an-irp.md)

[ディスパッチルーチンでの Irp の完了](completing-irps-in-dispatch-routines.md)

[IoCompletion ルーチンの使用](using-iocompletion-routines.md)

 

 




