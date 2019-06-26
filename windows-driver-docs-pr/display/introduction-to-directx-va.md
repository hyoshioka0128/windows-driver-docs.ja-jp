---
title: DirectX VA の概要
description: DirectX VA の概要
ms.assetid: e7d4faf7-f6ec-49ec-8116-faeed1ddd01c
keywords:
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示、DirectX ビデオ アクセラレータについて
- ビデオ アクセラレータ WDK DirectX では、DirectX ビデオ アクセラレータについて
- VA WDK DirectX では、DirectX ビデオ アクセラレータについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34cd076af5b9c3a5fd24de77d4696cf2e371fdac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379866"
---
# <a name="introduction-to-directx-va"></a>DirectX VA の概要


## <span id="ddk_introduction_to_directx_va_gg"></span><span id="DDK_INTRODUCTION_TO_DIRECTX_VA_GG"></span>


DirectX VA は、頻繁が実行されて、ハードウェア アクセラレータで実行する簡単なビデオ処理できます。 ビデオのデコード アクセラレータをアクセラレータに最小限のカスタマイズのさまざまなビデオ規格を実現するのには、アクセラレータにあまり複雑なビデオ処理操作に限定できます。 ビデオの処理があまり頻繁に実行されるとビット ストリームなどのより複雑な解析操作と可変長 (VLD) をデコードはホストの CPU。

DirectX の VA API および対応する[補正のモーション](motion-compensation.md)DDI では、次の操作のサポート。

-   [アルファ ブレンド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)DVD などの目的でサブピクチャ サポートをします。

-   [暗号化](encryption-support.md)を必要とするアプリケーション。

-   [デインター レース、フレーム レート変換](deinterlacing-and-frame-rate-conversion.md)ビデオ コンテンツの。

-   [ProcAmp](procamp-control-processing.md)を制御し、ビデオ コンテンツの処理を投稿します。

-   コピーとを表示する権限がありませんからビデオのコンテンツの保護、[出力保護のプロトコルの認定](copp-processing.md)します。

ここで説明する情報は、アプリケーションとデバイス ドライバー開発者向けの両方に適用されます。 指定された形式では、ユーザー モードのホスト デコーダーとカーネル モード デバイス ドライバーの間の情報を交換する方法を定義します。 ほとんどの場合、デバイス ドライバーをホストから、データは転送が、場合によっては、他の方向にデータを送信します。

Windows media ビデオ形式をデコードするためのサンプル コードでは、Windows メディア Porting Kit では、Windows メディア サンプル ドライバーを参照してください。 Windows Media Porting Kit は、Windows media 形式にオーディオとビデオの変換に使用されます。

Windows media 形式のサポートは、Windows Media ビデオ コーデックのバージョン 9 以降を使用する必要があります。 Windows Media ビデオ コーデック 8 が Windows XP に付属のバージョンは DirectX 問い合わせください。 をサポートしていません

使用するディスプレイ ドライバー、 [DDI デインター レース](deinterlacing-and-frame-rate-conversion.md)、ビデオ コンテンツのインター レースし、正しくインター レースとしてマークされている必要があります。 ミキシング レンダラー (VMR) ビデオでは、デインター レース DDI と共に VIDEOINFOHEADER2 構造体を使用して、インター レースを解除し、フレーム レートの変換を実行します。 VIDEOINFOHEADER2 構造の詳細については、Windows SDK のドキュメントを参照してください。

[ProcAmp コントロール DDI](procamp-control-processing.md) ProcAmp コントロールをサポートし、グラフィック デバイス ドライバー、ビデオ コンテンツの処理を投稿する DirectX VA を拡張します。 既存の DirectDraw と DirectX VA DDI DDI にマップします。 DDI がからアクセスできない、 **IAMVideoAccelerator**インターフェイス。 DDI ProcAmp コントロールは、Microsoft DirectX 9.0 と以降のバージョンのみで使用できます。

[現在標準実装](implementation-of-current-standards.md)トピックでは、ハードウェア アクセラレータと、次の動き補償ビデオ コーデックの標準を満たすソフトウェア デコーダーの要件について。ITU-T H.261、mpeg-1、mpeg-2 (H.262)、ITU-T H.263、mpeg-4、mpeg-4 AVC (H.264) および vc-1 です。

DirectX の問い合わせください。 付属ツールはありません。 Windows media のサポートを提供するツールの詳細については、Windows Media Porting Kit を参照してください。

 

 





