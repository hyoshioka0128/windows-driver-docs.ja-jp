---
title: 完了ルーチンに関する制約
description: 完了ルーチンに関する制約
ms.assetid: 3873fd27-cfa8-414d-9437-c0789b20ff27
keywords:
- IRP 完了ルーチン WDK ファイルシステム、制約
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78ed54a0c334ec16d2d0bae56c6f7b9035289d7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841457"
---
# <a name="constraints-on-completion-routines"></a>完了ルーチンに関する制約


## <span id="ddk_constraints_on_completion_routines_if"></span><span id="DDK_CONSTRAINTS_ON_COMPLETION_ROUTINES_IF"></span>


次のガイドラインでは、ファイルシステムフィルタードライバーの完了ルーチンでの一般的なプログラミングエラーを回避する方法について簡単に説明します。

### <a name="span-idirql-related_constraintsspanspan-idirql-related_constraintsspanspan-idirql-related_constraintsspanirql-related-constraints"></a><span id="IRQL-Related_Constraints"></span><span id="irql-related_constraints"></span><span id="IRQL-RELATED_CONSTRAINTS"></span>IRQL に関連する制約

完了ルーチンは IRQL ディスパッチ\_レベルで呼び出すことができるため、次の制約が適用されます。

-   完了ルーチンは、 [**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)や[**obquerynamestring**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-obquerynamestring)など、低い IRQL を必要とするカーネルモードルーチンを安全に呼び出すことができません。

-   完了ルーチンで使用されるデータ構造は、非ページプールから割り当てられる必要があります。

-   完了ルーチンをページング可能にすることはできません。

-   完了ルーチンは、リソース、ミューテックス、または高速ミューテックスを取得できません。 ただし、スピンロックを取得することはできます。

### <a name="span-idchecking_the_pendingreturned_flagspanspan-idchecking_the_pendingreturned_flagspanspan-idchecking_the_pendingreturned_flagspanchecking-the-pendingreturned-flag"></a><span id="Checking_the_PendingReturned_Flag"></span><span id="checking_the_pendingreturned_flag"></span><span id="CHECKING_THE_PENDINGRETURNED_FLAG"></span>PendingReturned たフラグを確認しています

-   完了ルーチンがイベントを通知する場合を除き、 **Irp&gt;PendingReturned た**フラグを確認する必要があります。 このフラグが設定されている場合、完了ルーチンは[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出して、IRP を pending としてマークする必要があります。

-   完了ルーチンがイベントを通知する場合、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出すことはできません。

### <a name="span-idconstraints_on_returning_statusspanspan-idconstraints_on_returning_statusspanspan-idconstraints_on_returning_statusspanconstraints-on-returning-status"></a><span id="Constraints_on_Returning_Status"></span><span id="constraints_on_returning_status"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS"></span>ステータスを返す場合の制約

-   ファイルシステムフィルタードライバーの完了ルーチンでは、必要な\_処理\_\_の状態\_成功または状態のいずれかを返す必要があります。 その他のすべての NTSTATUS 値は、i/o マネージャーによって [状態]\_[成功] にリセットされます。

### <a name="span-idconstraints_on_returning_status_more_processing_requiredspanspan-idconstraints_on_returning_status_more_processing_requiredspanspan-idconstraints_on_returning_status_more_processing_requiredspanconstraints-on-returning-status_more_processing_required"></a><span id="Constraints_on_Returning_STATUS_MORE_PROCESSING_REQUIRED"></span><span id="constraints_on_returning_status_more_processing_required"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS_MORE_PROCESSING_REQUIRED"></span>ステータスを返すための制約\_\_処理\_必要があります

完了ルーチンがステータスを返す必要がある場合は、次の3つのケース\_\_処理\_必要があります。

-   対応するディスパッチルーチンが、完了ルーチンによってイベントが通知されるのを待機している場合。 この場合は、完了ルーチンが返された後に i/o マネージャーが IRP を途中で完了しないようにするために、ステータス\_より多くの\_処理\_必要があります。

-   完了ルーチンが IRP をワーカーキューにポストし、対応するディスパッチルーチンが状態\_PENDING を返した場合。 このケースでは、完了ルーチンが返された後に i/o マネージャーが IRP を途中で完了しないようにするために、ステータス\_より多く\_処理\_必要があります。

-   同じドライバーが[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)または[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)を呼び出すことによって IRP を作成したとき。 ドライバーは、上位レベルのドライバーからこの IRP を受信しなかったため、完了ルーチンで IRP を安全に解放できます。 [**Iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)を呼び出した後、完了ルーチンは、それ以上の完了処理が不要であることを示すために必要な\_処理\_のステータス\_を返す必要があります。

完了ルーチンは、oplock 操作に必要な\_処理\_より多くの\_状態を返すことはできません。 Oplock 操作を保留 (worker キューに投稿) することはできません。また、ディスパッチルーチンは、保留中のステータス\_を返すことはできません。

### <a name="span-idconstraints_on_posting_irps_to_a_work_queuespanspan-idconstraints_on_posting_irps_to_a_work_queuespanspan-idconstraints_on_posting_irps_to_a_work_queuespanconstraints-on-posting-irps-to-a-work-queue"></a><span id="Constraints_on_Posting_IRPs_to_a_Work_Queue"></span><span id="constraints_on_posting_irps_to_a_work_queue"></span><span id="CONSTRAINTS_ON_POSTING_IRPS_TO_A_WORK_QUEUE"></span>Irp を作業キューに投稿する際の制約

-   完了ルーチンが Irp を作業キューにポストする場合は、各 IRP をワーカーキューにポストする前に、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出す必要があります。 それ以外の場合は、IRP をデキューして別のドライバールーチンによって完了し、 **Iomarkirppending**の呼び出しが発生する前にシステムによって解放され、クラッシュが発生する可能性があります。

 

 




