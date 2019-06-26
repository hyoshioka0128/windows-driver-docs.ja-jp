---
title: 記憶域クラス ドライバーの RetryRequest ルーチン
description: 記憶域クラス ドライバーの RetryRequest ルーチン
ms.assetid: de1eea7d-88db-444c-a9f7-462ad4a5df27
keywords:
- RetryRequest
- WDK 記憶域の要求を再試行しています
- エラー WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd56a8ef9820c25c7ffd27add77964b84cdabe4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379092"
---
# <a name="storage-class-drivers-retryrequest-routine"></a>記憶域クラス ドライバーの RetryRequest ルーチン


## <span id="ddk_storage_class_drivers_retryrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_RETRYREQUEST_ROUTINE_KG"></span>


基になる記憶域ポート ドライバーは、バスの bus パリティ エラー、選択範囲のタイムアウト、およびターゲット/コント ローラーでビジー状態のエラーを含むデータの転送に関連するデバイスのエラーが発生した場合は、要求を再試行します。 再試行が失敗した場合、記憶域ポート ドライバーは、該当するエラーにより要求を完了し、I/O エラーもログに記録します。

ストレージ クラス ドライバーは、ポートのドライバーが前のエラーのいずれかにより既に失敗した要求を再試行する試みる必要があることはありません。

ストレージ クラス ドライバーは、デバイスに固有のエラー、ターゲット/コント ローラー、負荷の高い、バスのリセット以外のターゲット/コント ローラーのエラーが原因で失敗またはタイムアウトの要求を再試行中の要求を担当します。 一般に、 *RetryRequest*ルーチンが次の下位のドライバーに、このような IRP を再送信し、SRB がポート ドライバーの LU 固有のキューの先頭に配置することを指示します。

具体的を*RetryRequest*ルーチンは、次を行う必要があります。

1.  部分的な転送要求に適切な値の開始アドレスと長さを設定してください。

2.  0、 **SrbStatus**と**ScsiStatus** SRB のメンバー。

3.  セットアップ、 **SrbFlags**に必要な場合、デバイスのメンバー。

4.  ポート ドライバーですでに説明した IRP の I/O スタックの場所を設定[記憶域クラス ドライバーのディスパッチ ルーチン](storage-class-driver-s-dispatch-routines.md)を通じて[記憶域クラス ドライバー SplitTransferRequest ルーチン](storage-class-driver-s-splittransferrequest-routine.md)します。

5.  呼び出す[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine) 、IRP のため、ドライバーの[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンが IRP の前に SRB を解放する必要があります返します。 *IoCompletion*ルーチンも必要になる要求を複数回再試行するかを呼び出してドライバーの*InterpretRequestSense*または*ReleaseQueue*ルーチン。

6.  要求を使用してドライバーを次の下位に渡す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

 

 




