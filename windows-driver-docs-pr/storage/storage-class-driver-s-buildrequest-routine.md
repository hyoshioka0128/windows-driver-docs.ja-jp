---
title: 記憶域クラス ドライバーの BuildRequest ルーチン
description: 記憶域クラス ドライバーの BuildRequest ルーチン
ms.assetid: 2ba26628-4862-440c-b8f1-dd983cf9923b
keywords:
- BuildRequest
- I/O スタックの場所の WDK ストレージ
- WDK 記憶域の要求を再試行しています
- SCSI 要求意味 WDK ストレージ
- 要求の意味が WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7587cc600364d89fb54b9f7544edcdaafbcefaba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368222"
---
# <a name="storage-class-drivers-buildrequest-routine"></a>記憶域クラス ドライバーの BuildRequest ルーチン


## <span id="ddk_storage_class_drivers_buildrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_BUILDREQUEST_ROUTINE_KG"></span>


上位レベルのすべてのカーネル モード ドライバーなど、記憶域クラス ドライバーは、次の下位のドライバーの IRP の I/O スタックの場所を設定する必要がありますと[記憶域周辺機器への要求の処理](handling-requests-to-storage-peripherals.md)します。 クラス ドライバーを設定する使いなれたシステム提供のポートのドライバーの Irp では、ポート ドライバーの I/O スタックの場所は次のように設定します。

-   **MajorFunction** IRP を含む\_MJ\_SCSI

-   **Parameters.Scsi.Srb** SRB へのポインターが含まれています

各クラス ドライバーは、それらを設定する Cdb で基になる記憶域ポート ドライバーともされる Srb のメモリの割り当てを担当します。 クラス ドライバーとそのされる Srb のルック アサイド リストを設定できますか**ExInitializeNPageLookasideList**呼び出したり**ExAllocatePool**非ページ メモリ。 参照してください[ルック アサイド リストを使用した](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-lookaside-lists)ルック アサイド リストおよび非ページ プールの使用に関する詳細。

プールから、またはドライバーが作成したルック アサイド リストから、メモリを割り当てます、かどうかすべての記憶域クラス ドライバーはされる Srb のメモリを解放します。 記憶域クラス ドライバーの*IoCompletion*で説明されているルーチン[記憶域クラス ドライバー IoCompletion ルーチン](storage-class-driver-s-iocompletion-routines.md)、通常される Srb ルック アサイド リストに戻るに割り当てられたメモリを解放します。

クラス ドライバーの*BuildRequest*ルーチンは、デバイスとの通信に設定されている CDB の長さを含む SRB メンバーで適切な値を設定する必要があります。 設定を要求センス情報や、ドライバーは、再試行する必要がありますを返す要求の場合、 *IoCompletion* IRP の日常的な。 読み取りまたは書き込み要求を Or、 **SrbFlags**で、適切な転送の方向、SRB\_フラグ\_データ\_IN または SRB\_フラグ\_データ\_それぞれします。

A *BuildRequest*ルーチンが、SRB のペアを設定する責任を共有*SendSrbSynchronous*と*SendSrbAsynchronous*ルーチン。 つまり、 *BuildRequest*ルーチンよく、すべての要求に対して設定される SRB メンバーを設定中に、 *SendSrbXxx* SRB の値を設定要求の種類ごとにのみ関連する各ルーチン。 ポート ドライバーに IRP が渡されると、 *SendSrbAsynchronous* 、日常的な IRP ようを設定すると、ドライバーによって提供される*IoCompletion*ルーチン。

ほとんどされる Srb 設定クラス ドライバーが読み込まれた後、**関数**メンバー SRB に設定\_関数\_EXECUTE\_SCSI バス経由で送信するデバイスの I/O 要求を示します。

システム定義の SRB メンバーとその値の詳細については、次を参照してください。 [ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)します。

### <a name="span-idsettingupsrbsforrequestsensespanspan-idsettingupsrbsforrequestsensespanspan-idsettingupsrbsforrequestsensespansetting-up-srbs-for-request-sense"></a><span id="Setting_Up_SRBs_for_Request_Sense"></span><span id="setting_up_srbs_for_request_sense"></span><span id="SETTING_UP_SRBS_FOR_REQUEST_SENSE"></span>要求の意味のされる Srb の設定

クラスのドライバーでは、ポート ドライバーがターゲット コント ローラーには、条件の確認が返されるときに、SCSI 要求意味またはそれと同等の情報を返すことを要求できます。 これを行うには、クラス ドライバーの設定**SenseInfoBuffer**ポインターと**SenseInfoBufferLength** SRB のためポート ドライバー戻ることができます要求意味については、条件が発生した場合。 ポートのドライバーを設定して要求センス情報が返されることを示します、 **SrbStatus** SRB を持つメンバー\_状態\_AUTOSENSE\_IRP が返されるときに有効です。 詳細については*InterpretSenseInfo*ルーチンを参照してください[記憶域クラス ドライバー InterpretRequestSense ルーチン](storage-class-driver-s-interpretrequestsense-routine.md)します。

### <a name="span-idretriesspanspan-idretriesspanspan-idretriesspanretries"></a><span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>再試行

記憶域クラス ドライバーは、ターゲット/コント ローラーのエラー、バスのリセット、または要求タイムアウトが原因で失敗した要求を再試行します。 その結果、多くのクラス ドライバーは IRP の独自 I/O スタックの場所での再試行回数を維持します。 このようなクラス ドライバーの*BuildRequest*ルーチンが初期化することも、特定の要求の再試行回数の上限を設定する前にその*IoCompletion*ルーチンとポートのドライバーに IRP を送信します。 詳細については*RetryRequest*ルーチンを参照してください[記憶域クラス ドライバー RetryRequest ルーチン](storage-class-driver-s-retryrequest-routine.md)します。

 

 




