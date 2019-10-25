---
title: 記憶域フィルター ドライバーの IoCompletion ルーチン
description: 記憶域フィルター ドライバーの IoCompletion ルーチン
ms.assetid: 1a27598b-7113-4f95-8777-bbb10003c268
keywords:
- ストレージフィルタードライバー WDK、IoCompletion
- フィルタードライバー WDK storage、IoCompletion
- SFD WDK storage、IoCompletion
- IoCompletion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b77ac503fe610afc21a39cec42719fb29f614a47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844469"
---
# <a name="storage-filter-drivers-iocompletion-routines"></a>記憶域フィルター ドライバーの IoCompletion ルーチン


## <span id="ddk_storage_filter_drivers_iocompletion_routines_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_IOCOMPLETION_ROUTINES_KG"></span>


低レベルドライバー (ポート、クラス、および追加のフィルタードライバーが存在する場合) が[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出したときに、ストレージフィルタードライバーの[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが呼び出されます。 記憶域フィルタードライバー (SFD) の*iocompletion*ルーチンは、ドライバーによって割り当てられた IRP の完了処理を防止するために**必要な\_\_処理**、または sfd がある場合は元の IRP を保持するために、状態\_返す必要があります。IRP を再利用してから完了します。

他の上位レベルのドライバーと同様に、SFD の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンは、 [**iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)を呼び出して、 [**ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) [**で作成されたドライバーのディスパッチルーチンである任意の IRP を解放します。IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)。

SFD は、デバイスによっては、その*ディスパッチ*ルーチンから次の下位のドライバーに送信する Irp の[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを提供する場合があります。 特に、非標準の形式でデータを取得して処理するデバイスでは、このようなデバイスからシステムメモリへの転送要求に対して、その*Iocompletion*ルーチンから*TranslateDataIn*ルーチンを呼び出す必要がある場合があります。

このような*TranslateDataIn*ルーチンは、IRQL = = ディスパッチ\_レベルで任意のスレッドコンテキストで呼び出されることに注意してください。 このため、ドライバーがデータを返すバッファーは、非ページプールに配置されているか、または、割り当てられた非ページシステム領域の仮想アドレスを使用してロックダウンされ、アクセス可能である必要があります。 発生した IRQL でユーザーが指定したバッファーに安全にアクセスする方法の詳細については、「[データバッファーにアクセスするためのメソッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)」を参照してください。

一般に、ストレージフィルタードライバーは、フィルタードライバーによって SRBs と CDBs が設定される Irp のクラスドライバーの*iocompletion*ルーチンと同じ機能を持つ[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを提供する必要があります。 そのため、ストレージフィルタードライバーには、ストレージクラスドライバーの*Iocompletion*ルーチンから呼び出すことができる*releasequeue*、*解釈 Requestsense*、または*retryrequest*ルーチンが含まれている場合があります。

*解釈 Requestsense*、 *retryrequest*、および*releasequeue*ルーチンの詳細については、「[ストレージクラスドライバー](storage-class-drivers.md)」を参照してください。 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンの一般的な要件の詳細については、「 [Iocompletion ルーチンの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-iocompletion-routines)」を参照してください。

 

 




