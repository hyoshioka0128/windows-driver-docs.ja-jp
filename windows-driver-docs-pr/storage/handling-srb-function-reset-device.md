---
title: SRB_FUNCTION_RESET_DEVICE の処理
description: SRB_FUNCTION_RESET_DEVICE の処理
ms.assetid: d95bca21-306e-4598-a8c6-04990885e23d
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_RESET_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 156f4635de920238e7305c7ef25b854c369c91c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383114"
---
# <a name="handling-srbfunctionresetdevice"></a>処理 SRB\_関数\_リセット\_デバイス


## <span id="ddk_handling_srb_function_reset_device_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_RESET_DEVICE_KG"></span>


ScsiPort ドライバーは、不要になった、ミニポート ドライバーをこの SRB を送信します。 Storport ミニポート ドライバーのみがこの SRB を処理する必要があります。

HBA というように、ターゲット デバイスをリセットする機能がある場合[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)設定、 [**ポート\_構成\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff563900)、ポート ドライバーがリセット未完了の要求がタイムアウトしたときにデバイスを要求します。

システムのポート ドライバー呼び出し、ミニポート ドライバーの*HwScsiStartIo*ルーチンを SRB、**関数**SRB にメンバーが設定されている\_関数\_リセット\_デバイスです。 ミニポート ドライバーは、要求は、デバイスのリセット要求を受信すると、デバイスの完了を完了します。

デバイスのリセットが失敗したか、タイムアウト、またはポート ドライバーが待機しているときにタイムアウトが発生した場合、 **NextRequest**通知、ポートのドライバー呼び出し[ *HwScsiResetBus* ](https://msdn.microsoft.com/library/windows/hardware/ff557318).

 

 




