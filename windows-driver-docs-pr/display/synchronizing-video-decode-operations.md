---
title: ビデオ デコード操作の同期
description: ビデオ デコード操作の同期
ms.assetid: 4c88bf8f-0f10-4281-b856-a0e056d69d0e
keywords:
- ビデオデコード WDK DirectX VA、同期
- ビデオをデコードする WDK DirectX VA、同期
- WDK DirectX VA の同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b10c168597a872aff9adea873cf955b5ac92363f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825516"
---
# <a name="synchronizing-video-decode-operations"></a>ビデオ デコード操作の同期


## <span id="ddk_synchronizing_video_decode_operations_gg"></span><span id="DDK_SYNCHRONIZING_VIDEO_DECODE_OPERATIONS_GG"></span>


DirectX VA 2.0 の同期メカニズムは1.0 バージョンから向上し、Microsoft Direct3D 操作で使用される同期メカニズムに似ています。

DirectX VA 1.0 では、主にデコーダーによって同期が実行されます。 デコーダーは、圧縮されたバッファーを使用する前に、 [*DdMoCompQueryStatus*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)関数を呼び出して、バッファーが使用可能かどうかを判断します (つまり、ハードウェアはバッファーにアクセスしていません)。 バッファーが使用できない場合、デコーダーはスリープ、ポーリング、または別の操作を実行する必要があります。

DirectX VA 2.0 では、Direct3D が頂点バッファーとインデックスバッファーで既に使用している同期モデルが使用されます。 DirectX VA 2.0 では、デコーダーが圧縮バッファーをロックすることによって同期が実行されます。 ユーザーモード表示ドライバーが圧縮バッファーをロックしようとして、バッファーが使用中の場合、ドライバーはロックを解除するか、バッファーの名前を変更することができます。 ユーザーモードのディスプレイドライバーは、 [**D3DDDICB\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)構造体の**破棄**メンバーが[**pfnlockcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)関数の呼び出しで設定されている場合、ビデオメモリマネージャーがバッファーの名前を変更することを要求します。 ユーザーモード表示ドライバーによってバッファーの名前が変更された場合、ドライバーは代替バッファーへのポインターを返します。これにより、デコーダーはブロックされずに続行できます。

通常、DirectX VA 2.0 の場合、同期は、ハードウェアがバッファーコピーを追加せずに、圧縮されたバッファーを直接使用できる場合にのみ問題になります。

 

 





