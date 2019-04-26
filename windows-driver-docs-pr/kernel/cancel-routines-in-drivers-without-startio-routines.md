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
ms.openlocfilehash: cee9b06809bc16e81acf960aade0998eda1a2ced
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338719"
---
# <a name="cancel-routines-in-drivers-without-startio-routines"></a>StartIo ルーチンを使用していないドライバーのキャンセル ルーチン





I/O マネージャーが保持、 **CurrentIrp**フィールドに関連付けられているデバイスのキュー オブジェクトの Irp がキューに置かれた場合にのみ、デバイス オブジェクト。

ドライバーがない[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンが Irp の独自の内部キューを管理します。 このようなドライバー、 [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742) 、入力のどちらである IRP ルーチンを呼び出すことができます、 **CurrentIrp**入力対象のデバイス オブジェクトも、ドライバーは IRP の内部のキューです。 ドライバーが IRP を現在処理中とがありますが自身の状態を維持する必要があります、*キャンセル*キューの各ルーチン。 Executive スピン ロックによって、内部キューを保護する必要があるために、ドライバーの内部キューは、インタロックされたキューになります。

ときに、ドライバーの*キャンセル*ルーチンを呼び出すと、通常は次のこと。

1.  呼び出し[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)を渡して、 **Irp -&gt;CancelIrql**します。

2.  インタロックされたキューを保護し、キューでは IRP を検索する方法について説明します、スピン ロックを取得**Irp -&gt;キャンセル**に設定**TRUE**します。

    -   インタロックされたキューには、このような IRP が見つかると、そのデキュー、キューを保護するスピン ロックを解放、w で IRP の I/O の状態のブロック設定

        ステータス\_の中止された**状態**の場合は 0 と**情報**、[次へ] のキューに置かれた IRP の呼び出しを開始[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)とキャンセルの IRP では、および返します control

    -   このような IRP が見つからない場合、*キャンセル*ルーチンが保持していることと、制御が戻りますスピン ロックは解放されます。

        ドライバーは通常、IRP がキューに配置しない場合、IRP が既に開始されて、入力の場合は、その I/O 処理が前提としています。

ドライバーを*キャンセル*ルーチンが処理できる[ **IRP\_MJ\_クリーンアップ**](https://msdn.microsoft.com/library/windows/hardware/ff550718)も要求します。 参照してください[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)の詳細については**IRP\_MJ\_クリーンアップ**要求。

 

 




