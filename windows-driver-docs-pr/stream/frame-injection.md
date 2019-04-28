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
ms.openlocfilehash: 2ef84ec774a23a05762718d3bbbe16e58ab7833a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376122"
---
# <a name="frame-injection"></a>フレーム挿入





AVStream で既定では、依頼者は、アロケーターから空のフレームを取得し、キューに配置します。 ミニドライバーでいずれかのフレームの塗りつぶし、[暗証番号 (pin) を中心とした処理](pin-centric-processing.md)または[フィルターを中心とした処理](filter-centric-processing.md)します。 フレームは、トランスポートの間で最終的に、回線を完了して、要求元に返すことは、回線の次のオブジェクトに移動します。 AVStream には、次のフレームが再利用します。

ミニドライバーを使用してこの既定の動作をオーバーライドできます*インジェクション モード*します。 挿入モードでは、ミニドライバーは、回線にフレームを配置する責任を負います。 既定の方法で、回線の周囲にフレームが反映されます。 フレームは、起動した AVStream オブジェクトに戻り、AVStream 呼び出しミニドライバーの[ *AVStrMiniFrameReturn* ](https://msdn.microsoft.com/library/windows/hardware/ff556320)ルーチン。

このルーチンで、ミニドライバーでしたインスタンスのフレームの割り当てを解除、フレームの戻り値の保留中の作業を完了または補充し、フレームを再挿入します。

挿入モードをミニドライバーの呼び出しを設定する[ **KsPinRegisterFrameReturnCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff563522)へのポインターとその*AVStrMiniFrameReturn*ルーチン。

*呼び出さない* ***KsPinRegisterFrameReturnCallback*** *フィルターが停止状態でない限り、します。*

回路にフレームを挿入するには、呼び出す[ **KsPinSubmitFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff563529)または[ **KsPinSubmitFrameMdl**](https://msdn.microsoft.com/library/windows/hardware/ff563530)します。

次の図は、ソース フィルターの構成設定、AVStream フィルターを示します、*インプレース*フレームを挿入するソースとフィルター、およびレンダリングのフィルターを変換します。

![avstream のフィルター セットを示す図](images/inject1.png)

 

 




