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
ms.openlocfilehash: 9621f371bf6bf3bb64b2670711d7c2b010a0ade5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343690"
---
# <a name="completing-irps"></a>IRP の完了





短縮形の語句を「IRP の完了」が意味の「ドライバー スタックのすべてのメンバーは、I/O 操作を完了できるようにします」。 IRP が完了すると、I/O マネージャーは、発信側のアプリケーション要求の I/O 操作が完了したことを通知します。

ドライバーは IRP の処理を完了したら、それを呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) (通常内から、 [ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)ルーチン)。 これによりより高度なドライバーを設定するかどうかを判断する I/O マネージャー [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP のルーチンです。 場合は、各*IoCompletion*ルーチンが呼び出されると、さらに、チェーン内のすべての階層型ドライバーが IRP を完了するまでです。

すべてのドライバーは IRP が完了したら、I/O マネージャーは、操作の元の要求者にステータスを返します。 ドライバーが作成した IRP を設定するより高度なドライバーを指定する必要がありますに注意してください、 *IoCompletion*ルーチン IRP のリリースを作成します。

このセクションでは、次のトピックについて説明します。

[IRP を完了するタイミング](when-to-complete-an-irp.md)

[ディスパッチ ルーチンに Irp の完了](completing-irps-in-dispatch-routines.md)

[IoCompletion ルーチンを使用します。](using-iocompletion-routines.md)

 

 




