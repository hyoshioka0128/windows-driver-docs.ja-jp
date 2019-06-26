---
title: 記憶域クラス ドライバーの InterpretRequestSense ルーチン
description: 記憶域クラス ドライバーの InterpretRequestSense ルーチン
ms.assetid: abfb529d-7fab-40f7-b4cd-e6adb4cf643e
keywords:
- InterpretRequestSense
- 要求の意味が WDK ストレージ
- エラー WDK ストレージ
- WDK 記憶域の要求を再試行しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2d62ee9909357a9e57ca207ed0d7a08330b3a5f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386815"
---
# <a name="storage-class-drivers-interpretrequestsense-routine"></a>記憶域クラス ドライバーの InterpretRequestSense ルーチン


## <span id="ddk_storage_class_drivers_interpretrequestsense_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_INTERPRETREQUESTSENSE_ROUTINE_KG"></span>


*InterpretRequestSense*ルーチン SRB ので返されるデータを解釈する**SenseInfoBuffer**、ない場合、要求を再試行する必要があります、かどうかを決定、NTSTATUS 値が、エラーにマップしますIRP の I/O の状態のブロックです。

システムのポート ドライバーでは、SRB を設定して、要求センス情報が使用できるかどうかを示します\_状態\_AUTOSENSE\_VALID または SRB\_状態\_要求\_意味\_で失敗しました**SrbStatus**します。

検出要求の情報が使用できない場合*InterpretRequestSense*確認する必要があります、 **SrbStatus**特定の要求を再試行するかを適切なマッピングを確認するかどうかを決定する値をNTSTATUS 値。

*InterpretRequestSense*ルーチンは、ドライバーが指定したエラーのログ記録ルーチンも呼び出すことができます。 含める必要がありますが、記憶域クラス ドライバー ログ、I/O エラー、たびに、 **PathId**、 **TargetId**、 **Lun**、および**SrbStatus**によって値の設定SRB の記憶域ポート ドライバーと、可能であれば、関連の要求の意味については、エラーの一部としてログ エントリの**DumpData**します。 ストレージ クラス ドライバーを使用する必要がありますに注意してください、 **PathId**、 **TargetId**、および**Lun**からこのようなされる Srb 他の要求に対処します。

I/O エラーのログ記録の詳細については、次を参照してください。[ログ エラー](https://docs.microsoft.com/windows-hardware/drivers/kernel/logging-errors)します。

 

 




