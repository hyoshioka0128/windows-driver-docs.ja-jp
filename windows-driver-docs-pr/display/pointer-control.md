---
title: ポインターの制御
description: ポインターの制御
ms.assetid: 70e80be0-28f8-40a7-9018-fab71d80c8f6
keywords:
- 描画ポインター WDK Windows 2000 を表示します。
- ディスプレイ ドライバー WDK Windows 2000 では、ポインター
- Windows 2000 の WDK のポインターを表示します。
- ポインター情報 WDK Windows 2000 の表示を渡す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c31e49fb0ffeea2cacc4a860971af4feee692d91
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550839"
---
# <a name="pointer-control"></a>ポインターの制御


## <span id="ddk_pointer_control_gg"></span><span id="DDK_POINTER_CONTROL_GG"></span>


すべてのアプリケーションは、マウスなどのポインティング デバイスへの応答でウィンドウの表示を移動するポインターを制御できる必要があります。 ディスプレイ ドライバー、GDI、またはビデオのミニポート ドライバーできます[ポインターの描画](pointer-drawing.md)します。 参照にも[ポインターを制御する](controlling-the-pointer--drvsetpointershape.md)と[、ポインターを移動](moving-the-pointer--drvmovepointer.md)します。

GDI は、すべてのポインターが直線的にアドレス指定可能なバッファーを使用するディスプレイの描画を直接処理できます。 デバイスでの*線形フレーム バッファー*、GDI を使用して[ **DrvCopyBits** ](https://msdn.microsoft.com/library/windows/hardware/ff556182)ポインターの描画します。 ただし、ハードウェアでサポートされているし、ディスプレイ ドライバーに実装されているポインターのコードは、高速です。

ディスプレイ ドライバーはどのような種類のポインターの描画、および種類 GDI を処理することがのこともできます。 たとえば、デバイスはハードウェアでモノクロのポインターがサポートが GDI 代わりにそれらを処理することができます、色のポインターの呼び出しが失敗する可能性があります。

ディスプレイ ドライバーが排他的所有されていることがない、プロセッサが場合の状況でポインターを制御でき、ポインターが縦方向の同期割り込みなど、割り込みを描画する必要はありません。 、これらの特殊なケースでミニポート ドライバーが描画し、(これは、ビデオのミニポート ドライバーで使用できるだけ) 特定のカーネル モード コールバックが必要であるため、ポインターを制御する必要があります。 これは、パフォーマンスに悪影響 Ioctl ポインター操作ごとに、ミニポート ドライバーと通信する必要があるためです。

ディスプレイ ドライバーおよびミニポート ドライバーのペアを作成するには、2 つのドライバーの間、必要に応じて、いずれかまたはすべてのポインターの描画を想定するミニポート ドライバーを許可してをポインターの情報を渡すため Ioctl を含める必要があります。

 

 





