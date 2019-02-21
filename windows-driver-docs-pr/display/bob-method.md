---
title: Bob メソッド
description: Bob メソッド
ms.assetid: 3ef4ad25-fe62-4f80-8d0a-d21035d93c1f
keywords:
- DirectX VPE サポート WDK DirectDraw、インターリーブのビデオを表示します。
- VPEs WDK DirectDraw を描画、ビデオがインターリーブを表示します。
- DirectDraw VPEs WDK Windows 2000 の表示、インターリーブのビデオを表示します。
- 拡張機能のビデオ ポート WDK DirectDraw、インターリーブのビデオを表示します。
- VPEs WDK DirectDraw、インターリーブのビデオを表示します。
- インターリーブのビデオを表示します。
- インタリーブされたビデオは、WDK のビデオ ポートの拡張機能を表示します。
- WDK DirectDraw を bob します。
- デインター レース WDK ビデオ ポートの拡張機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb7159560173e198ad8fea688a5a748636a72a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538417"
---
# <a name="bob-method"></a>Bob メソッド


## <span id="ddk_bob_method_gg"></span><span id="DDK_BOB_METHOD_GG"></span>


データの表示の bob メソッドは、各フィールドを個別に表示 (テレビに似ています)、オーバーレイを使用します。 結果のイメージは通常の半分の高さは、補間のオーバーレイ、stretch を使用して、垂直方向の 200% を拡大する必要があります。 ただし、bob のアルゴリズムがすべてこの場合は、結果のイメージはジッターを上下奇数のフィールドともフィールドのオフセットを 1 行あるためです。 奇数のフィールドにオーバーレイの開始アドレスを 1 つの行を追加する、インターポレーターを使用して、垂直方向の stretch を実行している限り、この問題は解決します。

Bob メソッドは、1 秒あたり 60 の (NTSC) プログレッシブ フレームを生成し、インター レースされたソースからのすべての一時的な情報を保持します。 ビデオをビデオ_カメラで作成されたイメージには、モーションが含まれている場合は、bob、プログレッシブのモニターの最適な低コストの表示処理です。 すべてのインター レースのビデオ データ ソースの bob メソッドが機能しますが、weave メソッドが鮮明な画像を生成します。

既定では、DirectShow はインター レースの表示を修正するため、bob メソッドを使用します。

 

 





