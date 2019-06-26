---
title: ビデオ デコード操作の同期
description: ビデオ デコード操作の同期
ms.assetid: 4c88bf8f-0f10-4281-b856-a0e056d69d0e
keywords:
- WDK の DirectX va なので、同期をデコードするビデオ
- ビデオの WDK DirectX va なので、同期のデコード
- WDK DirectX VA の同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ed23ab0b98491230657003d2c37443fe1ef74cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372042"
---
# <a name="synchronizing-video-decode-operations"></a>ビデオ デコード操作の同期


## <span id="ddk_synchronizing_video_decode_operations_gg"></span><span id="DDK_SYNCHRONIZING_VIDEO_DECODE_OPERATIONS_GG"></span>


DirectX VA 2.0 の同期メカニズムでは、バージョン 1.0 からが改善され、マイクロソフトの Direct3D 操作で使用される同期メカニズムに似ています。

DirectX VA 1.0 では、同期は、主に、デコーダーによって実行されます。 デコーダーが圧縮されたバッファーを使用する前に呼び出し、 [ *DdMoCompQueryStatus* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)バッファーが使用可能なかどうかを判断する関数 (つまり、ハードウェアがないバッファーにアクセスする)。 バッファーが利用できない場合、デコーダーする必要がありますスリープ状態、ポーリング、別の操作を実行します。

DirectX VA 2.0 では、Direct3D は、頂点バッファーとインデックス バッファーで既に使用している同期モデルを使用します。 DirectX VA 2.0 では、同期は圧縮されたバッファーのロック、デコーダーによって実行されます。 ユーザー モードで表示する場合ドライバーが、圧縮されたバッファーをロックしようとしています。 バッファーが使用されて、ドライバーするロックが失敗するか、バッファーの名前を変更します。 ユーザー モードのディスプレイ ドライバーは、ビデオ メモリ マネージャーでは、ドライバーを設定すると、バッファーが名前を変更ことを要求、**破棄**のメンバー、 [ **D3DDDICB\_LOCKFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)構造体への呼び出しで、 [ **pfnLockCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)関数。 ユーザー モードのディスプレイ ドライバーには、バッファーが名前変更する場合、ドライバーは、デコーダーがブロックされることがなく続行できるように、別のバッファーにポインターを返します。

通常、DirectX VA 2.0 では、同期はのみ問題に場合は、ハードウェアは、追加のバッファー コピーせずに直接圧縮されたバッファーを使用できます。

 

 





