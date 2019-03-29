---
title: サイズ変更可能な BAR のサポート
description: 個別のグラフィックス処理ユニット (GPU) が公開、PCI バス経由でフレーム バッファーのごく一部のみを今日一般的です。
ms.assetid: 9CBB8D2E-D3E3-4F52-BCAC-F17446D74991
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb377432c7ec01d96d418100244dcaa08545568
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579468"
---
# <a name="resizable-bar-support"></a>サイズ変更可能な BAR のサポート


個別のグラフィックス処理ユニット (GPU) が公開、PCI バス経由でフレーム バッファーのごく一部のみを今日一般的です。 32 ビットの Os と互換性のため、独立した Gpu 通常要求、フレーム バッファーに 256 MB の I/O 領域とこれは、一般的な方法のファームウェアに構成します。

Windows Display Driver Model (WDDM) v2 での Windows が横棒グラフを参照してくださいサイズ変更可能なサポートの Gpu で GPU バー post ファームウェア初期化のサイズを外し[上サイズ変更バー機能](https://go.microsoft.com/fwlink/p/?LinkId=525610)で、 [PCI SIG 仕様ライブラリ](https://go.microsoft.com/fwlink/p/?LinkId=690603)します。

横棒グラフ、サイズ変更可能なサポート、GPU を表示および静的な画像を示すバーの再プログラミング中に保持できることを確認してください。 空白とバックエンドの移動が画面に表示したく具体的には、このプロセス中にアップします。 滑らかに表示されるファームウェア イメージ、ブート ローダーのイメージおよびカーネル モード ドライバーの生成の最初のイメージが重要です。 PCI のトランザクションが発生しないこと、GPU に向けた、再ネゴシエーションが行われている間が保証されます。

ほとんどの場合この再ネゴシエーションはできません、カーネル モード ドライバーに表示されます。 再ネゴシエーションが成功したときに、カーネル モード ドライバーは独立した GPU の全体の VRAM を公開する最大サイズに GPU バーをサイズが変更されたことを確認します。

成功のサイズ変更時に、カーネル モード ドライバーが、1 つを公開します。 *CPUVisible*、ビデオ メモリ マネージャーにメモリのセグメント。 ビデオ メモリ マネージャーが、CPU はメモリのセグメントのコンテンツにアクセスする必要がある場合は、この範囲に直接 CPU 仮想アドレスをマップします。

 

 





