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
ms.openlocfilehash: 28611b80631ab5b2bc0319b6f8bbd1a0278603fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372333"
---
# <a name="handling-srbfunctionresetdevice"></a>処理 SRB\_関数\_リセット\_デバイス


## <span id="ddk_handling_srb_function_reset_device_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_RESET_DEVICE_KG"></span>


ScsiPort ドライバーは、不要になった、ミニポート ドライバーをこの SRB を送信します。 Storport ミニポート ドライバーのみがこの SRB を処理する必要があります。

HBA というように、ターゲット デバイスをリセットする機能がある場合[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))設定、 [**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)、ポート ドライバーがリセット未完了の要求がタイムアウトしたときにデバイスを要求します。

システムのポート ドライバー呼び出し、ミニポート ドライバーの*HwScsiStartIo*ルーチンを SRB、**関数**SRB にメンバーが設定されている\_関数\_リセット\_デバイスです。 ミニポート ドライバーは、要求は、デバイスのリセット要求を受信すると、デバイスの完了を完了します。

デバイスのリセットが失敗したか、タイムアウト、またはポート ドライバーが待機しているときにタイムアウトが発生した場合、 **NextRequest**通知、ポートのドライバー呼び出し[ *HwScsiResetBus* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85)).

 

 




