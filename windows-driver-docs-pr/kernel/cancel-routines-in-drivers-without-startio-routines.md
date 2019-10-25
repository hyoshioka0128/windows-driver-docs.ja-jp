---
title: StartIo ルーチンを使用していないドライバーのキャンセル ルーチン
description: StartIo ルーチンを使用していないドライバーのキャンセル ルーチン
ms.assetid: c6e1a05e-28ed-4f42-8678-55f01303b312
keywords:
- Irp の取り消し、StartIo ルーチン
- Cancel ルーチン、StartIo ルーチン
- StartIo ルーチン、キャンセルルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 645848b9c642d71cc7af5468e20f553ecb8c5e1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828568"
---
# <a name="cancel-routines-in-drivers-without-startio-routines"></a>StartIo ルーチンを使用していないドライバーのキャンセル ルーチン





I/o マネージャーは、関連付けられたデバイスキューオブジェクトで Irp がキューに置かれている場合にのみ、デバイスオブジェクト**の "状態**" フィールドを保持します。

[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンがないドライバーは、irp の内部キューを管理します。 このようなドライバーでは、入力ターゲットデバイス**オブジェクトの存在でも、ドライバー**の内部キュー内の irp でもない入力 IRP で、[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを呼び出すことができます。 ドライバーは、現在処理されている IRP に関する独自の状態を維持し、各キューの*キャンセル*ルーチンを保持する必要があります。 内部キューは executive スピンロックによって保護されている必要があるため、ドライバーの内部キューはインタロックされたキューである必要があります。

ドライバーの*キャンセル*ルーチンが呼び出されると、通常は次のように実行されます。

1.  [**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を呼び出し、 **Irp-&gt;CancelIrql**を渡します。

2.  インタロックされたキューを保護し、Irp を検出するためにキューにステップインするスピンロックを取得します。このロックは、 **&gt;Cancel**が**TRUE**に設定されています。

    -   このような IRP がインタロックされたキューで見つかった場合、デキュー it は、キューを保護するスピンロックを解放し、IRP の i/o 状態ブロックを w で設定します。

        状態**の状態と** **情報**が0の場合は\_が取り消され、次のキューに入っている irp が開始され、取り消された irp で[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)が呼び出され、制御が返されます

    -   このような IRP が見つからない場合、*キャンセル*ルーチンは、保持しているすべてのスピンロックを解放し、制御を返します。

        通常、このドライバーは、IRP がキューに登録されていない場合、入力 IRP の i/o 処理が既に開始されていると想定しています。

*キャンセル*ルーチンが含まれているドライバーは、 [**IRP\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)要求も処理できます。 **IRP\_MJ\_クリーンアップ**要求の詳細については、「 [*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 」を参照してください。

 

 




