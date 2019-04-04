---
title: SCSI ポート ドライバーの内部キューのロック
description: SCSI ポート ドライバーの内部キューのロック
ms.assetid: ea5be4e1-4908-431c-9c80-96539157b87e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e938816dd8fa1ef0db51995733118bcac7199012
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527361"
---
# <a name="locking-scsi-port-drivers-internal-queue"></a>SCSI ポート ドライバーの内部キューのロック


## <span id="ddk_locking_scsi_port_driver_s_internal_queue_kg"></span><span id="DDK_LOCKING_SCSI_PORT_DRIVER_S_INTERNAL_QUEUE_KG"></span>


クラスのドライバーと他の高度なドライバーは、そのキューに要求の処理を停止する SCSI ポートを強制できます。 クラスのドライバーでは、SCSI ポートのキューを停止、SRB の SRB の種類を送信することで\_関数\_ロック\_キュー。 通常、クラス ドライバーは、デバイスの電源の状態を変更するには、SCSI ポートのキュー内の要求の処理を停止します。 デバイスの電源の状態を変更した後は、クラス ドライバーは、キューのロックを解除します。 シーケンスは次のとおりです。

1.  クラス ドライバー SCSI ポートのキューのロック (IRP を使用して\_MJ\_SRB の SRB 関数の値を持つ SCSI\_関数\_ロック\_キュー)。

2.  クラス ドライバーの電源状態の変更を要求する (IRP を使用して\_MJ\_、SRB の SCSI\_フラグ\_バイパス\_ロック\_IRP がキューに登録されません power ことを確認するキューのフラグが設定)。

3.  SCSI ポートのキューのロックを解除クラス ドライバー (IRP\_MJ\_SRB の SRB 関数の値を持つ SCSI\_関数\_ロックの解除\_キューと、SRB\_フラグ\_バイパス\_LOCKED\_キュー フラグが設定)。

そのキューのロックが解除されると SCSI ポートは、キューに置かれたされる Srb の処理を再開します。 クラス ドライバーは、別のドライバーによってロックされたキューをバイパスしないようにします。

クラスのドライバーの観点からロックを解除するキューの詳細については、[記憶域クラス ドライバー ReleaseQueue ルーチン](storage-class-driver-s-releasequeue-routine.md)を参照してください。

 

 




