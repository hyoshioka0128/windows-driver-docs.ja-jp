---
title: StartIo ルーチンを使用していないドライバーのキャンセル ルーチン
description: StartIo ルーチンを使用していないドライバーのキャンセル ルーチン
ms.assetid: c6e1a05e-28ed-4f42-8678-55f01303b312
keywords:
- Irp、StartIo ルーチンのキャンセル
- キャンセル ルーチン、StartIo ルーチン
- StartIo ルーチン、キャンセル ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce3e593a7f51e9614d4e11409b5f56bcc080b9ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377238"
---
# <a name="cancel-routines-in-drivers-without-startio-routines"></a>StartIo ルーチンを使用していないドライバーのキャンセル ルーチン





I/O マネージャーが保持、 **CurrentIrp**フィールドに関連付けられているデバイスのキュー オブジェクトの Irp がキューに置かれた場合にのみ、デバイス オブジェクト。

ドライバーがない[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンが Irp の独自の内部キューを管理します。 このようなドライバー、 [*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel) 、入力のどちらである IRP ルーチンを呼び出すことができます、 **CurrentIrp**入力対象のデバイス オブジェクトも、ドライバーは IRP の内部のキューです。 ドライバーが IRP を現在処理中とがありますが自身の状態を維持する必要があります、*キャンセル*キューの各ルーチン。 Executive スピン ロックによって、内部キューを保護する必要があるために、ドライバーの内部キューは、インタロックされたキューになります。

ときに、ドライバーの*キャンセル*ルーチンを呼び出すと、通常は次のこと。

1.  呼び出し[ **IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を渡して、 **Irp -&gt;CancelIrql**します。

2.  インタロックされたキューを保護し、キューでは IRP を検索する方法について説明します、スピン ロックを取得**Irp -&gt;キャンセル**に設定**TRUE**します。

    -   インタロックされたキューには、このような IRP が見つかると、そのデキュー、キューを保護するスピン ロックを解放、w で IRP の I/O の状態のブロック設定

        ステータス\_の中止された**状態**の場合は 0 と**情報**、[次へ] のキューに置かれた IRP の呼び出しを開始[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)とキャンセルの IRP では、および返します control

    -   このような IRP が見つからない場合、*キャンセル*ルーチンが保持していることと、制御が戻りますスピン ロックは解放されます。

        ドライバーは通常、IRP がキューに配置しない場合、IRP が既に開始されて、入力の場合は、その I/O 処理が前提としています。

ドライバーを*キャンセル*ルーチンが処理できる[ **IRP\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)も要求します。 参照してください[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)の詳細については**IRP\_MJ\_クリーンアップ**要求。

 

 




