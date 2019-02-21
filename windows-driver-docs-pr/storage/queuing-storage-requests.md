---
title: ストレージ要求のキュー
description: ストレージ要求のキュー
ms.assetid: 077f7e4f-feb5-4a2e-b22b-b1d8d6871987
keywords:
- 周辺機器の WDK ストレージ、キューに置かれた要求
- 記憶域周辺機器 WDK、キューに置かれた要求
- キューに置かれた要求の WDK ストレージ
- キューの WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcde1f1ff09d4e2e4681e402a996f513a3bd00e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529069"
---
# <a name="queuing-storage-requests"></a>ストレージ要求のキュー


## <span id="ddk_queueing_storage_requests_kg"></span><span id="DDK_QUEUEING_STORAGE_REQUESTS_KG"></span>


記憶域クラス ドライバー Irp の内部キューを設定することはできますはめったにありませんもに、ドライバーのパフォーマンスが低下する可能性があると、これを行うために必要な記憶域ポート ドライバーが既にドライバーが作成した、LU 固有のデバイスのキューを保持するため、Irp します。 特定の HBA が複数の未実行のコマンドをサポートしているかどうか (たとえば、SCSI、タグ付きキュー)、HBA を処理するためにキューに置かれたまたは記憶域クラス ドライバーは各 IRP が渡されるときに、各自のデバイスにすべての要求を送信し、システムが指定したポート ドライバーに依存迅速に要求します。

特定の SCSI エラーが発生すると、システム ポートのドライバーは LU 固有の適切なキューがフリーズして、クラス ドライバーに通知します。 エラーを処理して、固定された要求のキューを解放する方法の詳細については、次を参照してください。

[記憶域クラス ドライバー ReleaseQueue ルーチン](storage-class-driver-s-releasequeue-routine.md)

[記憶域クラス ドライバー InterpretRequestSense ルーチン](storage-class-driver-s-interpretrequestsense-routine.md)

[記憶域クラス ドライバー RetryRequest ルーチン](storage-class-driver-s-retryrequest-routine.md)

HBA が返されたストレージに記載されているコマンドがキューをサポートする場合\_アダプター\_記述子のデータ クラス ドライバー設定 SRB\_フラグ\_キュー\_有効にすると、使用して、 **QueueAction**その要求がキューに登録する方法を制御する作成される Srb のメンバー。

 

 




