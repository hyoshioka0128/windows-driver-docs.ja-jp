---
title: DirectSound ハードウェア アクセラレータの概要
description: DirectSound ハードウェア アクセラレータの概要
ms.assetid: 1f18f88a-2dd6-4b7a-b083-f43ab58571b3
keywords:
- ハードウェア アクセラレータ WDK DirectSound、DirectSound ハードウェア アクセラレータについて
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 610712f39e8837e7ce687c0147b12b8ee450f1fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332237"
---
# <a name="overview-of-directsound-hardware-acceleration"></a>DirectSound ハードウェア アクセラレータの概要


## <span id="overview_of_directsound_hardware_acceleration"></span><span id="OVERVIEW_OF_DIRECTSOUND_HARDWARE_ACCELERATION"></span>


さまざまなオーディオのアダプターは、DirectSound ストリームを 1 つまたは複数のハードウェアの混在を実行する機能は DirectSound ハードウェア アクセラレータを提供します。 ハードウェアの混在と、CPU からオーディオ ミキシング操作を実行し、ハードウェアの速度で実行することによってパフォーマンスが向上します。 混在をに加えてには、ハードウェアが関連するサンプル レートの変換 (SRC) 減衰などの操作を実行し、必要に応じて、3 D 処理がソフトウェアで実行する必要がありますはそれ以外の場合。

すべての WaveCyclic または WavePci のレンダリング デバイスは、オーディオ ストリームを混在させる場合の 1 つまたは複数のハードウェアのピンを提示します。 単一ストリームのデバイスの場合、 [KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)は常に 1 つの使用可能なハードウェア レンダリング ピンでインスタンス化します。

DirectSound ハードウェア アクセラレーションを使ったデバイスは、暗証番号 (pin) を混在させる 1 つ以上のハードウェアを提供します。 DirectSound ストリームを混在させるのには、各追加の pin を使用できます。 ハードウェア ミキサーのピンにフィードする DirectSound ストリームは KMixer をバイパスし、ソフトウェア KMixer の混合の待機時間を回避します。 DirectSound は、すべてのオーディオ デバイスの使用可能なハードウェア アクセラレータによるミキサーのピンのこれらのピンがあるトポロジに準拠している限り、 [DirectSound ノード順序要件](directsound-node-ordering-requirements.md)します。 DirectSound は、ピンが KSDATAFORMAT で指定された DirectSound データ形式をサポートする必要がありますも\_指定子\_DSOUND (を参照してください[DirectSound Stream データ形式](directsound-stream-data-format.md))。

[SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver) KMixer のように、その他のストリームの KMixer で混合し、予約済みのハードウェアの暗証番号 (pin) に渡す他の (予約されていない) ハードウェア ピンがすべて割り当てられた後、1 つのハードウェア暗証番号 (pin) が常に予約します。

図に[レンダリング Wave コンテンツを使用して DirectSound ソフトウェアおよびハードウェア バッファー](rendering-wave-content-using-directsound-software-and-hardware-buffers.md)はこれらの概念を示しています。

オーディオ デバイスは、十分な数の pin を混在させるハードウェアを提供する場合は、ハードウェア アクセラレータを使用した、DirectSound アプリケーションの出力ストリームのすべてがあります。 そうでない場合、DirectSound のアプリケーションはいくつかのオプションがあります。

-   最小待機時間を必要とするストリームへのピンを混在使用可能なハードウェアに静的に割り当てることができます。

-   共有リソースのプールとしてピンを扱うことで、必要に応じて、ストリームへのピンを混在使用可能なハードウェアに動的に割り当てることができます。

詳細については、音声の管理、Microsoft Windows SDK ドキュメントの説明を参照してください。

DirectSound は、ハードウェア ミキサー ピンの 2 つの種類を使用できます。2D および 3D です。 SRC、減衰の混在しますが、いない 3D 配置 2D 暗証番号 (pin) を実行します。 DirectSound は、ソフトウェアの減衰と頻度のために必要な計算を実行する、2D の暗証番号 (pin) の適切なノードに結果を適用して 3D 配置を行う 2D 暗証番号 (pin) を使用できます。 これに対し、3D の pin には、これを行うには DirectSound で使用する代わりに 3D バッファーと 3D リスナーのプロパティから直接、独自の 3D 効果を計算することである 3D ノードが含まれています。 3D のノードのプロパティの一覧では、次を参照してください。 [ **KSNODETYPE\_3D\_効果**](https://msdn.microsoft.com/library/windows/hardware/ff537148)します。 2D と 3D の pin の詳細については、次を参照してください。 [WDM オーディオでは 2D DirectSound アクセラレーションをサポートしている](supporting-2d-directsound-acceleration-in-wdm-audio.md)と[WDM オーディオでは 3D DirectSound アクセラレーションをサポートしている](supporting-3d-directsound-acceleration-in-wdm-audio.md)します。

 




