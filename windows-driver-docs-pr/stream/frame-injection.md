---
title: フレーム挿入
description: フレーム挿入
ms.assetid: cdfb1763-92a8-4a60-8f49-2af34a8beca5
keywords:
- WDK AVStream のフレーム
- インジェクションモード WDK AVStream フレーム
- フレームインジェクション WDK AVStream
- pin 中心のフィルター (WDK AVStream)
- フィルター中心のフィルター (WDK AVStream)
- 空のフレーム WDK AVStream
- 既定のフレーム動作 WDK AVStream
- 既定のフレーム動作のオーバーライド WDK streaming media
- 接続 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b35de0fd7d27bd90a4ea6f1c40b846cd224b6563
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842597"
---
# <a name="frame-injection"></a>フレーム挿入





AVStream の既定では、要求元はアロケーターから空のフレームを取得し、キューに配置します。 ミニドライバーは、[ピン中心](pin-centric-processing.md)の処理または[フィルター処理を中心](filter-centric-processing.md)とした処理のいずれかによってフレームを塗りつぶします。 このフレームは、トランスポートを経由して回線内の次のオブジェクトに移動し、最終的には回線を完了し、要求元に戻ります。 AVStream はフレームを再利用します。

ミニドライバーは、*挿入モード*を使用して、この既定の動作をオーバーライドできます。 挿入モードでは、ミニドライバーは、フレームを回線に配置する役割を担います。 フレームは、既定の方法で回線の周りに伝達されます。 フレームが開始された AVStream オブジェクトに戻ると、AVStream はミニドライバーが提供する[*AVStrMiniFrameReturn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinframereturn)ルーチンを呼び出します。

このルーチンでは、ミニドライバーは、インスタンスの割り当てを解除したり、フレームを返したときに保留中の作業を完了したり、フレームを補充して reinject したりすることができます。

挿入モードを設定するために、ミニドライバーは[**KsPinRegisterFrameReturnCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinregisterframereturncallback)を呼び出し、 *AVStrMiniFrameReturn*ルーチンへのポインターを提供します。

*フィルターが停止状態の場合を除き*、 ***KsPinRegisterFrameReturnCallback***を*呼び出さない*でください。

回線にフレームを挿入するには、 [**KsPinSubmitFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinsubmitframe)または[**KsPinSubmitFrameMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinsubmitframemdl)を呼び出します。

次の図は、ソースフィルター、*インプレース*変換フィルター、およびソースの挿入フレームを使用したレンダリングフィルターで構成される avstream フィルターセットを示しています。

![avstream フィルターセットを示す図](images/inject1.png)

 

 




