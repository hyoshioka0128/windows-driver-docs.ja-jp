---
title: システムのキャンセル スピン ロックの使用
description: システムのキャンセル スピン ロックの使用
ms.assetid: dd3cf1e7-8ecc-4721-9160-86bf928687e4
keywords:
- スピン ロック WDK カーネルをキャンセルします。
- スピン ロック WDK カーネル
- システムは、スピン ロック WDK カーネルをキャンセルします。
- STATUS_CANCELLED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de5d057827710875c458c933e3d7086e09e2d74
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387001"
---
# <a name="using-the-systems-cancel-spin-lock"></a>システムのキャンセル スピン ロックの使用





1 つに、システムは*スピン ロックをキャンセル*が取得または特定のシステム ルーチンを呼び出すときにリリースされました。

ステータスの IRP を完了することがありますすべてのルーチンを含む、キャンセル可能な Irp の状態を変更するドライバー ルーチン\_取り消された場合を取得およびこのセクションのガイドラインに従ってシステム キャンセル スピン ロックを解放する必要があります。

以外の I/O マネージャーが指定したデバイスのキュー、ドライバーの任意のルーチンを使用するドライバー、*キャンセル*IRP のキャンセル可能な状態を変更するルーチンを呼び出す必要がありますまず[ **IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))システム キャンセル スピン ロックを取得します。

キャンセルのスピン ロックの獲得により、呼び出し元だけがその IRP のキャンセル可能な状態を変更できます。 I/O マネージャーがドライバーを呼び出すことはできません、呼び出し元は、スピン ロックを保持しているときに*キャンセル*その IRP のルーチンです。 同様に、別のドライバーなど、日常的な*DispatchCleanup*ルーチンをその IRP のキャンセル可能な状態を変更することはできません同時に再試行してください。

Irp の独自のキューを管理し、ドライバーによって提供されるスピン ロックを使用して、キューのアクセスを同期するドライバー、ドライバー ルーチン必要はありません呼び出す前にキャンセル スピン ロックの取得を[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine). ただし、これらのドライバーを確認する必要があります、*キャンセル*日常的なポインターを**IoSetCancelRoutine**判断を返すかどうか、*キャンセル*ルーチンが既に開始します。 参照してください[Driver-Supplied スピン ロックを使用する](using-a-driver-supplied-spin-lock.md)詳細についてはします。

呼び出すドライバーのルーチン**IoAcquireCancelSpinLock**呼び出す必要があります**IoReleaseCancelSpinLock**できるだけ早くします。

ドライバーは呼び出す必要がありますしない[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP スピン ロックを保持しているときに使用します。 スピン ロックを保持しながら、IRP を完了しようとすると、デッドロックが起こります。

 

 




