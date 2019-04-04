---
title: 記憶域クラス ドライバーの IoCompletion ルーチン
description: 記憶域クラス ドライバーの IoCompletion ルーチン
ms.assetid: 03cf50be-1b7d-4e5b-8ee5-bbdef860d893
keywords:
- IoCompletion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc61ba878b2ef783f0e82eb10ea478a7f72b6130
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581695"
---
# <a name="storage-class-drivers-iocompletion-routines"></a>記憶域クラス ドライバーの IoCompletion ルーチン


## <span id="ddk_storage_class_drivers_iocompletion_routines_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_IOCOMPLETION_ROUTINES_KG"></span>


ストレージ クラス ドライバーが 1 つまたは複数必要[ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン、ドライバーは、ポート ドライバーに送信するすべての IRP の完了時に同期的に待機する、しない限り、必要に応じて、要求を再試行し、ディスパッチ内からされる Srb のメモリを解放または*BuildRequest*ルーチン。 すべて IRP を同期的に処理すると、クラス ドライバーのパフォーマンスが低下することに注意してください。 さらに、システムのページング ファイルは、すべてを処理する必要がありますが保持するデバイスの記憶域クラス ドライバーは要求を非同期的に転送し、したがっている必要があります、 *IoCompletion*読み取り/書き込み要求のルーチンです。

」の説明に従って[記憶域クラス ドライバー BuildRequest ルーチン](storage-class-driver-s-buildrequest-routine.md)かどうかのバックアップや非ページ プール ルック アサイド リストに、記憶域クラス ドライバーはされる Srb に割り当てたメモリを解放する責任があります。 など、他の高度なカーネル モード ドライバー、担当も IRP」の説明に従って、譲渡要求を分割するなど、割り当て、任意の Irp の解放[記憶域クラス ドライバー SplitTransferRequest ルーチン](storage-class-driver-s-splittransferrequest-routine.md)します。

クラス ドライバーの*IoCompletion*状態の I/O ブロックが設定されていることを確認し、元の IRP を完了するために行うルーチンからです。 SRB のでは IRP の完了をエラーに変換を含めることができますが返される**ScsiStatus**メンバーまたは**SenseInfoBuffer** NTSTATUS 型の値や」の説明に従って、エラーをログにメンバー[ディスパッチ ルーチンに Irp の完了](https://msdn.microsoft.com/library/windows/hardware/ff542019)します。

記憶域ポート ドライバーがターゲット論理ユニット (LU) の内部キューがフリーズして、SRB の設定要求の処理で特定の種類のエラーが発生すると、\_状態\_キュー\_要求の完了時に固定されています。 その結果、クラス ドライバーでは、通常、デバイスの I/O 要求のキューの状態を変更する内部のルーチンがあります。 詳細については、[記憶域クラス ドライバー ReleaseQueue ルーチン](storage-class-driver-s-releasequeue-routine.md)を参照してください。

場合、ドライバーの*BuildRequest*ルーチンのポートのドライバーが、要求の要求の意味が情報を返すことが要求されたその*IoCompletion*日常的ないずれかを呼び出す内部*InterpretRequestSense*ルーチンまたは同じ機能のインラインを実装します。 詳細については、[記憶域クラス ドライバー InterpretRequestSense ルーチン](storage-class-driver-s-interpretrequestsense-routine.md)を参照してください。

記憶域クラス ドライバーは、ターゲット コント ローラーのエラー、バスのリセット、または要求タイムアウトが原因で失敗した要求を再試行します。 ポートのドライバーが、特定の要求でを返す場合、 **SrbStatus**設定すると、このようなエラーを示す、クラス ドライバーが呼び出すことができます、 *RetryRequest*ルーチンからその*IoCompletion*ルーチンまたは場合によってからその*InterpretRequestSense*ルーチン。 詳細については、[記憶域クラス ドライバー RetryRequest ルーチン](storage-class-driver-s-retryrequest-routine.md)を参照してください。

に関する一般的な情報*IoCompletion*ルーチンを参照してください[Irp の完了](https://msdn.microsoft.com/library/windows/hardware/ff542018)します。

 

 




