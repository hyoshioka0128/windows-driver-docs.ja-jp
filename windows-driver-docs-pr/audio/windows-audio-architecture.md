---
title: Windows オーディオ アーキテクチャ
description: このトピックでは、Windows 10 のオーディオ アーキテクチャの概要が提供されています。
ms.assetid: 1FC95504-18AA-4F3B-8E96-005276699694
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78b2b241feb5c90811a787e2d38b355764795172
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335362"
---
# <a name="windows-audio-architecture"></a>Windows オーディオ アーキテクチャ


このトピックでは、Windows 10 のオーディオ アーキテクチャの概要が提供されています。

## <a name="span-idwindows10audiostackdiagramspanspan-idwindows10audiostackdiagramspanspan-idwindows10audiostackdiagramspanwindows-10-audio-stack-diagram"></a><span id="Windows_10_Audio_Stack_Diagram"></span><span id="windows_10_audio_stack_diagram"></span><span id="WINDOWS_10_AUDIO_STACK_DIAGRAM"></span>Windows 10 のオーディオ スタックの図


この図では、Windows 10 のオーディオ スタックの主要な要素の概要を示します。

![アプリ、オーディオ エンジン、ドライバーおよびハードウェアを示す windows 10 オーディオ スタックの図 ](images/audio-windows-10-stack-diagram.png)

## <a name="span-idapisspanspan-idapisspanspan-idapisspanapis"></a><span id="APIs"></span><span id="apis"></span><span id="APIS"></span>Api


**最上位レベルの Api**

最上位レベルの Api は、アプリケーションの開発に使用されます。 これらの Api で現在使用中し、サポートされています。

-   XAML [MediaElement クラス](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.mediaelement)(C#、VB、C++)
-   HTML[オーディオ オブジェクト](https://msdn.microsoft.com/library/windows/apps/hh767373.aspx)と[ビデオ オブジェクト](https://msdn.microsoft.com/library/windows/apps/hh767390.aspx)&lt;タグ&gt;(web サイトおよび Windows Web アプリで使用)
-   [名前空間の Windows.Media.Capture](https://msdn.microsoft.com/library/windows/apps/xaml/windows.media.capture) (C#、VB、C++)
-   [Microsoft Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197) (C++)

これらの古い Api が非推奨とされます。

-   [DirectShow](https://msdn.microsoft.com/library/windows/desktop/dd375454)
-   [DirectSound](https://msdn.microsoft.com/library/ee416960.aspx)
-   [PlaySound](https://msdn.microsoft.com/library/dd743680)
-   [Windows.Media.MediaControlContract](https://msdn.microsoft.com/library/windows/apps/dn706169)

**低レベルの Api**

オーディオのストリーミングには、これらの下位レベル Api がお勧めします。

-   [WASAPI](https://msdn.microsoft.com/library/windows/desktop/dd371455) (高パフォーマンス、ただしより複雑です)
-   [IXAudio2](https://msdn.microsoft.com/library/windows/desktop/ee415908) (通常はゲームに使用)
-   [MIDI](https://msdn.microsoft.com/library/windows/desktop/dd742875)

列挙には、この下位レベル API を使用することをお勧めします。

-   [Windows.Devices.Enumeration](https://msdn.microsoft.com/library/windows/apps/br225459)

これらの Api は Windows アプリケーションでは推奨されません。

-   [MMDevice API について](https://msdn.microsoft.com/library/windows/desktop/dd316556)(Windows.Devices.Enumeration に置き換え)
-   [DeviceTopology API](https://msdn.microsoft.com/library/windows/desktop/dd370809)
-   [EndpointVolume API](https://msdn.microsoft.com/library/windows/desktop/dd370832)

## <a name="span-idaudioenginespanspan-idaudioenginespanspan-idaudioenginespanaudio-engine"></a><span id="Audio_Engine"></span><span id="audio_engine"></span><span id="AUDIO_ENGINE"></span>オーディオ エンジン


オーディオ エンジンは、2 つの関連コンポーネント、オーディオ エンジン (audioeng.dll) を読み込みますオーディオ デバイス グラフ (audiodg.exe) で構成されます。

オーディオ エンジン:

-   混在し、オーディオ ストリームを処理します。 オーディオ エンジンでバッファーを使用して、オーディオを転送する方法の詳細については、次を参照してください。 [WaveRT ポート ドライバーについて](understanding-the-wavert-port-driver.md)します。
-   オーディオ処理オブジェクト (APOs) オーディオ信号の処理 H または W の特定のプラグインを読み込みます。 パスワードの詳細については、次を参照してください。 [Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)します。

## <a name="span-idaudioserviceaudiosrvdllspanspan-idaudioserviceaudiosrvdllspanaudio-service-audiosrvdll"></a><span id="audio_service__audiosrv.dll_"></span><span id="AUDIO_SERVICE__AUDIOSRV.DLL_"></span>オーディオのサービス (audiosrv.dll)


オーディオのサービス:

-   セットアップし、オーディオ ストリームの制御に使用されます。
-   バック グラウンド オーディオ再生をかわすなどの Windows ポリシーを実装します。

## <a name="span-idaudioendpointbuilderaudioendpointbuilderexespanspan-idaudioendpointbuilderaudioendpointbuilderexespanaudio-endpoint-builder-audioendpointbuilderexe"></a><span id="audio_endpoint_builder__audioendpointbuilder.exe_"></span><span id="AUDIO_ENDPOINT_BUILDER__AUDIOENDPOINTBUILDER.EXE_"></span>オーディオ エンドポイント ビルダー (audioendpointbuilder.exe)


オーディオ エンドポイント ビルダー (audioendpointbuilder.exe):

-   新しいオーディオ デバイスを検出し、ソフトウェア オーディオ エンドポイントの作成に使用されます。 使用されるアルゴリズムの詳細については、次を参照してください。[オーディオ エンドポイント ビルダー アルゴリズム](audio-endpoint-builder-algorithm.md)します。

## <a name="span-idaudiodriversspanspan-idaudiodriversspanspan-idaudiodriversspanaudio-drivers"></a><span id="Audio_Drivers"></span><span id="audio_drivers"></span><span id="AUDIO_DRIVERS"></span>オーディオ ドライバー


オーディオ ドライバー:

-   ポート ミニポート モデルに従います。 詳細については、次を参照してください。 [WDM オーディオ用語](wdm-audio-terminology.md)と[WaveRT ミニポート ドライバーを開発](developing-a-wavert-miniport-driver.md)します。
-   オーディオを含む複数のオーディオ デバイスから、オーディオ スタックを表示し、キャプチャを許可する: 統合のスピーカーやヘッドセット/ヘッドホン、マイクの USB デバイス、Bluetooth デバイス、HDMI など。
-   ポート ミニポート モデルは Linux のサウンドのアーキテクチャの高度な ALSA に対応します。
-   ドライバーのサンプル コードについては、次を参照してください。[サンプル オーディオ ドライバー](sample-audio-drivers.md)します。

## <a name="span-idhardwarespanspan-idhardwarespanspan-idhardwarespanhardware"></a><span id="Hardware"></span><span id="hardware"></span><span id="HARDWARE"></span>ハードウェア


任意の特定のデバイスに存在するオーディオ ハードウェアによって異なりますが、含めることができます。

-   オーディオ コーデック
-   (省略可能) DSP
-   統合されたスピーカー、マイクなど
-   外部デバイス:USB オーディオ デバイス、Bluetooth のオーディオ デバイス、HDMI オーディオなど。
-   H または W (例: コーデックまたは DSP) の代わりに、または、APOs だけでなく、信号処理を実装することもできます。








