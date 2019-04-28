---
title: IoCompletion ルーチンの使用
description: IoCompletion ルーチンの使用
ms.assetid: 07a6e930-eef0-4408-9f71-55a827aa558e
keywords:
- IoCompletion ルーチン
- Irp WDK カーネル、IoCompletion ルーチンの完了
- ルーチンをディスパッチ Irp WDK カーネルを完了すると、
- ディスパッチ ルーチンの WDK カーネル、Irp の完了
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 253099033b27b7a0e2bcaf613c275e92882bf30c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364941"
---
# <a name="using-iocompletion-routines"></a>IoCompletion ルーチンの使用





高度なドライバーを IRP 固有にする方法は、下位レベルで監視する特定の要求を実行するドライバーは、1 つ以上を持つことができます[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン。 高度なドライバーのドライバーを削減する要求を送信する Irp を割り当てることがあります、 *IoCompletion*ルーチン。

最上位レベルまたは中間ドライバーの[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)または[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、を設定する最も可能性の高い*IoCompletion*下位レベルのドライバーでは、転送要求を非同期的に処理する必要がありますので、IRP のルーチンです。

ドライバー スタックの最下位レベルのドライバーを登録できません*IoCompletion*ルーチン。

ドライバーは一般に登録しないで*IoCompletion* Irp のルーチンが同期 I/O 操作に関連付けられています。 たとえばより高度なドライバーの[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンが IRP を使用して、割り当てることができる[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318). この場合は、ディスパッチ ルーチン通常は登録されません、 *IoCompletion*ルーチンが同期処理される一般にデバイスの制御が要求されるためです。 ドライバーが代わりに、割り当てるし、イベント オブジェクトを初期化し、その*DispatchDeviceControl*ルーチンがドライバーに割り当てられた Irp の送信時に初期化するイベントを待機できます。 通常より高度なドライバーは登録されません、 *IoCompletion*で割り当てられた IRP の日常的な[ **IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)、同様の理由。

このセクションでは、次のトピックについて説明します。

[IoCompletion ルーチンを登録します。](registering-an-iocompletion-routine.md)

[IoCompletion ルーチンを実装します。](implementing-an-iocompletion-routine.md)

 

 




