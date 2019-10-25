---
title: SRB_FUNCTION_RESET_DEVICE の処理
description: SRB_FUNCTION_RESET_DEVICE の処理
ms.assetid: d95bca21-306e-4598-a8c6-04990885e23d
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_RESET_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 081187ef43872d82bce4a215fb4829873d30c80c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833729"
---
# <a name="handling-srb_function_reset_device"></a>SRB\_関数の処理\_\_デバイスのリセット


## <span id="ddk_handling_srb_function_reset_device_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_RESET_DEVICE_KG"></span>


ScsiPort ドライバーは、この SRB をミニポートドライバーに送信しなくなりました。 この SRB を処理する必要があるのは、Storport ミニポートドライバーだけです。

[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))が[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)を設定するときに示されているように、HBA にターゲットデバイスをリセットする機能がある場合、ポートドライバーは、未完了の要求がタイムアウトしたときにデバイスのリセットを要求します。

システムポートドライバーは、SRB を使用して、ミニポートドライバーの*HwScsiStartIo*ルーチンを呼び出します。この場合、**関数**メンバーが SRB\_関数に設定され、\_デバイスがリセット\_ます。 ミニポートドライバーは、デバイスがリセットデバイスの要求を受け取ったときに、デバイスで未完了の要求を完了する役割を担います。

デバイスのリセットが失敗またはタイムアウトした場合、またはポートドライバーが**Nextrequest**通知を待機しているときにタイムアウトが発生した場合、ポートドライバーは[*HwScsiResetBus*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))を呼び出します。

 

 




