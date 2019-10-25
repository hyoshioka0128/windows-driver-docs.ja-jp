---
title: DirectX VA の概要
description: DirectX VA の概要
ms.assetid: e7d4faf7-f6ec-49ec-8116-faeed1ddd01c
keywords:
- Directx ビデオアクセラレータ WDK Windows 2000 display、DirectX Video アクセラレーションについて
- ビデオアクセラレーション WDK DirectX、DirectX ビデオアクセラレータについて
- VA WDK DirectX、DirectX ビデオアクセラレータについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9cfbd09ebc6abf521333e2eda8990126605bcb3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840347"
---
# <a name="introduction-to-directx-va"></a>DirectX VA の概要


## <span id="ddk_introduction_to_directx_va_gg"></span><span id="DDK_INTRODUCTION_TO_DIRECTX_VA_GG"></span>


DirectX VA では、頻繁に実行されるビデオ処理操作と、ハードウェアアクセラレータによる実行が可能です。 アクセラレータに対して複雑なビデオ処理操作を存在することで、ビデオのデコードアクセラレーションを、アクセラレータに対して最小限のカスタマイズでさまざまなビデオ標準で実現できます。 ビットストリーム解析や可変長デコード (VLD) など、実行頻度が低いビデオ処理操作は、ホストの CPU で実行できます。

DirectX VA API および対応する[モーション補正](motion-compensation.md)DDI は、次の操作のサポートを提供します。

-   DVD サブピクチャサポートなどの目的での[アルファブレンド](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

-   それを必要とするアプリケーションの[暗号化](encryption-support.md)。

-   ビデオコンテンツの[インターレース解除とフレームレート変換](deinterlacing-and-frame-rate-conversion.md)。

-   ビデオコンテンツの[ProcAmp](procamp-control-processing.md)制御と後処理。

-   [認定出力保護プロトコル](copp-processing.md)を使用して、承認されていないコピーや表示からビデオコンテンツを保護します。

ここに示されている情報は、アプリケーションとデバイスドライバーの開発者の両方に適用されます。 指定された形式は、ユーザーモードのホストデコーダーとカーネルモードデバイスドライバーの間で情報を交換する方法を定義します。 ほとんどの場合、データはホストからデバイスドライバーに転送されますが、場合によっては、データが別の方向に送信されることもあります。

Windows media ビデオ形式のデコードに使用するサンプルコードについては、「windows media 移植キット」の「Windows media サンプルドライバー」を参照してください。 Windows Media 移植キットは、オーディオとビデオを Windows メディア形式に変換するために使用されます。

Windows メディア形式をサポートするには、Windows Media Video コーデックバージョン9以降を使用する必要があります。 Windows XP に付属している windows Media Video コーデックバージョン8では、DirectX VA はサポートされていません。

[ノンインターレース DDI](deinterlacing-and-frame-rate-conversion.md)を使用するディスプレイドライバーでは、ビデオコンテンツをインターレースし、インターレースとして適切にマークする必要があります。 ビデオミキシングレンダラー (VMR) では、VIDEOINFOHEADER2 構造体をノンインターレース DDI と共に使用して、インターレースを解除し、フレームレート変換を実行します。 VIDEOINFOHEADER2 構造体の詳細については、Windows SDK のドキュメントを参照してください。

[ProcAmp コントロール DDI](procamp-control-processing.md)は、DirectX VA を拡張して、グラフィックスデバイスドライバーによるビデオコンテンツの ProcAmp 制御と後処理をサポートします。 DDI は、既存の DirectDraw および DirectX VA DDI にマップされます。 DDI は、 **Iamvideoaccelerator**インターフェイスを介してアクセスできません。 ProcAmp コントロール DDI は、Microsoft DirectX 9.0 以降のバージョンでのみ使用できます。

[現在の標準トピックの実装](implementation-of-current-standards.md)では、モーション補正ビデオコーデックの標準に適合するために満たす必要があるハードウェアアクセラレータとソフトウェアデコーダーの要件について詳しく説明しています。これは、Itu-t-261、mpeg-2、Mpeg-2 (.h)、itu-t、mpeg-2、mpeg-4、MPEG-2 AVC (h.264) と VC-1。

DirectX VA で提供されるツールはありません。 Windows media サポート用に提供されているツールの詳細については、「Windows Media 移植キット」を参照してください。

 

 





