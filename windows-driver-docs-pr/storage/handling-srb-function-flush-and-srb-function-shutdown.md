---
title: SRB_FUNCTION_FLUSH および SRB_FUNCTION_SHUTDOWN の処理
description: SRB_FUNCTION_FLUSH および SRB_FUNCTION_SHUTDOWN の処理
ms.assetid: d4b8b3e5-d895-42ca-bd28-9d3cef805654
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_FLUSH
- SRB_FUNCTION_SHUTDOWN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13a329f73fa8e505d5858cf57f51337d38d2d126
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556476"
---
# <a name="handling-srbfunctionflush-and-srbfunctionshutdown"></a>処理 SRB\_関数\_フラッシュと SRB\_関数\_シャット ダウン


## <span id="ddk_handling_srb_function_flush_and_srb_function_shutdown_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_FLUSH_AND_SRB_FUNCTION_SHUTDOWN_KG"></span>


HBA が内部で示されるときにデータをキャッシュする場合[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)設定、 [**ポート\_構成\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff563900)、 [ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)ルーチンは、SRB をサポートする必要があります\_関数\_フラッシュと SRB\_関数\_次のようにシャット ダウンを要求します。

-   SRB その**関数**メンバー SRB に設定\_関数\_フラッシュ ディスクには、通常、HBA にキャッシュされたデータを転送するミニポート ドライバーに指示します。 ミニポート ドライバーする必要がありますすべてのキャッシュされたデータを転送するまで、フラッシュの要求を保持し、フラッシュの要求を完了し。

-   このようなフラッシュ要求は、アプリケーションがファイルを閉じるか、またはアプリケーション自体が終了したときに生じた可能性があります。

-   SRB その**関数**メンバー SRB に設定\_関数\_シャット ダウンをターゲット デバイスにキャッシュされているすべてのデータをフラッシュなどのデータの転送を完了するミニポート ドライバーに指示します。 ミニポート ドライバーする必要がありますシャット ダウン要求にないデータは、HBA の内部キャッシュに残りますまでターゲット論理ユニットをして、シャット ダウン要求を完了し。

    ミニポート ドライバー呼び出すことができます可能性があります、同じ論理ユニットの 1 つ以上のシャット ダウン要求またはシャット ダウン要求がいくつか別の論理ユニットをシステム自体が実際にはシャット ダウンする前に注意してください。

 

 




