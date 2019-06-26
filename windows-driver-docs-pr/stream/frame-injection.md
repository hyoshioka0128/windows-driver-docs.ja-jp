---
title: フレーム挿入
description: フレーム挿入
ms.assetid: cdfb1763-92a8-4a60-8f49-2af34a8beca5
keywords:
- WDK AVStream フレーム
- 挿入モードの WDK AVStream フレーム
- フレームの WDK AVStream の挿入
- 暗証番号 (pin) を中心としたフィルター WDK AVStream
- フィルターを中心としたフィルター WDK AVStream
- 空のフレーム WDK AVStream
- 既定のフレーム動作 WDK AVStream
- 既定のフレーム動作 WDK ストリーミング メディアを上書きします。
- WDK AVStream の回路
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17c9a61903cbbb61e825eaceb18d768fadc8f65d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384071"
---
# <a name="frame-injection"></a>フレーム挿入





AVStream で既定では、依頼者は、アロケーターから空のフレームを取得し、キューに配置します。 ミニドライバーでいずれかのフレームの塗りつぶし、[暗証番号 (pin) を中心とした処理](pin-centric-processing.md)または[フィルターを中心とした処理](filter-centric-processing.md)します。 フレームは、トランスポートの間で最終的に、回線を完了して、要求元に返すことは、回線の次のオブジェクトに移動します。 AVStream には、次のフレームが再利用します。

ミニドライバーを使用してこの既定の動作をオーバーライドできます*インジェクション モード*します。 挿入モードでは、ミニドライバーは、回線にフレームを配置する責任を負います。 既定の方法で、回線の周囲にフレームが反映されます。 フレームは、起動した AVStream オブジェクトに戻り、AVStream 呼び出しミニドライバーの[ *AVStrMiniFrameReturn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinframereturn)ルーチン。

このルーチンで、ミニドライバーでしたインスタンスのフレームの割り当てを解除、フレームの戻り値の保留中の作業を完了または補充し、フレームを再挿入します。

挿入モードをミニドライバーの呼び出しを設定する[ **KsPinRegisterFrameReturnCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinregisterframereturncallback)へのポインターとその*AVStrMiniFrameReturn*ルーチン。

*呼び出さない* ***KsPinRegisterFrameReturnCallback*** *フィルターが停止状態でない限り、します。*

回路にフレームを挿入するには、呼び出す[ **KsPinSubmitFrame** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinsubmitframe)または[ **KsPinSubmitFrameMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinsubmitframemdl)します。

次の図は、ソース フィルターの構成設定、AVStream フィルターを示します、*インプレース*フレームを挿入するソースとフィルター、およびレンダリングのフィルターを変換します。

![avstream のフィルター セットを示す図](images/inject1.png)

 

 




