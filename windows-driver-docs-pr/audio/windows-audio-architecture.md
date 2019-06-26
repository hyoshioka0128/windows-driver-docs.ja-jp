---
title: Windows オーディオ アーキテクチャ
description: このトピックでは、Windows 10 のオーディオ アーキテクチャの概要が提供されています。
ms.assetid: 1FC95504-18AA-4F3B-8E96-005276699694
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3b5cb95051e1f524cdf164d2336f7e6a46a318f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354092"
---
# <a name="windows-audio-architecture"></a>Windows オーディオ アーキテクチャ


このトピックでは、Windows 10 のオーディオ アーキテクチャの概要が提供されています。

## <a name="span-idwindows10audiostackdiagramspanspan-idwindows10audiostackdiagramspanspan-idwindows10audiostackdiagramspanwindows-10-audio-stack-diagram"></a><span id="Windows_10_Audio_Stack_Diagram"></span><span id="windows_10_audio_stack_diagram"></span><span id="WINDOWS_10_AUDIO_STACK_DIAGRAM"></span>Windows 10 のオーディオ スタックの図


この図では、Windows 10 のオーディオ スタックの主要な要素の概要を示します。

![アプリ、オーディオ エンジン、ドライバーおよびハードウェアを示す windows 10 オーディオ スタックの図 ](images/audio-windows-10-stack-diagram.png)

## <a name="span-idapisspanspan-idapisspanspan-idapisspanapis"></a><span id="APIs"></span><span id="apis"></span><span id="APIS"></span>Api


**最上位レベルの Api**

最上位レベルの Api は、アプリケーションの開発に使用されます。 これらの Api で現在使用中し、サポートされています。

-   XAML [MediaElement クラス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement)(C#、VB、C++)
-   HTML[オーディオ オブジェクト](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio)と[ビデオ オブジェクト](https://developer.mozilla.org/en-US/docs/Web/API/HTMLVideoElement)&lt;タグ&gt;(web サイトおよび Windows Web アプリで使用)
-   [名前空間の Windows.Media.Capture](https://docs.microsoft.com/uwp/api/Windows.Media.Capture) (C#、VB、C++)
-   [Microsoft Media Foundation](https://docs.microsoft.com/windows/desktop/medfound/microsoft-media-foundation-sdk) (C++)

これらの古い Api が非推奨とされます。

-   [DirectShow](https://docs.microsoft.com/windows/desktop/DirectShow/directshow)
-   [DirectSound](https://docs.microsoft.com/previous-versions/windows/desktop/ee416960(v=vs.85))
-   [PlaySound](https://docs.microsoft.com/previous-versions/dd743680(v=vs.85))
-   [Windows.Media.MediaControlContract](https://docs.microsoft.com/uwp/extension-sdks/windows-desktop-extension-sdk)

**低レベルの Api**

オーディオのストリーミングには、これらの下位レベル Api がお勧めします。

-   [WASAPI](https://docs.microsoft.com/windows/desktop/CoreAudio/wasapi) (高パフォーマンス、ただしより複雑です)
-   [IXAudio2](https://docs.microsoft.com/windows/desktop/api/xaudio2/nn-xaudio2-ixaudio2) (通常はゲームに使用)
-   [MIDI](https://docs.microsoft.com/windows/desktop/Multimedia/about-midi)

列挙には、この下位レベル API を使用することをお勧めします。

-   [Windows.Devices.Enumeration](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration)

これらの Api は Windows アプリケーションでは推奨されません。

-   [MMDevice API について](https://docs.microsoft.com/windows/desktop/CoreAudio/mmdevice-api)(Windows.Devices.Enumeration に置き換え)
-   [DeviceTopology API](https://docs.microsoft.com/windows/desktop/CoreAudio/devicetopology-api)
-   [EndpointVolume API](https://docs.microsoft.com/windows/desktop/CoreAudio/endpointvolume-api)

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








