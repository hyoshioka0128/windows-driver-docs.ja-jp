---
title: PCI ベース テレビのキャプチャ
description: PCI ベース テレビのキャプチャ
ms.assetid: ae97d5f7-82de-4d6e-9835-ff4c7427f333
keywords:
- グラフ構成 WDK ビデオ キャプチャ、テレビの PCI ベースのキャプチャをフィルター処理します。
- テレビの PCI ベース WDK ビデオ キャプチャをキャプチャします。
- テレビ キャプチャ WDK ビデオのキャプチャ
- テレビ キャプチャ WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7afab4fbfde1e8ecc4175c8614c575790048220
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560334"
---
# <a name="pci-based-tv-capture"></a>PCI ベース テレビのキャプチャ


テレビやラジオ チューナー、テレビのオーディオ、およびクロスバー PCI ベースのキャプチャ デバイスのフィルターの複雑なグラフでは、必要な対応している多くの場合、それぞれに異なる可能性がある色空間とフレームを別のプレビューとキャプチャ ストリーム、バスのハードウェアディメンション。 このようなデバイスでは、VBI またはタイムコードも個別のストリームを提供できます。

次の図は、プレビューとキャプチャのストリームに接続されている別のレンダラーを示しています。

![プレビューとキャプチャのストリームに接続されている別のレンダラーを示す図](images/pci-tvtuner.gif)

[PROPSETID\_アロケーター\_コントロール](https://msdn.microsoft.com/library/windows/hardware/ff567792)プロパティ セットがこの種類のグラフのフィルターを特定します。

この種類のグラフのフィルター オプションのバリエーションがプレビュー ピンを標準のビデオのレンダラーではなくビデオ Mixer/レンダラー (VMR) DirectShow フィルターを使用して接続するのには、 [ **KS\_VIDEOINFOHEADER2**](https://msdn.microsoft.com/library/windows/hardware/ff567702)構造形式。 ディスプレイ デバイスのビデオ ポート マネージャー (VPM) をサポートするこのモードで構成すると、[拡張機能のビデオ ポート](video-port-based-capture.md)(VPEs) カーネル モードのビデオ トランスポートでは、バッファーは、Microsoft と共にキャプチャ デバイスに渡されます。DirectDraw surface の処理で、 [ **KS\_フレーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567645)構造体。

ビデオ キャプチャ ミニドライバーは、所有権、バッファーの無期限に--ロック、入力、ロック解除、およびそれらがキャプチャされると、サーフェスを反転し、保持できます。 ミニドライバーは、全画面表示 MS-DOS アプリケーションや排他モードのゲームの実行中に画面の損失を示す通知を登録する必要があります。 このような場合、ミニドライバーは、キャプチャ フィルターにバッファーを完了します。

ビデオ キャプチャ ハードウェアには、FM ラジオ チューナーが含まれている場合は、次を参照してください。[ラジオ チューナーでのビデオ キャプチャ デバイス](video-capture-devices-with-radio-tuners.md)します。

 

 




