---
title: 記憶域クラス ドライバーの BuildRequest ルーチン
description: 記憶域クラス ドライバーの BuildRequest ルーチン
ms.assetid: 2ba26628-4862-440c-b8f1-dd983cf9923b
keywords:
- BuildRequest
- I/o スタックの場所 WDK ストレージ
- WDK ストレージの再試行要求
- SCSI 要求感知 WDK ストレージ
- 要求 sense WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd6f9d63a9514c62ba62d4ab116daca462bec6b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844754"
---
# <a name="storage-class-drivers-buildrequest-routine"></a>記憶域クラス ドライバーの BuildRequest ルーチン


## <span id="ddk_storage_class_drivers_buildrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_BUILDREQUEST_ROUTINE_KG"></span>


すべての上位レベルのカーネルモードドライバーと同様に、記憶域の[周辺機器への要求を処理](handling-requests-to-storage-peripherals.md)するときに、ストレージクラスドライバーは、次の下位のドライバーに対して IRP の i/o スタックの場所を設定する必要があります。 システムが提供するポートドライバーの SRBs を使用してクラスドライバーが設定する Irp では、ポートドライバーの i/o スタックの場所は次のように設定されます。

-   **MajorFunction**には、IRP\_MJ\_SCSI が含まれています

-   Srb には、SRB へのポインターが含まれてい**ます。**

各クラスドライバーは、SRBs にメモリを割り当て、基になるストレージポートドライバー用に CDBs を設定する役割を担います。 クラスドライバーでは、SRBs のルックアサイドリストを設定**するか、** 非ページメモリに対して**Exallocatepool**を呼び出すことができます。 ルックアサイドリストと非ページプールの使用の詳細については、「[ルックアサイドリストの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-lookaside-lists)」を参照してください。

プールからメモリを割り当てるか、ドライバーによって作成されたルックアサイドリストからメモリを割り当てるかにかかわらず、すべてのストレージクラスドライバーは、SRBs に割り当てられたメモリを解放する役割を担います。 ストレージクラスドライバーの*Iocompletion*ルーチン ([ストレージクラスドライバーの iocompletion ルーチン](storage-class-driver-s-iocompletion-routines.md)) で説明されているように、通常は、SRBs に割り当てられたメモリをルックアサイドリストに解放します。

クラスドライバーの*Buildrequest*ルーチンは、デバイスと通信するように設定されている CDB の長さなど、SRB メンバーに適切な値を設定する必要があります。 要求に関する情報を返す要求や、ドライバーが再試行しなければならない可能性がある要求については、IRP に*Iocompletion*ルーチンを設定します。 読み取り要求または書き込み要求の場合、 **Srbflags**は適切な転送方向、SRB\_フラグ\_データ\_または SRB\_フラグ\_データ\_出力されます。

*Buildrequest*ルーチンは、 *Sendsrbsynchronous*ルーチンと*SendSrbAsynchronous*ルーチンのペアを使用して SRB を設定する責任を共有する場合があります。 つまり、 *Buildrequest*ルーチンは、すべての要求に対して一般的に設定されている SRB メンバーを設定できました。一方、 *Sendsrbxxx*ルーチンでは、各種類の要求に対して SRB 値が適切に設定されます。 IRP が*SendSrbAsynchronous*ルーチンからポートドライバーに渡される場合は、ドライバーによって提供される*iocompletion*ルーチンを使用して irp を設定する必要があります。

クラスドライバーが読み込まれると、最も多くの SRBs が設定されます。これにより、**関数**メンバーが SRB\_関数に設定され\_\_SCSI が実行され、バスを介して送信されるデバイス i/o 要求が示されます。

システム定義の SRB メンバーとその値の詳細については、「 [**SCSI\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)」を参照してください。

### <a name="span-idsetting_up_srbs_for_request_sensespanspan-idsetting_up_srbs_for_request_sensespanspan-idsetting_up_srbs_for_request_sensespansetting-up-srbs-for-request-sense"></a><span id="Setting_Up_SRBs_for_Request_Sense"></span><span id="setting_up_srbs_for_request_sense"></span><span id="SETTING_UP_SRBS_FOR_REQUEST_SENSE"></span>Request Sense の SRBs の設定

クラスドライバーは、ターゲットコントローラーからチェック条件が返されたときに、ポートドライバーが SCSI の要求意味または同等の情報を返すように要求できます。 これを行うために、クラスドライバーは**Senseinfobuffer**ポインターと**Senseinfobufferlength**を SRB に設定します。これにより、ポートドライバーは、チェック条件が発生した場合に要求に関する情報を返すことができます。 ポートドライバーは、SRB\_STATUS を使用して**Srbstatus**メンバーを設定することによって要求センス情報が返されたことを示しています。これは、IRP を返したときに有効\_\_ます。 の*解釈*の詳細については、「[ストレージクラスドライバーの解釈 requestsense ルーチン](storage-class-driver-s-interpretrequestsense-routine.md)」を参照してください。

### <a name="span-idretriesspanspan-idretriesspanspan-idretriesspanretries"></a><span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>試行

ストレージクラスドライバーは、ターゲット/コントローラーのエラー、バスのリセット、または要求のタイムアウトによって失敗した要求を再試行する役割を担います。 そのため、多くのクラスドライバーは、IRP の i/o スタックの場所に再試行回数を保持します。 このようなクラスドライバーの*Buildrequest*ルーチンでは、指定された要求の再試行制限を初期化する前に、その要求の*iocompletion*ルーチンを設定し、IRP をポートドライバーに送信することもできます。 *Retryrequest*ルーチンの詳細については、「[ストレージクラスドライバーの retryrequest ルーチン](storage-class-driver-s-retryrequest-routine.md)」を参照してください。

 

 




