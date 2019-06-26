---
title: SRB_FUNCTION_RESET_BUS の処理
description: SRB_FUNCTION_RESET_BUS の処理
ms.assetid: 285cbd5c-e364-4f0f-9020-0bc6f3d45cac
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_RESET_BUS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fac1ca0389068fd7f130d8e2cc14e9850911fc0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371174"
---
# <a name="handling-srbfunctionresetbus"></a>処理 SRB\_関数\_リセット\_バス


## <span id="ddk_handling_srb_function_reset_bus_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_RESET_BUS_KG"></span>


常に、システム ポートのドライバーは、ミニポート ドライバーに直接リセット bus 要求を送信[ *HwScsiResetBus* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))ルーチンを記載[SCSI ミニポート ドライバー HwScsiResetBus日常的な](scsi-miniport-driver-s-hwscsiresetbus-routine.md)します。

ただし、可能性は、 [ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))を SRB で呼び出されるルーチンを**関数**SRB にメンバーが設定されている\_関数\_リセット\_バスのオペレーティング システムの NT ベースの記憶域クラス ドライバーは、この操作を要求した場合。 *HwScsiStartIo*ルーチンを呼び出すだけで、 *HwScsiResetBus*受信のバスのリセット要求を満たすためのルーチンです。

 

 




