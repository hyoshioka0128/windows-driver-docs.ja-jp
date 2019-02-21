---
title: 記憶域周辺機器に電力要求を処理
description: 記憶域周辺機器に電力要求を処理
ms.assetid: 3cc7b885-27ad-4384-aeec-4d76f9ad4f1c
keywords:
- 記憶域周辺機器の WDK、電源を要求します。
- 記憶域周辺機器 WDK、電源の要求
- 電源要求 WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 447676b22443a19eb4565e95a14355210eb66a82
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553443"
---
# <a name="handling-power-requests-to-storage-peripherals"></a>記憶域周辺機器に電力要求を処理


## <span id="ddk_handling_power_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_POWER_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


ストレージ クラス ドライバーは、電源の要求を処理するデバイスに固有のコマンドを発行します。 ほとんどの場合、記憶域クラス ドライバー:

-   クエリ性能の要求に対する応答でそのデバイスに I/O をブロック (IRP\_MJ\_を含む POWER [ **IRP\_MN\_クエリ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551699)) 場合このような I/O を処理すると、ドライバーがセット power 要求を一定の時間に成功を妨げる可能性

-   セット power 要求への応答でそのデバイスの電源状態を設定 (IRP\_MJ\_を含む POWER [ **IRP\_MN\_設定\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744))

-   デバイスの電源をセット power 要求に応答には、そのデバイスを I/O で再起動します。

-   次の下位のドライバーに電源の要求を転送します。

ドライバーを呼び出す必要がありますので注意[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)と[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)ではなく、**保留**、電源の要求を送信します。

記憶域クラス ドライバーがあるない限り、 [ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)日常的なその必要がありますロック ストレージ ポート ドライバーの LU 固有のキュー (IRP\_MJ\_SRB の SCSI\_関数\_ロック\_キュー) (これは、いくつかの手順があります)、電源操作が完了するまでに同期されていない操作をブロックする、デバイスの電源状態を設定する前にします。 電源操作を処理するために発行された任意のされる Srb SRB を設定する必要があります\_フラグ\_バイパス\_ロック\_ポート ドライバーに到達するかどうかを確認するキュー。 ドライバーでは、電源状態の設定が完了すると、キューのロック解除にする必要があります (IRP\_MJ\_SRB の SCSI\_関数\_UNLOCK\_キューと SRB\_フラグ\_バイパス\_ロック\_キュー) ポート ドライバーの電源投入後にキューに置かれた Irp をデバイスに送信を再開できるようにします。

ストレージ クラス ドライバーがある場合、 *StartIo*日常的なそのルーチン処理同期クラス ドライバーは明示的にロックし、ポート ドライバーの LU 固有のキューのロックを解除する必要はありませんので。

クラス ドライバーは、別のドライバーによってロックされているキューをバイパスしないようにします。

 

 




