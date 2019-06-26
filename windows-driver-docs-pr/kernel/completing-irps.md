---
title: IRP の完了
description: IRP の完了
ms.assetid: 4b4be95e-ebf5-4726-87fc-20c3e6c94f52
keywords:
- Irp WDK のカーネルの完了
- Irp WDK カーネルの完了
- 完成した Irp WDK カーネル
- I/O WDK カーネルでは、操作が完了しました
- Irp の完了についての Irp WDK カーネルの完了
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6992c9a14567b204bde1d7d76f6d01944217ebb0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383355"
---
# <a name="completing-irps"></a>IRP の完了





短縮形の語句を「IRP の完了」が意味の「ドライバー スタックのすべてのメンバーは、I/O 操作を完了できるようにします」。 IRP が完了すると、I/O マネージャーは、発信側のアプリケーション要求の I/O 操作が完了したことを通知します。

ドライバーは IRP の処理を完了したら、それを呼び出す[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) (通常内から、 [ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチン)。 これによりより高度なドライバーを設定するかどうかを判断する I/O マネージャー [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP のルーチンです。 場合は、各*IoCompletion*ルーチンが呼び出されると、さらに、チェーン内のすべての階層型ドライバーが IRP を完了するまでです。

すべてのドライバーは IRP が完了したら、I/O マネージャーは、操作の元の要求者にステータスを返します。 ドライバーが作成した IRP を設定するより高度なドライバーを指定する必要がありますに注意してください、 *IoCompletion*ルーチン IRP のリリースを作成します。

このセクションでは、次のトピックについて説明します。

[IRP を完了するタイミング](when-to-complete-an-irp.md)

[ディスパッチ ルーチンに Irp の完了](completing-irps-in-dispatch-routines.md)

[IoCompletion ルーチンを使用します。](using-iocompletion-routines.md)

 

 




