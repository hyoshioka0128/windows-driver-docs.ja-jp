---
title: SRB_FUNCTION_FLUSH と SRB_FUNCTION_SHUTDOWN の処理
description: SRB_FUNCTION_FLUSH と SRB_FUNCTION_SHUTDOWN の処理
ms.assetid: d4b8b3e5-d895-42ca-bd28-9d3cef805654
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_FLUSH
- SRB_FUNCTION_SHUTDOWN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa6d91c8c0d98e12e41f68151bbff3b61f355e99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842332"
---
# <a name="handling-srb_function_flush-and-srb_function_shutdown"></a>SRB\_関数の処理\_FLUSH および SRB\_関数\_シャットダウン


## <span id="ddk_handling_srb_function_flush_and_srb_function_shutdown_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_FLUSH_AND_SRB_FUNCTION_SHUTDOWN_KG"></span>


[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))が[ **\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)を設定するときに示されているように、HBA がデータを内部的にキャッシュする場合は、 [**HWSCSISTARTIO**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチンで SRB\_関数\_FLUSH および SRB がサポートされている必要があり\_関数は、次のように\_シャットダウン要求を実行します。

-   **関数**メンバーが SRB\_FUNCTION\_FLUSH に設定されている場合は、HBA にキャッシュされたデータ (通常はディスク) を転送するようにミニポートドライバーに指示します。 ミニポートドライバーは、すべてのキャッシュデータが転送されるまでフラッシュ要求を保持し、次にフラッシュ要求を完了する必要があります。

-   このようなフラッシュ要求は、アプリケーションがファイルを閉じたとき、またはアプリケーション自体が終了したときに発生する可能性があります。

-   その**関数**メンバーが SRB\_に設定されている場合、\_SHUTDOWN は、すべてのキャッシュデータをターゲットデバイスにフラッシュするなど、データの転送を完了するようにミニポートドライバーに指示します。 ミニポートドライバーは、ターゲット論理ユニットの HBA 内部キャッシュにデータが残っていない状態になるまで、シャットダウン要求を保持する必要があります。その後、シャットダウン要求を完了します。

    ミニポートドライバーは、システム自体が実際にシャットダウンされる前に、同じ論理ユニットまたは複数の論理ユニットに対する複数のシャットダウン要求で、複数のシャットダウン要求を使用して呼び出すことができることに注意してください。

 

 




