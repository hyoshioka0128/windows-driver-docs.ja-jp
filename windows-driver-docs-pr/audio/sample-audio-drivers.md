---
title: オーディオ ドライバーのサンプル
description: オーディオ ドライバーのサンプル
ms.assetid: bea50e70-e1ec-4a66-9bfc-8bd644b07ce7
keywords:
- WDM オーディオドライバー WDK、サンプルドライバー
- オーディオドライバー WDK、サンプルドライバー
- サンプルドライバー WDK オーディオ
- Ac97 サンプル audio driver WDK audio
- Dマス uart サンプル audio driver WDK audio
- Fmsynth サンプル audio driver WDK audio
- Gfx サンプル audio driver WDK audio
- Mpu401 サンプル audio driver WDK audio
- Msvad サンプル audio driver WDK audio
- Sb16 サンプル audio driver WDK audio
- Stdunk サンプル audio driver WDK audio
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9242bb43973280df23a142e33f86d53f411ab811
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925537"
---
# <a name="sample-audio-drivers"></a>オーディオ ドライバーのサンプル


## <a name="span-idsysvad_audio_samplespanspan-idsysvad_audio_samplespanspan-idsysvad_audio_samplespansysvad-audio-sample"></a><span id="SYSVAD_Audio_Sample"></span><span id="sysvad_audio_sample"></span><span id="SYSVAD_AUDIO_SAMPLE"></span>SYSVAD Audio サンプル


**システム仮想オーディオデバイスドライバーのサンプル (SYSVAD)**

SYSVAD ドライバーは、WDM オーディオアーキテクチャの多くの重要な機能を取り上げています。 これらは、独自のオーディオデバイス用のカスタムドライバーを作成するための出発点として使用できるソースコードと共に動作する実装です。

*Sysvad*ソリューションファイルには、次のプロジェクトが含まれています。

-   **TabletAudioSample**

    *TabletAudioSample*プロジェクトは、複数のオーディオデバイスのサポートを公開する WDM オーディオドライバーを開発する方法を示しています。 これらのオーディオデバイスの中には、システムに埋め込まれているものがあります (スピーカー、mic 配列など)。 ドライバーは、レンダリングデバイスに WaveRT と audio オフロードを使用します。 ドライバーは、実際のハードウェアベースアダプターではなく "仮想オーディオデバイス" を使用し、オーディオオフロード WDM オーディオドライバーアーキテクチャのさまざまな側面を強調表示します。 Windows オーディオエンジンの詳細については、「[ハードウェアオフロードオーディオ処理 (Windows ドライバー)](hardware-offloaded-audio-processing.md)」を参照してください。

-   **電話のオーディオサンプル**

    *TabletAudioSample* *プロジェクトとよく似てい*ます。 モバイルデバイスの最適化が含まれています。

-   **EndpointsCommon**

    *Endpointscommon*プロジェクトには、タブレットとスマートフォンの両方に共通のコードが含まれています。 詳細については、「[ユニバーサル Windows Drivers For Audio](audio-universal-drivers.md)」を参照してください。

-   **SwapAPO**

    *Swapapo*プロジェクトは、オーディオ処理オブジェクトを開発する方法を示しています。 これには、オーディオ処理オブジェクトの登録と登録解除の方法を示すサンプルコードが含まれています。また、処理オブジェクトで使用可能な機能を反映するようにコントロールパネルのプロパティページをカスタマイズする方法も示しています。 詳細については、「 [Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)」を参照してください。

-   **KeywordDetectorAdapter**

    *KeywordDetectorAdapter*プロジェクトは、キーワード検出アダプターを開発する方法を示しています。 詳細については、「[音声ライセンス認証](voice-activation.md)」を参照してください。

**GitHub から Sysvad audio サンプルをダウンロードして抽出する**

SYSVAD audio サンプルは、 [Windows Driver Samples GitHub](https://github.com/Microsoft/Windows-driver-samples)で入手できます。

Sysvad audio サンプルは次の場所で参照できます。

<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

SYSVAD サンプルをダウンロードして開くには、次の手順に従います。

a. GitHub ツールを使用して、サンプルを操作できます。 また、ユニバーサルドライバーのサンプルを1つの zip ファイルにダウンロードすることもできます。

<https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

b. マスター .zip ファイルをローカルハードドライブにダウンロードします。

c. *Windows-driver-samples-master*を右クリックし、[**すべて展開**] を選択します。 新しいフォルダーを指定するか、抽出されたファイルを格納する既存のフォルダーを参照します。 たとえば、ファイルを抽出する新しいフォルダーとして*C:\\driversamples\\ *を指定することができます。

d. ファイルが抽出されたら、次のサブフォルダーに移動します。

*C:\\driversamples\\Audio\\Sysvad*

**Visual Studio でドライバーソリューションを開く**

Microsoft Visual Studio で、[**ファイル** &gt; ] [**開く** &gt; ] [**プロジェクト/ソリューション...** ] の順にクリックし、抽出したファイルが格納されているフォルダー (例 *: C:\\driversamples\\Audio\\Sysvad*) に移動します。 *Sysvad*ソリューションファイルをダブルクリックして開きます。

Visual Studio で、ソリューションエクスプローラーを見つけます。 (まだ開いていない場合は、[**表示**] メニューの [**ソリューションエクスプローラー** ] をクリックします)。ソリューションエクスプローラーには、6つのプロジェクトを持つソリューションが1つ表示されます。

## <a name="span-idsample_audio_driversspanspan-idsample_audio_driversspanarchived-audio-samples"></a><span id="sample_audio_drivers"></span><span id="SAMPLE_AUDIO_DRIVERS"></span>アーカイブされたオーディオのサンプル


これらのオーディオサンプルでは、以前のバージョンの Microsoft Windows Driver Kit (WDK) がサポートされています。 これらは、[こちらで](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples)入手できる zip ファイルのダウンロードの一部として入手できます。

-   **Microsoft 仮想オーディオデバイスドライバーのサンプル (Msvad)**

-   **AC97 ドライバー (Ac97)**

-   **DirectMusic UART Driver サンプル (Dマス Uart)**

-   **DirectMusic ソフトウェアシンセサイザーのサンプル (ddksynth)**

-   **FM シンセサイザー (Fmsynth)**

-   **オーディオアダプターのサンプル**

**オーディオ処理コーデックのサンプル**

-   **Msfilter サンプルコーデック (MsFilter)**

-   **.Msgsm610 サンプルコーデック (gsm610)**

詳細については、WDK の各サンプルに付属している readme ドキュメントを参照してください。

WDK のサンプルについては、「 [Windows Driver Kit Samples Pack (Windows ドライバー)](https://docs.microsoft.com/windows-hardware/drivers/samples/index) 」を参照してください。

 

 




