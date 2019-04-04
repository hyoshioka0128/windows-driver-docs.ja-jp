---
title: SCSI ポート I/O モデル
description: SCSI ポート I/O モデル
ms.assetid: c79fdc99-30ae-4c4a-a130-2b8743bbff7f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc6afbec4f2a1811ab55af39d11b807a2caa58f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529028"
---
# <a name="scsi-port-io-model"></a>SCSI ポート I/O モデル


## <span id="ddk_scsi_port_i_o_model_kg"></span><span id="DDK_SCSI_PORT_I_O_MODEL_KG"></span>


SCSI ポート ドライバーは、一連のディスパッチとドライバーのテーブル オブジェクトに、ミニポート ドライバー コールバック ルーチンへのポインターを使用して、ミニポート ドライバーと通信します。 ミニポート ドライバー呼び出し[ **ScsiPortInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff564645)からその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン SCSI ポートのディスパッチを初期化するにはこれらのコールバック ポインターを持つテーブルとドライバーのオブジェクト。 このような 1 つのコールバック ポインターは、I/O 要求を処理するために使用するミニポート ドライバーの開始の I/O ルーチンのエントリ ポイントです。 ポート ドライバーへのポインターを割り当てます、 **DriverStartIo**ドライバー オブジェクトのメンバー。

SCSI ポートより高度なドライバーからの I/O 要求を受け取る、たびに、内部キューに要求をキューします。 SCSI ポートの内部キューの詳細については、[SCSI ポート ドライバーのキュー管理](scsi-port-driver-s-queue-management.md)を参照してください。

SCSI ポートを呼び出す対象のデバイス準備ができたら、次の I/O 要求を受信する[ **IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)に格納されているさらに、ミニポート ドライバー開始 I/O コールバック ルーチンを呼び出す**DriverObject -&gt;DriverStartIo**します。 操作と、ミニポート ドライバーの開始の I/O ルーチンの必要な特性については、[SCSI ミニポート ドライバー HwScsiStartIo ルーチン](scsi-miniport-driver-s-hwscsistartio-routine.md)を参照してください。

SCSI ポートは、割り込みをマスクするために、開始の I/O ルーチンが重要なオペレーティング システムとドライバーの構造体へのアクセスを同期されたことを保証するために、ミニポート ドライバーの開始の I/O ルーチンを呼び出す前に、プロセッサの IRQL を発生させます。

ストレージ クラス ドライバーと SCSI ポート ドライバーとの間の I/O 要求パケットのフローは非同期ですが、SCSI ポート ドライバーとターゲット デバイスの間の I/O 要求パケットのフローは同期です。 SCSI ポートは、以前の I/O 要求が完了する前に、SCSI ポートに新しい I/O 要求を送信するクラスのドライバーをできるようにする内部キュー システムを使用します。 ただし、SCSI ポートまで送信しません、次の I/O 要求ターゲット デバイスに、ミニポート ドライバーが次の I/O 要求を受信する準備がミニポート ドライバーから通知を受信します。 ミニポート ドライバーでは、SCSI ポートを通知を呼び出すことによって、 [ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)ライブラリ ルーチン。

Storport ドライバーは、割り込みのマスクに関して具体的にはより柔軟な I/O モデルを提供します。 Storport の I/O モデルと SCSI ポート I/O モデル間の違いについては、[Storport I/O モデル](storport-i-o-model.md)を参照してください。

 

 




