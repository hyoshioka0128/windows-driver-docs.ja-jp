---
title: オーディオ ドライバーのサンプル
description: オーディオ ドライバーのサンプル
ms.assetid: bea50e70-e1ec-4a66-9bfc-8bd644b07ce7
keywords:
- WDM オーディオ ドライバー WDK サンプル ドライバー
- オーディオ ドライバー WDK サンプル ドライバー
- サンプル ドライバー WDK オーディオ
- Ac97 サンプル オーディオ ドライバー WDK オーディオ
- Dmusuart サンプル オーディオ ドライバー WDK オーディオ
- Fmsynth サンプル オーディオ ドライバー WDK オーディオ
- Gfx サンプル オーディオ ドライバー WDK オーディオ
- Mpu401 サンプル オーディオ ドライバー WDK オーディオ
- Msvad サンプル オーディオ ドライバー WDK オーディオ
- Sb16 サンプル オーディオ ドライバー WDK オーディオ
- Stdunk サンプル オーディオ ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 797b125b9aca5968b380e511c40fda3ee731a4d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580219"
---
# <a name="sample-audio-drivers"></a>オーディオ ドライバーのサンプル


## <a name="span-idsysvadaudiosamplespanspan-idsysvadaudiosamplespanspan-idsysvadaudiosamplespansysvad-audio-sample"></a><span id="SYSVAD_Audio_Sample"></span><span id="sysvad_audio_sample"></span><span id="SYSVAD_AUDIO_SAMPLE"></span>SYSVAD オーディオ サンプル


**システム オーディオの仮想デバイス ドライバーのサンプル (SYSVAD)**

SYSVAD ドライバーには、WDM オーディオ アーキテクチャの多くの重要な機能が強調表示されます。 これらは、独自のオーディオ デバイス用のカスタム ドライバーを作成するための開始点として使用できるソース コードで実装を作業しています。

*Sysvad*ソリューション ファイルには、次のプロジェクトが含まれています。

-   **TabletAudioSample**

    *TabletAudioSample*プロジェクトは、複数のオーディオ デバイスのサポートを公開している WDM オーディオ ドライバーを開発する方法を示します。 プラグ可能な他のユーザーは、システムの埋め込み (スピーカー、マイク配列) は一部のオーディオ デバイス (ヘッドホンによる立体音響スピーカー/mic、Bluetooth ヘッドセット スピーカー/mic)。 ドライバーは WaveRT および表示デバイスのオーディオのオフロードを使用します。 ドライバーは、実際のハードウェア ベースのアダプターではなく「仮想オーディオ デバイス」を使用し、WDM オーディオ ドライバーのアーキテクチャがオフロードされたオーディオのさまざまな側面が強調表示されます。 Windows オーディオ エンジンの詳細については、[Hardware-Offloaded オーディオ処理 (Windows ドライバー)](hardware-offloaded-audio-processing.md)を参照してください。

-   **PhoneAudioSample**

    *PhoneAudioSample*プロジェクトのとよく似ていますが、 *TabletAudioSample*プロジェクト。 これには、モバイル デバイス向けの最適化が含まれます。

-   **EndpointsCommon**

    *EndpointsCommon*プロジェクトには、電話とタブレットの両方に共通のコードが含まれています。 詳細については、[オーディオのユニバーサル Windows ドライバー](audio-universal-drivers.md)を参照してください。

-   **SwapAPO**

    *SwapAPO*プロジェクトは、オーディオ処理オブジェクトを開発する方法を示します。 登録して、オーディオ処理オブジェクトの登録を解除する方法を示すサンプル コードが含まれていて、オブジェクトの処理で使用できる機能を反映するようにコントロール パネルの プロパティ ページをカスタマイズする方法についても説明します。 詳細については、[Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)を参照してください。

-   **KeywordDetectorAdapter**

    *KeywordDetectorAdapter*プロジェクトは、キーワード detector アダプターを開発する方法を示します。 詳細については、[音声をアクティブ化](voice-activation.md)を参照してください。

**ダウンロードして、GitHub から Sysvad オーディオ サンプルを抽出**

SYSVAD オーディオ サンプルで使用できる、 [Windows ドライバーのサンプル GitHub](https://github.com/Microsoft/Windows-driver-samples)します。

Sysvad オーディオ サンプルは、ここを参照できます。

<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

以下の手順をダウンロードして SYSVAD サンプルを開きます。

a.  GitHub ツールを使用して、サンプルを使用することができます。 1 つの zip ファイルに汎用ドライバー サンプルをダウンロードすることもできます。

<https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

b.  Master.zip ファイルをローカル ハード ドライブにダウンロードします。

c. 右クリックして*Windows ドライバーのサンプル-master.zip*、選択**すべて展開**します。 新しいフォルダーを指定するか、抽出したファイルを保存する既存のサブスクリプションへの参照します。 たとえば、指定する*c:\\DriverSamples\\* として新しいファイルの抽出先フォルダーです。

d. ファイルが抽出されると、次のサブフォルダーに移動します。

*C:\\DriverSamples\\オーディオ\\Sysvad*

**Visual Studio でのドライバー ソリューションを開く**

Microsoft Visual Studio]、[クリックして**ファイル** &gt; **オープン** &gt; **プロジェクト/ソリューション.** を抽出したファイルを含むフォルダーに移動します (たとえば、 *c:\\DriverSamples\\オーディオ\\Sysvad*)。 ダブルクリックして、 *Sysvad*ソリューション ファイルを開きます。

Visual Studio では、ソリューション エクスプ ローラーを見つけます。 (これがまだ開いていない場合は、選択**ソリューション エクスプ ローラー**から、**ビュー**メニュー)。ソリューション エクスプ ローラーでは、6 つのプロジェクトを含む 1 つのソリューションを確認できます。

## <a name="span-idsampleaudiodriversspanspan-idsampleaudiodriversspanarchived-audio-samples"></a><span id="sample_audio_drivers"></span><span id="SAMPLE_AUDIO_DRIVERS"></span>アーカイブされたオーディオ サンプル


これらのオーディオ サンプルでは、以前のバージョンの Microsoft Windows Driver Kit (WDK) をサポートします。 利用できる使用可能な zip ファイルのダウンロードの一環として[ここ](https://go.microsoft.com/fwlink/p/?LinkId=618052)します。

-   **Microsoft 仮想のオーディオ デバイス ドライバーのサンプル (Msvad)**

-   **AC97 ドライバー (Ac97)**

-   **DirectMusic UART ドライバー サンプル (Dmusuart)**

-   **DirectMusic ソフトウェア シンセサイザー サンプル (ddksynth)**

-   **FM シンセサイザー (Fmsynth)**

-   **オーディオのアダプターのサンプル**

**処理のオーディオ コーデックのサンプル**

-   **Msfilter サンプル コーデック (MsFilter)**

-   **Msgsm610 サンプル コーデック (gsm610)**

詳細については、各 WDK でこれらのサンプルに付属する readme ドキュメントを参照してください。

WDK サンプルについては、次を参照してください。 [Windows ドライバー キット サンプル パック (Windows ドライバー)。](https://msdn.microsoft.com/library/windows/hardware/ff554118)

 

 




