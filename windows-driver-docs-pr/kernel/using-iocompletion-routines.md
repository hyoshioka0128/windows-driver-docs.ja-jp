---
title: IoCompletion ルーチンの使用
description: IoCompletion ルーチンの使用
ms.assetid: 07a6e930-eef0-4408-9f71-55a827aa558e
keywords:
- IoCompletion ルーチン
- Irp WDK カーネル、IoCompletion ルーチンを完了する
- Irp WDK カーネル、ディスパッチルーチンを完了する
- ディスパッチルーチン WDK カーネル、Irp の完了
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b60c07b87a4fa460c7c9a629d43fe679b1f99308
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838353"
---
# <a name="using-iocompletion-routines"></a>IoCompletion ルーチンの使用





特定の要求を実行する下位レベルのドライバーが1つ以上の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを持つことができるように、IRP 固有のベースのドライバーを監視する上位のドライバー。 低いドライバーに要求を送信するための Irp を割り当てる上位レベルのドライバーには、 *Iocompletion*ルーチンが必要です。

最上位レベルまたは中間のドライバーの[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)または[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでは、ほとんどの場合、IRP の*iocompletion*ルーチンを設定します。これは、下位レベルのドライバーでは、転送要求を非同期に処理する必要があるためです。

ドライバースタック内の最下位レベルのドライバーは、 *Iocompletion*ルーチンを登録できません。

通常、ドライバーは、同期 i/o 操作に関連付けられている Irp に対して*Iocompletion*ルーチンを登録しません。 たとえば、上位レベルのドライバーの[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を使用して IRP を割り当てることができます。 この場合、通常、デバイス制御要求は同期的に処理されるため、ディスパッチルーチンは*Iocompletion*ルーチンを登録しません。 代わりに、ドライバーはイベントオブジェクトを割り当てて初期化することができます。また、 *DispatchDeviceControl*ルーチンは、ドライバーによって割り当てられた irp で送信されるときにイベントが初期化されるのを待機できます。 通常、上位レベルのドライバーは、同じ理由で、 [**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)で割り当てられた IRP の*iocompletion*ルーチンを登録しません。

このセクションは、次のトピックで構成されています。

[IoCompletion ルーチンの登録](registering-an-iocompletion-routine.md)

[IoCompletion ルーチンの実装](implementing-an-iocompletion-routine.md)

 

 




