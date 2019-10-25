---
title: システムのキャンセル スピン ロックの使用
description: システムのキャンセル スピン ロックの使用
ms.assetid: dd3cf1e7-8ecc-4721-9160-86bf928687e4
keywords:
- キャンセルスピンロック WDK カーネル
- スピンロック WDK カーネル
- システムのキャンセルスピンロックの WDK カーネル
- STATUS_CANCELLED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef5450e4f50cac20440edfcae29caa671fba3288
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835846"
---
# <a name="using-the-systems-cancel-spin-lock"></a>システムのキャンセル スピン ロックの使用





システムには、特定のシステムルーチンが呼び出されたときに取得または解放される、1回の*キャンセルスピンロック*が用意されています。

状態\_キャンセルされた IRP を完了する可能性のあるすべてのルーチンなど、キャンセル可能な Irp の状態を変更するドライバールーチンは、このセクションのガイドラインに従って、システムキャンセルスピンロックを取得して解放する必要があります。

I/o マネージャーが提供するデバイスキューを使用するドライバーでは、IRP の取り消し可能な状態を変更する*キャンセル*ルーチン以外のドライバールーチンは、まず[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))を呼び出してシステムキャンセルスピンロックを取得する必要があります。

キャンセルスピンロックを取得すると、その IRP の取り消し可能な状態を呼び出し元だけが変更できるようになります。 呼び出し元がスピンロックを保持している間、i/o マネージャーはその IRP のドライバーの*キャンセル*ルーチンを呼び出すことができません。 同様に、 *DispatchCleanup*ルーチンなどの別のドライバールーチンは、その IRP の取り消し可能な状態を同時に変更することはできません。

Irp の独自のキューを管理し、ドライバーによって提供されるスピンロックを使用してキューアクセスを同期するドライバーでは、ドライバールーチンは[**Iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出す前にキャンセルスピンロックを取得する必要はありません。 ただし、これらのドライバーは、 **Iosetcancelroutine**が返す*キャンセル*ルーチンポインターを確認して、*キャンセル*ルーチンが既に開始されているかどうかを確認する必要があります。 詳細について[は、「ドライバーによって提供されるスピンロックの使用](using-a-driver-supplied-spin-lock.md)」を参照してください。

**IoAcquireCancelSpinLock**を呼び出すドライバールーチンは、できるだけ早く**IoReleaseCancelSpinLock**を呼び出す必要があります。

スピンロックを保持した状態で、ドライバーが IRP で[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出すことはできません。 スピンロックを保持した状態で IRP を完了しようとすると、デッドロックが発生する可能性があります。

 

 




