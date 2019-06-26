---
title: 記憶域フィルター ドライバーの IoCompletion ルーチン
description: 記憶域フィルター ドライバーの IoCompletion ルーチン
ms.assetid: 1a27598b-7113-4f95-8777-bbb10003c268
keywords:
- 記憶域フィルター ドライバー WDK、IoCompletion
- フィルター ドライバー WDK ストレージ、IoCompletion
- SFD WDK ストレージ、IoCompletion
- IoCompletion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf4038f221fb05351b62a11546cbf3f875dd57d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376686"
---
# <a name="storage-filter-drivers-iocompletion-routines"></a>記憶域フィルター ドライバーの IoCompletion ルーチン


## <span id="ddk_storage_filter_drivers_iocompletion_routines_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_IOCOMPLETION_ROUTINES_KG"></span>


記憶域フィルター ドライバーの[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンは、下位レベルのドライバー (ポート、クラス、および追加のフィルター ドライバー、存在する場合) が呼び出されたときに呼び出されます[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。 *IoCompletion*ストレージ フィルター ドライバー (SFD) のルーチンを返す必要があります**状態\_詳細\_処理\_REQUIRED**の処理を完了するドライバーによって割り当てられたの IRP では、または、SFD は IRP を再利用が完了する前に、元の IRP を保持します。

などの他の高度なドライバー、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) 、SFD のルーチンが通話を担当[ **IoFreeIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)いずれかを解放するにはドライバーを IRP*ディスパッチ*ルーチンで作成された[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)または[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest).

SFD を提供することによって、そのデバイス、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)から次の下位ドライバーに送信する Irp の日常的な*ディスパッチ*ルーチン。 SFD を取得し、非標準の形式でデータを処理するデバイスが具体的には、必要があります、 *TranslateDataIn*ルーチンを呼び出すからその*IoCompletion*転送要求のルーチンこのようなデバイスからシステム メモリにします。

注このような*TranslateDataIn* IRQL でルーチンを呼び出すとディスパッチを = =\_レベルと任意のスレッド コンテキストでします。 そのため、これには、ドライバーはデータを返します。 バッファーは非ページ プールである必要がありますまたはロックダウンする必要があり、仮想アドレスの非ページ システム領域、マップを使用してアクセスします。 安全に発生した IRQL でユーザーが指定したバッファーにアクセスする方法の詳細については、次を参照してください。[メソッドにアクセスするデータ バッファーの](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)します。

一般に、ストレージのフィルター ドライバーを指定する必要があります、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)クラス ドライバーのと同じ機能を日常的な*IoCompletion* Irp のルーチンをフィルター ドライバーは、される Srb と Cdb を設定します。 いずれかまたはすべてのストレージのフィルター ドライバーがその結果、必要があります、 *ReleaseQueue*、 *InterpretRequestSense*、または*RetryRequest*ルーチンから呼び出すことが、記憶域クラス ドライバー *IoCompletion*ルーチン。

詳細については*InterpretRequestSense*、 *RetryRequest*、および*ReleaseQueue*ルーチンを参照してください[ストレージ クラス ドライバー](storage-class-drivers.md). 一般的な要件の詳細については[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンを参照してください[IoCompletion ルーチンを使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-iocompletion-routines)します。

 

 




