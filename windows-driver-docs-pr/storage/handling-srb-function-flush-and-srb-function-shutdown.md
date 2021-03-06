---
title: SRB_FUNCTION_FLUSH と SRB_FUNCTION_SHUTDOWN の処理
description: SRB_FUNCTION_FLUSH と SRB_FUNCTION_SHUTDOWN の処理
ms.assetid: d4b8b3e5-d895-42ca-bd28-9d3cef805654
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_FLUSH
- SRB_FUNCTION_SHUTDOWN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac8b0c0f9d7896ff0e29147cfe742e9f427af2fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372344"
---
# <a name="handling-srbfunctionflush-and-srbfunctionshutdown"></a>処理 SRB\_関数\_フラッシュと SRB\_関数\_シャット ダウン


## <span id="ddk_handling_srb_function_flush_and_srb_function_shutdown_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_FLUSH_AND_SRB_FUNCTION_SHUTDOWN_KG"></span>


HBA が内部で示されるときにデータをキャッシュする場合[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))設定、 [**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)、 [ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチンは、SRB をサポートする必要があります\_関数\_フラッシュと SRB\_関数\_次のようにシャット ダウンを要求します。

-   SRB その**関数**メンバー SRB に設定\_関数\_フラッシュ ディスクには、通常、HBA にキャッシュされたデータを転送するミニポート ドライバーに指示します。 ミニポート ドライバーする必要がありますすべてのキャッシュされたデータを転送するまで、フラッシュの要求を保持し、フラッシュの要求を完了し。

-   このようなフラッシュ要求は、アプリケーションがファイルを閉じるか、またはアプリケーション自体が終了したときに生じた可能性があります。

-   SRB その**関数**メンバー SRB に設定\_関数\_シャット ダウンをターゲット デバイスにキャッシュされているすべてのデータをフラッシュなどのデータの転送を完了するミニポート ドライバーに指示します。 ミニポート ドライバーする必要がありますシャット ダウン要求にないデータは、HBA の内部キャッシュに残りますまでターゲット論理ユニットをして、シャット ダウン要求を完了し。

    ミニポート ドライバー呼び出すことができます可能性があります、同じ論理ユニットの 1 つ以上のシャット ダウン要求またはシャット ダウン要求がいくつか別の論理ユニットをシステム自体が実際にはシャット ダウンする前に注意してください。

 

 




