---
title: 完了ルーチンに関する制約
description: 完了ルーチンに関する制約
ms.assetid: 3873fd27-cfa8-414d-9437-c0789b20ff27
keywords:
- IRP の完了ルーチン WDK ファイル システム、制約
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef0e4a1b84b672d7a5f0c21e90c8d7a75ba24ded
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359400"
---
# <a name="constraints-on-completion-routines"></a>完了ルーチンに関する制約


## <span id="ddk_constraints_on_completion_routines_if"></span><span id="DDK_CONSTRAINTS_ON_COMPLETION_ROUTINES_IF"></span>


次のガイドラインでは、ファイル システム フィルター ドライバー完了ルーチンの一般的なプログラミング エラーを回避する方法について簡単に説明します。

### <a name="span-idirql-relatedconstraintsspanspan-idirql-relatedconstraintsspanspan-idirql-relatedconstraintsspanirql-related-constraints"></a><span id="IRQL-Related_Constraints"></span><span id="irql-related_constraints"></span><span id="IRQL-RELATED_CONSTRAINTS"></span>IRQL 関連の制約

IRQL のディスパッチの完了ルーチンを呼び出すことができますので\_次の制約の対象は、レベル。

-   完了ルーチンが低いかどうかなどを必要とするカーネル モードのルーチンを安全に呼び出すことはできません[ **IoDeleteDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549083)または[ **ObQueryNameString** ](https://msdn.microsoft.com/library/windows/hardware/ff550990).

-   完了ルーチンで使用される任意のデータ構造は、非ページ プールから割り当てられる必要があります。

-   ページング可能な完了ルーチンを作成できません。

-   完了ルーチンには、リソース、ミュー テックス、または高速なミュー テックスを取得できません。 ただし、スピン ロックを取得することができます。

### <a name="span-idcheckingthependingreturnedflagspanspan-idcheckingthependingreturnedflagspanspan-idcheckingthependingreturnedflagspanchecking-the-pendingreturned-flag"></a><span id="Checking_the_PendingReturned_Flag"></span><span id="checking_the_pendingreturned_flag"></span><span id="CHECKING_THE_PENDINGRETURNED_FLAG"></span>PendingReturned フラグのチェック

-   確認する必要があります完了ルーチンでは、イベントを通知、しない限り、 **Irp -&gt;PendingReturned**フラグ。 このフラグが設定されている場合、完了ルーチンを呼び出す必要があります[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) IRP が保留中としてマークします。

-   呼び出す必要がありますいない場合は、完了のルーチンでは、イベントを通知、 [ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)します。

### <a name="span-idconstraintsonreturningstatusspanspan-idconstraintsonreturningstatusspanspan-idconstraintsonreturningstatusspanconstraints-on-returning-status"></a><span id="Constraints_on_Returning_Status"></span><span id="constraints_on_returning_status"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS"></span>制約の状態を返す

-   ファイル システム フィルター ドライバー完了ルーチンは、いずれかの状態を返す必要があります\_成功または状態\_詳細\_処理\_必要な作業です。 その他のすべての NTSTATUS 値の状態にリセットされます\_I/O マネージャーによって成功します。

### <a name="span-idconstraintsonreturningstatusmoreprocessingrequiredspanspan-idconstraintsonreturningstatusmoreprocessingrequiredspanspan-idconstraintsonreturningstatusmoreprocessingrequiredspanconstraints-on-returning-statusmoreprocessingrequired"></a><span id="Constraints_on_Returning_STATUS_MORE_PROCESSING_REQUIRED"></span><span id="constraints_on_returning_status_more_processing_required"></span><span id="CONSTRAINTS_ON_RETURNING_STATUS_MORE_PROCESSING_REQUIRED"></span>状態を返す制約\_詳細\_処理\_必要な作業

3 つのケースがある場合、完了ルーチンの状態を返す必要があります\_詳細\_処理\_REQUIRED:

-   ときに、対応するディスパッチ ルーチンは、完了ルーチンによって通知するイベントを待機しています。 ここでは状態を返す必要が\_詳細\_処理\_I/O マネージャーが IRP の完了の日常的な取得後に途中で完了するを防ぐために必要な作業です。

-   完了ルーチンのワーカーのキューに IRP が投稿して、状態が返されましたが、対応するディスパッチ ルーチンと\_保留します。 状態を返すために重要ですが同様に、ここで\_詳細\_処理\_I/O マネージャーが IRP の完了の日常的な取得後に途中で完了するを防ぐために必要な作業です。

-   呼び出すことによって、同じドライバーが IRP を作成するときに[ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)または[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)します。 ドライバーより高度なドライバーからこの IRP を受信しませんでした、ため、その安全に完了ルーチンの IRP を解放することができます。 呼び出した後[ **IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)、完了ルーチンの状態を返す必要があります\_詳細\_処理\_ことを示すために必要な作業それ以上ない完了処理が必要です。

完了ルーチンの状態を返すことができない\_詳細\_処理\_oplock 操作に必要です。 Oplock の操作は保留 (ワーカー キューにポストされた)、することはできず、ディスパッチ ルーチンは、状態を返すことはできません\_保留にします。

### <a name="span-idconstraintsonpostingirpstoaworkqueuespanspan-idconstraintsonpostingirpstoaworkqueuespanspan-idconstraintsonpostingirpstoaworkqueuespanconstraints-on-posting-irps-to-a-work-queue"></a><span id="Constraints_on_Posting_IRPs_to_a_Work_Queue"></span><span id="constraints_on_posting_irps_to_a_work_queue"></span><span id="CONSTRAINTS_ON_POSTING_IRPS_TO_A_WORK_QUEUE"></span>Irp の作業キューに投稿の制約

-   完了ルーチンの Irp 作業キューに投稿する場合を呼び出す必要[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)各 IRP ワーカー キューに送信する前にします。 それ以外の場合、IRP でしたデキューされた別のドライバーのルーチンで完了し、呼び出しの前に、システムによって解放**IoMarkIrpPending**原因となり、クラッシュが発生します。

 

 




