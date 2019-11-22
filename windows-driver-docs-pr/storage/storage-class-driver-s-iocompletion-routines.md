---
title: 記憶域クラス ドライバーの IoCompletion ルーチン
description: 記憶域クラス ドライバーの IoCompletion ルーチン
ms.assetid: 03cf50be-1b7d-4e5b-8ee5-bbdef860d893
keywords:
- IoCompletion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9747be4f8e0fea0eb5f623a355069e79f0b98e92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845631"
---
# <a name="storage-class-drivers-iocompletion-routines"></a>記憶域クラス ドライバーの IoCompletion ルーチン


## <span id="ddk_storage_class_drivers_iocompletion_routines_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_IOCOMPLETION_ROUTINES_KG"></span>


ストレージクラスドライバーは、1つ以上の[**iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを持つ必要があります。ただし、ドライバーがポートドライバーに送信するすべての IRP の完了を同期的に待機し、必要に応じて要求を再試行し、ディスパッチまたは*buildrequest*ルーチン内から SRBs のメモリを解放します。 すべての IRP を同期的に処理することで、クラスドライバーのパフォーマンスが低下することに注意してください。 さらに、システムページファイルを保持する可能性があるデバイスのストレージクラスドライバーは、すべての転送要求を非同期に処理する必要があるため、読み取り/書き込み要求に対して*Iocompletion*ルーチンが必要です。

「[ストレージクラスドライバーの BuildRequest ルーチン](storage-class-driver-s-buildrequest-routine.md)」で説明されているように、ストレージクラスドライバーは、ルックアサイドリストに戻すか、非ページプールに戻すかにかかわらず、SRBs に割り当てたメモリを解放する役割を担います。 他の上位レベルのカーネルモードドライバーと同様に、これらのドライバーは、[ストレージクラスドライバーの SplitTransferRequest ルーチン](storage-class-driver-s-splittransferrequest-routine.md)に記載されているように、転送要求を分割するための irp など、割り当てられる irp をすべて解放する役割も担います。

クラスドライバーの*Iocompletion*ルーチンは、最終的に i/o 状態ブロックが設定され、元の IRP を完了するようにします。 IRP を完了するには、「[ディスパッチルーチンでの irp の完了](https://docs.microsoft.com/windows-hardware/drivers/kernel/completing-irps-in-dispatch-routines)」で説明されているように、SRB の**ScsiStatus** Member または**senseinfobuffer**メンバーで返されたエラーを NTSTATUS 型の値に変換したり、エラーをログに記録したりすることができます.

要求の処理中に特定の種類のエラーが発生した場合、ストレージポートドライバーはターゲット論理ユニット (LU) の内部キューをフリーズし、要求の完了時に、SRB\_STATUS\_QUEUE\_凍結します。 そのため、クラスドライバーは通常、デバイスの i/o 要求のキューの状態を変更する内部ルーチンを備えています。 詳細については、「[ストレージクラスドライバーの ReleaseQueue ルーチン](storage-class-driver-s-releasequeue-routine.md)」を参照してください。

ドライバーの*Buildrequest*ルーチンが要求の要求に関する情報を返すことを要求した場合、その*iocompletion*ルーチンは、内部の*解釈 requestsense*ルーチンを呼び出すか、同じを実装します。機能インライン。 詳細については、「[ストレージクラスドライバーの解釈 Requestsense ルーチン](storage-class-driver-s-interpretrequestsense-routine.md)」を参照してください。

ストレージクラスドライバーは、ターゲットコントローラーのエラー、バスのリセット、または要求のタイムアウトによって失敗した要求を再試行する役割を担います。 ポートドライバーが、そのようなエラーを示すために**Srbstatus**が設定された特定の要求を返すと、クラスドライバーは、 *iocompletion*ルーチンを*iocompletion*ルーチンから呼び出すことも、場合によっては、その*解釈*されるルーチンから呼び出すこともできます。 詳細については、「[ストレージクラスドライバーの RetryRequest ルーチン](storage-class-driver-s-retryrequest-routine.md)」を参照してください。

*Iocompletion*ルーチンに関する一般的な情報については、「 [irp の完了](https://docs.microsoft.com/windows-hardware/drivers/kernel/completing-irps)」を参照してください。

 

 




