---
title: 幾何学的線
description: 幾何学的線
ms.assetid: 769b801c-6950-4f0f-9163-c4ddf070e519
keywords:
- WDK GDI、ジオメトリ全体を行します。
- GDI WDK Windows 2000 の表示、線、ジオメトリ全体
- グラフィック ドライバー WDK Windows 2000 を表示、線、ジオメトリ全体
- 描画 WDK GDI、線、ジオメトリ全体
- 幾何学的線 WDK GDI
- 幾何学的行 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f5107e6d12480f11309c8c39e7974099755edb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532641"
---
# <a name="geometric-wide-lines"></a>幾何学的線


## <span id="ddk_geometric_wide_lines_gg"></span><span id="DDK_GEOMETRIC_WIDE_LINES_GG"></span>


形状を*幾何学的*行は、幅、結合のスタイルおよびブラシ、およびで現在の世界からデバイスへの変換の端点キャップ スタイルによって決定されます、 [ **XFORMOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570618)構造体。 ソリッドまたは非ソリッド ブラシを使用して線を描画できます。

高度なハードウェアのドライバーもサポートして幾何学的で線、 [ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)関数。 GDI は、ドライバーが、GCAPS をテストして geometric ラインを含むパスを描画できるかどうかを決定します\_GEOMETRICWIDE 機能フラグ、 [ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835) への呼び出しで返される構造体。[**DrvEnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556211)します。 場合は、ドライバーには、機能がないか、GDI がより単純な呼び出しを自動的に変換関数は、パスまたはクリッピングがデバイスには複雑すぎるため、操作を処理するために失敗した場合、 [ **DrvFillPath**](https://msdn.microsoft.com/library/windows/hardware/ff556220)関数。

ジオメトリの太線は、ディスプレイ ドライバーのグラフィックス機能を特定の意味を持ちます。 デバイス座標を含むパスは、現在の変換の逆関数を使用してワールド座標に変換されます。 指定した幅と幾何学的構築し、アカウントの結合と終点のキャップを考慮して、パスの拡張のバージョンを取得します。 このパスはもう一度デバイス座標に変換し、指定のブラシで塗りつぶされます。

幾何学的線のスタイルは、浮動小数点値の配列によって指定されます。 配列は、有限の長さが、無期限に繰り返すことのように使用されます。 配列の最初のエントリは、ワールド座標、最初のダッシュの長さを指定します。次のエントリには、最初の空白の長さを指定します。 その後、破線と空白の長さの代替です。 たとえば、スタイルの配列 {3.0,1.0,1.0,1.0} は、長短ダッシュを交互に描画される線です。

スタイル設定は、拡大する前に、パスに沿って移動ドライバーとして考えることができます、ギャップに対応するパスの部分を「消去」。 これは、多くのサブパスにパスを分割します。 線のスタイルを使用して、通常どおりの終端のキャップと結合を適用することがなかった場合と、切断されたパスは拡張します。 スタイルの配列には、奇数の長さを指定できます。 たとえば、1.0 {0} スタイルの配列は原因交互ダッシュを使用した直線を描画するためにドライバーです。 パス内の最初のサブパスの最初の (現在までの距離をスタイル設定の配列として定義されている) スタイルの状態が提供されます。 Win32 の後に発生する各後続のサブパスの開始時の 0.0 にリセットすると見なされます**MoveToEx**操作。

 

 





