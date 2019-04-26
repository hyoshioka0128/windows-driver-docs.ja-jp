---
title: フレーム バッファーおよびハードウェアの登録へのアクセス
description: フレーム バッファーおよびハードウェアの登録へのアクセス
ms.assetid: 6f735f33-0bb7-45b8-ac01-f34ec4937a8b
keywords:
- フレーム バッファー WDK Windows 2000 を表示します。
- ディスプレイ ドライバー WDK Windows 2000 のサイズを減らす
- サイズの WDK Windows 2000 の表示
- ディスプレイ ドライバー WDK Windows 2000 では、サイズの縮小
- ビデオ ハードウェアが Windows 2000 の WDK の表示を登録します
- ハードウェアが Windows 2000 の WDK の表示を登録します
- 銀行 WDK Windows 2000 を表示します。
- メモリ バンク WDK Windows 2000 を表示します。
- 線形フレーム バッファー WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88f2f3a3282b0b255fe592142232c5388ea7ef36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346279"
---
# <a name="accessing-the-frame-buffer-and-hardware-registers"></a>フレーム バッファーおよびハードウェアの登録へのアクセス


## <span id="ddk_accessing_the_frame_buffer_and_hardware_registers_gg"></span><span id="DDK_ACCESSING_THE_FRAME_BUFFER_AND_HARDWARE_REGISTERS_GG"></span>


ディスプレイ ドライバーのサイズを小さくいくつかの方法はあります。 たとえば、ディスプレイ ドライバーが GDI より高速で実行し、その他のすべての操作を実行する GDI を指定できます関数のみを実装することができます。 GDI は膨大な量に描画の多くの場合、実行*線形フレーム バッファー*ドライバーのサイズを小さくします。 GDI はアクセスできない*メモリに蓄積される*直接したがって、フレーム バッファーが直線的にアドレス指定可能でない場合、ディスプレイ ドライバーする必要があります、フレーム バッファーに分割、一連の*銀行*GDI の手段を提供。適切な銀行に描画操作を実行します。 参照してください[蓄積されるフレーム バッファーをサポートしている](supporting-banked-frame-buffers.md)詳細についてはします。

ディスプレイ ドライバーが、O マップされ、メモリ マップト ビデオ レジスタへの直接アクセスします。 このアクセスは、高パフォーマンスを実現するためにディスプレイ ドライバーを使用します。 たとえば、ドライバーは、高スループットで線の描画コマンドを送信するビデオ ハードウェア レジスタにアクセスする必要があります。

同様に、S3 などのグラフィックス カードのグラフィック エンジン コードでは、最も内側のループの多くを必要といくつかのビデオ コント ローラー ポート (たとえば、グラフィック モード、ビット ブロック転送、および線の描画でテキスト出力) の読み取りや書き込み。 IOCTL を各要求のミニポート ドライバーに送信する、ディスプレイ ドライバーを必要とするのではなく、ディスプレイ ドライバーは、ビデオ ハードウェアに直接アクセスが許可されます。

 

 





