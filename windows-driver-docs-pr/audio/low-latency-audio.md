---
title: 低遅延オーディオ
description: このトピックでは、Windows 10 でのオーディオの待機時間の変更について説明します。 低待機時間のオーディオをサポートするために可能なドライバーの変更と同様に、アプリケーション開発者の API オプションを説明します。
ms.assetid: 888AEF01-271D-41CD-8372-A47551348959
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eaba9c3798c396e8198024f9a4b0368130e7d35
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358707"
---
# <a name="low-latency-audio"></a>低遅延オーディオ


このトピックでは、Windows 10 でのオーディオの待機時間の変更について説明します。 低待機時間のオーディオをサポートするために可能なドライバーの変更と同様に、アプリケーション開発者の API オプションを説明します。

このトピックは次のセクションで構成されます。

-   [概要](#overview)
-   [定義](#definitions)
-   [Windows オーディオ スタック](#windows_audio_stack)
-   [Windows 10 でのオーディオ スタックの機能強化](#audio_stack_improvements_in_windows_10)
-   [API の強化](#api_improvements)
-   [AudioGraph](#audiograph)
-   [Windows の音声セッション API (WASAPI)](#windows_audio_session_api_wasapi)
-   [ドライバの改善](#driver_improvements)
-   [評価ツール](#measurement_tools)
-   [サンプル](#samples)
-   [FAQ](#faq)

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要


オーディオの待機時間は、その時点のサウンドの間の遅延が作成され、聞いたときに。 オーディオの待ち時間を持つことは、次のようないくつかの主要なシナリオ、非常に重要です。

-   Pro オーディオ
-   音楽の作成
-   Communications
-   仮想現実
-   ゲーム

Windows 10 には、オーディオの待機時間を短縮する変更が含まれています。 このドキュメントの目的は次のとおりです。

1. Windows でのオーディオの待機時間のソースについて説明します。
2. Windows 10 のオーディオ スタックでオーディオの待機時間を短縮する変更について説明します。
3. どのアプリケーションの開発者およびハードウェアの製造元利用に関する、新しいインフラストラクチャのオーディオの待ち時間を使用したアプリケーションやドライバーを開発するために参照を提供します。 このトピックでは、これらの項目について説明します。
4. 新しい[ **AudioGraph** ](https://docs.microsoft.com/uwp/api/Windows.Media.Audio.AudioGraph) API の対話型とメディアの作成シナリオ。
5. 低待機時間をサポートするために WASAPI で変更します。
6. Ddi ドライバーでの機能強化。

## <a name="span-iddefinitionsspanspan-iddefinitionsspanspan-iddefinitionsspandefinitions"></a><span id="Definitions"></span><span id="definitions"></span><span id="DEFINITIONS"></span>定義


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>項目</p></td>
<td align="left"><p>説明</p></td>
</tr>
<tr class="even">
<td align="left"><p>待機時間を表示します。</p></td>
<td align="left"><p>アプリケーションは、Api、スピーカーから聞いたときまでのレンダリングにオーディオ データのバッファーを送信するまでの時間遅延します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>待機時間をキャプチャします。</p></td>
<td align="left"><p>サウンドがキャプチャ アプリケーションによって使用されている Api に送信されるまで、マイクからキャプチャされた時間間隔します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ラウンド トリップの待機時間</p></td>
<td align="left"><p>サウンドのマイクからキャプチャされた、アプリケーションによって処理およびスピーカーにレンダリング アプリケーションで送信されるまでの間の遅延します。 待機時間を表示 + キャプチャ待機時間がほぼ等しくなります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>タッチからアプリの間の待機時間</p></td>
<td align="left"><p>ユーザーがアプリケーションに信号が送信されるまで、画面をタップするまでの時間遅延します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>タッチのサウンドに待機時間</p></td>
<td align="left"><p>スピーカーを使用して、音が聞こえるし、画面では、イベントをタップするまでの間の遅延が、アプリケーションに送られます。 待機時間 + タッチからアプリの間の待機時間を表示するために等しくなります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idwindowsaudiostackspanspan-idwindowsaudiostackspanspan-idwindowsaudiostackspanwindows-audio-stack"></a><span id="Windows_Audio_Stack"></span><span id="windows_audio_stack"></span><span id="WINDOWS_AUDIO_STACK"></span>Windows オーディオ スタック


次の図は、Windows オーディオ スタックの簡略化されたバージョンを示します。

![アプリ、オーディオ エンジン ドライバーおよびハードウェアを示す短い待機時間オーディオ スタックの図](images/low-latency-audio-stack-diagram-1.png)

レンダリング パスで待機時間の概要を次に示します。

1. アプリケーションでは、バッファーにデータを書き込みます
2. オーディオ エンジンは、バッファーからデータが読み取られ、処理します。 また、オーディオ処理オブジェクト (APOs) の形式のオーディオ エフェクトを読み込みます。 パスワードの詳細については、次を参照してください。 [Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)します。
3. APOs の待機時間は、信号、APOs 内で処理によって異なります。
4. Windows 10 では、前に、オーディオ エンジンの待機時間が ~ 浮動小数点データを使用するアプリケーション/、~ 六整数型のデータを使用するアプリケーションと一致しません
5. Windows 10 では、すべてのアプリケーションに対して 1.3ms に、待機時間が短縮されました

6. オーディオ エンジンは、処理されたデータをバッファーに書き込みます。
7. Windows 10 では、前にこのバッファーが常に ~ 10 ミリ秒に設定します。
8. Windows 10 以降では、バッファー サイズは、(この詳細についてはこのトピックの後半で説明) オーディオ ドライバーによって定義されます。

9. オーディオ ドライバー、バッファーからデータを読み取りおよび H または W に書き込む
10. H または W は、もう一度 (その他のオーディオ エフェクトの形式) でデータを処理するオプションもあります。
11. ユーザーには、スピーカーのオーディオが聞こえます。

キャプチャのパスでの待機時間の概要を次に示します。

1. マイクからオーディオがキャプチャされます。
2. H または W には、(つまりオーディオ エフェクトを追加) するデータを処理するオプションがあります。
3. ドライバーは、H または W からデータを読み取り、バッファーにデータを書き込みます。
4. Windows 10 では、前にこのバッファーが常に 10 ミリ秒に設定します。
5. Windows 10 以降では、バッファー サイズは、オーディオ ドライバー (詳細については後述) によって定義されます。

6. オーディオ エンジンは、バッファーからデータが読み取られ、その処理を行います。 また、オーディオ処理オブジェクト (APOs) の形式のオーディオ エフェクトを読み込みます。
7. APOs の待機時間は、信号、APOs 内で処理によって異なります。
8. Windows 10 では、前に、オーディオ エンジンの待機時間に等しかったため ~ 六浮動小数点を使用するアプリケーションがデータをポイントし、~ 0 の整数型のデータを使用するアプリケーション。
9. Windows 10 に、待機時間が短縮されましたが ~ 0 すべてのアプリケーション。

10. オーディオ エンジンは、その処理が完了するとすぐに読み取り可能なデータが、アプリケーションが通知されます。
    オーディオ スタックには、排他モードのオプションも提供します。 その場合は、データは、オーディオ エンジンをバイパスし、バッファーの場所から読み取り、ドライバーをアプリケーションから直接移動します。 ただし、アプリケーションがエンドポイントを排他モードで開いた場合はありませんをレンダリングしたり、そのエンドポイントが使用できるその他のアプリケーション オーディオ。

低待機時間を必要とするアプリケーションの別の一般的な方法では、排他モードを使用して ASIO (オーディオ Stream 入力/出力) モデルを使用します。 ユーザーは、サード パーティ ASIO ドライバーをインストールした後、アプリケーションは、ASIO ドライバーにアプリケーションから直接データを送信できます。 ただし、アプリケーションは、ASIO ドライバーに直接通信がこのような方法で記述します。

両方の代替手段 (排他モードおよび ASIO) では、独自の制限事項があります。 低待機時間、提供が、(上記の「その一部が) 制限があります。 その結果、オーディオ エンジンが変更された、柔軟性を維持しながら、待機時間を短くためにします。

## <a name="span-idaudiostackimprovementsinwindows10spanspan-idaudiostackimprovementsinwindows10spanspan-idaudiostackimprovementsinwindows10spanaudio-stack-improvements-in-windows-10"></a><span id="Audio_Stack_Improvements_in_Windows_10"></span><span id="audio_stack_improvements_in_windows_10"></span><span id="AUDIO_STACK_IMPROVEMENTS_IN_WINDOWS_10"></span>Windows 10 でのオーディオ スタックの機能強化


Windows 10 は、待機時間を短縮するために 3 つの領域で強化されています。

1. オーディオを使用するすべてのアプリケーションが表示されます 4.5 16 ミリ秒削減ラウンドト リップの待機時間で (上のセクションで説明した) ようコードの変更または Windows 8.1 と比較して、ドライバーの更新プログラムなし。
   a. データが 16 ミリ秒が浮動小数点を使用するアプリケーションでは、遅延時間が短縮します。
   b. 整数型のデータを使用するアプリケーションは、4.5ms 待機時間を減らす必要があります。
2. 更新されたドライバーとシステムながらラウンドト リップの待機時間は、: します。 ドライバーは、新しい Ddi を使用して、サポートされる OS および H または w. の間でデータを転送するために使用するバッファーのサイズを報告するには つまり、そのデータの転送を (以前の OS バージョンと)、10 ミリ秒のバッファーを常に使用する必要はありません。 代わりに、ドライバーでは、5、ミリ秒、1 ミリ秒などの b などの小さなバッファーを使用できるかどうかを指定できます。 低待機時間を必要とするアプリケーションは、(AudioGraph または WASAPI) の新しいオーディオ Api を使用して、ドライバーによってサポートされているバッファー サイズを照会および H/W. との間のデータ転送に使用される 1 つを選択するには
3. アプリケーションでは、特定のしきい値を下回るバッファー サイズを使用して、レンダリング、オーディオをキャプチャして、ときに、OS がオーディオのストリーミングとその他のサブシステム間の干渉を回避するように、そのリソースを管理、特殊なモードを入力します。 オーディオのサブシステムの実行の中断を削減され、オーディオの故障の確率を最小限に抑えます。 アプリケーションでは、ストリーミングが停止したら、OS を通常の実行モードを返します。 オーディオのサブシステムは、次のリソースで構成されます。 をします。 オーディオの低待機時間で処理されているオーディオ エンジン スレッドです。
   b. すべてのスレッドと割り込み (ドライバー リソースの登録に関するセクションで説明されている新しい Ddi を使用して)、ドライバーによって登録されています。
   c. 一部またはすべてのオーディオのスレッドだけでなく小さなバッファーを要求するすべてのアプリケーションと同じのオーディオ デバイス グラフ (例: 同じ信号処理モード) を共有するすべてのアプリケーションからの小さなバッファーを要求するアプリケーションから:
4. ストリーミングのパスに AudioGraph コールバック。
5. アプリケーションが WASAPI、しに送信された作業項目のみを使用している場合、[リアルタイムの作業キュー API](https://docs.microsoft.com/windows/desktop/ProcThread/platform-work-queue-api)または[ **MFCreateMFByteStreamOnStreamEx** ](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfcreatemfbytestreamonstreamex)としてタグ付けされたと"Audio"または"ProAudio"します。

## <a name="span-idapiimprovementsspanspan-idapiimprovementsspanspan-idapiimprovementsspanapi-improvements"></a><span id="API_Improvements"></span><span id="api_improvements"></span><span id="API_IMPROVEMENTS"></span>API の強化


次の 2 つの Windows 10 Api では、低待機時間機能を提供します。

-   [**AudioGraph**](https://docs.microsoft.com/uwp/api/Windows.Media.Audio.AudioGraph)
-   [Windows の音声セッション API (WASAPI)](https://docs.microsoft.com/windows/desktop/CoreAudio/wasapi)

これは、アプリケーション開発者が特定の 2 つの Api を使用する方法です。

-   新しいアプリケーションの開発可能な限り、AudioGraph が優先されます。
-   場合にのみ、WASAPI を使用します。
    -   AudioGraph で提供されるよりさらに制御する必要があります。
    -   AudioGraph によって提供されるより長い待機時間を軽減する必要があります。

[測定ツール](#measurement_tools)セクションのこのトピックでは、受信トレイの HDAudio ドライバーを使用して Haswell システムから特定のサイズを示しています。

次のセクションでは、各 API の低待機時間機能について説明します。 最小の待機時間を実現するために、システムのために、前のセクションで説明したように、バッファー サイズをサポートするドライバーが更新が必要です。

### <a name="span-idaudiographspanspan-idaudiographspanspan-idaudiographspanaudiograph"></a><span id="AudioGraph"></span><span id="audiograph"></span><span id="AUDIOGRAPH"></span>AudioGraph

AudioGraph は対象として対話型の実現と音楽作成シナリオを簡単に Windows 10 のユニバーサル Windows プラットフォームの新しい API です。 AudioGraph がいくつかのプログラミング言語で利用できます (C++ では、 C#、JavaScript) あり、シンプルかつ機能豊富なプログラミング モデル。

AudioGraph は、低待機時間シナリオを対象にするため、 [AudioGraphSettings::QuantumSizeSelectionMode プロパティ](https://docs.microsoft.com/uwp/api/Windows.Media.Audio.AudioGraphSettings#Windows_Media_Audio_AudioGraphSettings_QuantumSizeSelectionMode)します。 このプロパティでは、次の表に示すように、次の値のいずれかのことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>[値]</p></td>
<td align="left"><p>説明</p></td>
</tr>
<tr class="even">
<td align="left"><p>SystemDefault</p></td>
<td align="left"><p>既定のバッファー サイズ、バッファーの設定 (約 10 ミリ秒)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LowestLatency</p></td>
<td align="left"><p>ドライバーでサポートされている最小値に、バッファーを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ClosestToDesired</p></td>
<td align="left"><p>いずれかの等しい DesiredSamplesPerQuantum プロパティによって定義された値または DesiredSamplesPerQuantum ドライバーでサポートされている場合は、近くにある値のいずれかにバッファー サイズを設定します。</p></td>
</tr>
</tbody>
</table>

 

AudioCreation サンプル (GitHub からダウンロードできます: <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AudioCreation>) 待機時間が短く AudioGraph を使用する方法を示しています。 次のコード スニペットでは、最小バッファー サイズを設定する方法を示します。

```cpp
AudioGraphSettings settings = new AudioGraphSettings(AudioRenderCategory.Media);
settings.QuantumSizeSelectionMode = QuantumSizeSelectionMode.LowestLatency;
CreateAudioGraphResult result = await AudioGraph.CreateAsync(settings);
```

### <a name="span-idwindowsaudiosessionapiwasapispanspan-idwindowsaudiosessionapiwasapispanspan-idwindowsaudiosessionapiwasapispanwindows-audio-session-api-wasapi"></a><span id="Windows_Audio_Session_API_WASAPI"></span><span id="windows_audio_session_api_wasapi"></span><span id="WINDOWS_AUDIO_SESSION_API_WASAPI"></span>Windows の音声セッション API (WASAPI)

Windows 10 以降、WASAPI に強化されています。

-   特定のオーディオ デバイスのオーディオ ドライバーでサポートされているバッファー サイズ (つまり、周期性値) の範囲を検出するアプリケーションを許可します。 アプリケーションが既定のバッファー サイズを選択するためにできるようになります (10 ミリ秒) または小さなバッファー (&lt;10 ミリ秒) 共有モードでストリームを開くときにします。 アプリケーションでは、バッファー サイズを指定しない場合、既定のバッファー サイズが使用されます。
-   現在の形式とオーディオ エンジンの周期性を検出するアプリケーションを許可します。 これにより、アプリケーション、オーディオ エンジンの現在の設定へのスナップです。
-   アプリをすべて再サンプリング オーディオ エンジンによってなしを指定の形式でレンダリング/キャプチャする必要があることを指定できます。

上記の機能は、すべての Windows デバイスで利用可能になります。 ただし、十分なリソースと更新されたドライバーの特定のデバイスでは、他よりも優れたユーザー エクスペリエンスが提供されます。

上記の機能と呼ばれる、新しいインターフェイスによって提供されます[ **IAudioClient3**](https://docs.microsoft.com/windows/desktop/api/audioclient/nn-audioclient-iaudioclient3)から派生した[ **IAudioClient2**](https://docs.microsoft.com/windows/desktop/api/audioclient/nn-audioclient-iaudioclient2)します。

[**IAudioClient3** ](https://docs.microsoft.com/windows/desktop/api/audioclient/nn-audioclient-iaudioclient3)次の 3 つの方法を定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>メソッド</p></td>
<td align="left"><p>説明</p></td>
</tr>
<tr class="even">
<td align="left"><p>GetCurrentSharedModeEnginePeriod</p></td>
<td align="left"><p>現在の形式とオーディオ エンジンの周期性を返します</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GetSharedModeEnginePeriod</p></td>
<td align="left"><p>指定したストリーム形式のエンジンでサポートされている周期性の範囲を返します</p></td>
</tr>
<tr class="even">
<td align="left"><p>InitializeSharedAudioStream</p></td>
<td align="left"><p>指定された間隔で共有のストリームを初期化します。</p></td>
</tr>
</tbody>
</table>

 

WASAPIAudio サンプル (GitHub で入手できます: <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WindowsAudioSession>) 待機時間が短く IAudioClient3 を使用する方法を示しています。

次のコード スニペットでは、音楽の作成のアプリは、システムでサポートされている最下位の待機時間の設定で動作する方法を示します。

```cpp
// 1. Activation

// Get a string representing the Default Audio (Render|Capture) Device
m_DeviceIdString = MediaDevice::GetDefaultAudio(Render|Capture)Id( 
Windows::Media::Devices::AudioDeviceRole::Default );

// This call must be made on the main UI thread.  Async operation will call back to 
// IActivateAudioInterfaceCompletionHandler::ActivateCompleted, which must be an agile // interface implementation
hr = ActivateAudioInterfaceAsync( m_DeviceIdString->Data(), __uuidof(IAudioClient3), 
nullptr, this, &asyncOp );

// 2. Setting the audio client properties – note that low latency offload is not supported

AudioClientProperties audioProps = {0};
audioProps.cbSize = sizeof( AudioClientProperties );
audioProps.eCategory = AudioCategory_Media;

// if the device has System.Devices.AudioDevice.RawProcessingSupported set to true and you want to use raw mode
// audioProps.Options |= AUDCLNT_STREAMOPTIONS_RAW;
//
// if it is important to avoid resampling in the audio engine, set this flag
// audioProps.Options |= AUDCLNT_STREAMOPTIONS_MATCH_FORMAT;


hr = m_AudioClient->SetClientProperties( &audioProps ); if (FAILED(hr)) { ... }

// 3. Querying the legal periods

hr = m_AudioClient->GetMixFormat( &mixFormat ); if (FAILED(hr)) { ... }

hr = m_AudioClient->GetSharedModeEnginePeriod(wfx, &defaultPeriodInFrames, &fundamentalPeriodInFrames, &minPeriodInFrames, &maxPeriodInFrames); if (FAILED(hr)) { ... }

// legal periods are any multiple of fundamentalPeriodInFrames between 
// minPeriodInFrames and maxPeriodInFrames, inclusive
// the Windows shared-mode engine uses defaultPeriodInFrames unless an audio client // has specifically requested otherwise

// 4. Initializing a low-latency client

hr = m_AudioClient->InitializeSharedAudioStream(
         AUDCLNT_STREAMFLAGS_EVENTCALLBACK,
         desiredPeriodInFrames,
         mixFormat,
         nullptr); // audio session GUID
         if (AUDCLNT_E_ENGINE_PERIODICITY_LOCKED == hr) {
         /* engine is already running at a different period; call m_AudioClient->GetSharedModeEnginePeriod to see what it is */
         } else if (FAILED(hr)) {
             ...
         }

// 5. Initializing a client with a specific format (if the format needs to be different than the default format)

AudioClientProperties audioProps = {0};
audioProps.cbSize = sizeof( AudioClientProperties );
audioProps.eCategory = AudioCategory_Media;
audioProps.Options |= AUDCLNT_STREAMOPTIONS_MATCH_FORMAT;

hr = m_AudioClient->SetClientProperties( &audioProps ); 
if (FAILED(hr)) { ... }

hr = m_AudioClient->IsFormatSupported(AUDCLNT_SHAREMODE_SHARED, appFormat, &closest);
if (S_OK == hr) {
       /* device supports the app format */
} else if (S_FALSE == hr) {
       /* device DOES NOT support the app format; closest supported format is in the "closest" output variable */
} else {
       /* device DOES NOT support the app format, and Windows could not find a close supported format */
}

hr = m_AudioClient->InitializeSharedAudioStream(
       AUDCLNT_STREAMFLAGS_EVENTCALLBACK,
       defaultPeriodInFrames,
       appFormat,
       nullptr); // audio session GUID
if (AUDCLNT_E_ENGINE_FORMAT_LOCKED == hr) {
       /* engine is already running at a different format */
} else if (FAILED(hr)) {
       ...
}
```

WASAPI を使用しても使用するアプリケーションの推奨されるさらに、[リアルタイムの作業キュー API](https://docs.microsoft.com/windows/desktop/ProcThread/platform-work-queue-api)または[ **MFCreateMFByteStreamOnStreamEx** ](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfcreatemfbytestreamonstreamex)作業項目を作成し、独自のスレッドではなくオーディオまたはオーディオ Pro としてタグします。 これは、ようにするには干渉オーディオ以外のサブシステムを回避する方法を管理します。 これに対し、AudioGraph のすべてのスレッドは自動的に適切に管理 OS によって。 WASAPIAudio サンプルから次のコード スニペットでは、MF 作業キュー Api を使用する方法を示します。

```cpp
// Specify Source Reader Attributes 
Attributes->SetUnknown( MF_SOURCE_READER_ASYNC_CALLBACK, static_cast<IMFSourceReaderCallback *>(this) ); 
    if (FAILED( hr )) 
    { 
        goto exit; 
    } 
    Attributes->SetString( MF_READWRITE_MMCSS_CLASS_AUDIO, L"Audio" ); 
    if (FAILED( hr )) 
    { 
        goto exit; 
    } 
    Attributes->SetUINT32( MF_READWRITE_MMCSS_PRIORITY_AUDIO, 0 ); 
    if (FAILED( hr )) 
    { 
        goto exit; 
    } 
    // Create a stream from IRandomAccessStream 
    hr = MFCreateMFByteStreamOnStreamEx (reinterpret_cast<IUnknown*>(m_ContentStream), &ByteStream ); 
    if ( FAILED( hr ) ) 
    { 
        goto exit; 
    } 
    // Create source reader 
    hr = MFCreateSourceReaderFromByteStream( ByteStream, Attributes, &m_MFSourceReader );
```

または、次のコード スニペットは、RT 作業キュー Api を使用する方法を示します。

```cpp
#define INVALID_WORK_QUEUE_ID 0xffffffff
DWORD g_WorkQueueId = INVALID_WORK_QUEUE_ID;
//#define MMCSS_AUDIO_CLASS    L"Audio"
//#define MMCSS_PROAUDIO_CLASS L"ProAudio"

STDMETHODIMP TestClass::GetParameters(DWORD* pdwFlags, DWORD* pdwQueue)
{
       HRESULT hr = S_OK;
       *pdwFlags = 0;
       *pdwQueue = g_WorkQueueId;
       return hr;
}

//-------------------------------------------------------
STDMETHODIMP TestClass::Invoke(IRtwqAsyncResult* pAsyncResult)
{
       HRESULT hr = S_OK;
       IUnknown *pState = NULL;
       WCHAR className[20];
       DWORD  bufferLength = 20;
       DWORD taskID = 0;
       LONG priority = 0;

       printf("Callback is invoked pAsyncResult(0x%0x)  Current process id :0x%0x Current thread id :0x%0x\n", (INT64)pAsyncResult, GetCurrentProcessId(), GetCurrentThreadId());

       hr = RtwqGetWorkQueueMMCSSClass(g_WorkQueueId, className, &bufferLength);
       IF_FAIL_EXIT(hr, Exit);

       if (className[0])
       {
              hr = RtwqGetWorkQueueMMCSSTaskId(g_WorkQueueId, &taskID);
              IF_FAIL_EXIT(hr, Exit);

              hr = RtwqGetWorkQueueMMCSSPriority(g_WorkQueueId, &priority);
              IF_FAIL_EXIT(hr, Exit);
              printf("MMCSS: [%ws] taskID (%d) priority(%d)\n", className, taskID, priority);
       }
       else
       {
              printf("non-MMCSS\n");
       }
       hr = pAsyncResult->GetState(&pState);
       IF_FAIL_EXIT(hr, Exit);

Exit:
       return S_OK;
}
//-------------------------------------------------------

int _tmain(int argc, _TCHAR* argv[])
{
       HRESULT hr = S_OK;
       HANDLE signalEvent;
       LONG Priority = 1;
       IRtwqAsyncResult *pAsyncResult = NULL;
       RTWQWORKITEM_KEY workItemKey = NULL;;
       IRtwqAsyncCallback *callback = NULL;
       IUnknown *appObject = NULL;
       IUnknown *appState = NULL;
       DWORD taskId = 0;
       TestClass cbClass;
       NTSTATUS status;

       hr = RtwqStartup();
       IF_FAIL_EXIT(hr, Exit);

       signalEvent = CreateEvent(NULL, true, FALSE, NULL);
       IF_TRUE_ACTION_EXIT(signalEvent == NULL, hr = E_OUTOFMEMORY, Exit);

       g_WorkQueueId = RTWQ_MULTITHREADED_WORKQUEUE;

       hr = RtwqLockSharedWorkQueue(L"Audio", 0, &taskId, &g_WorkQueueId);
       IF_FAIL_EXIT(hr, Exit);

       hr = RtwqCreateAsyncResult(NULL, reinterpret_cast<IRtwqAsyncCallback*>(&cbClass), NULL, &pAsyncResult);
       IF_FAIL_EXIT(hr, Exit);

       hr = RtwqPutWaitingWorkItem(signalEvent, Priority, pAsyncResult, &workItemKey);
       IF_FAIL_EXIT(hr, Exit);

       for (int i = 0; i < 5; i++)
       {
              SetEvent(signalEvent);
              Sleep(30);
              hr = RtwqPutWaitingWorkItem(signalEvent, Priority, pAsyncResult, &workItemKey);
              IF_FAIL_EXIT(hr, Exit);
    }

Exit:
       if (pAsyncResult)
       {
              pAsyncResult->Release();
       }

      if (INVALID_WORK_QUEUE_ID != g_WorkQueueId)
      {
        hr = RtwqUnlockWorkQueue(g_WorkQueueId);
        if (FAILED(hr))
        {
            printf("Failed with RtwqUnlockWorkQueue 0x%x\n", hr);
        }

        hr = RtwqShutdown();
        if (FAILED(hr))
        {
            printf("Failed with RtwqShutdown 0x%x\n", hr);
        }
      }

       if (FAILED(hr))
       {
          printf("Failed with error code 0x%x\n", hr);
       }
       return 0;
}
```

最後に、WASAPI しなければタグを使用して、アプリケーション開発者のストリームとオーディオのカテゴリと処理モードでは、生の信号を使用するかどうかに基づいて各ストリームの機能です。 影響を理解しない限り、すべてのオーディオ ストリームが、生のシグナル処理モードを使用しないことをお勧めします。 Raw モードをバイパスする処理を信号が、OEM によって選択されているすべてため。

-   特定のエンドポイントにレンダー信号を最適可能性があります。
-   キャプチャ シグナルは、アプリケーションを理解することはできませんの形式では可能性があります。
-   待機時間を向上する可能性があります。

## <a name="span-iddriverimprovementsspanspan-iddriverimprovementsspanspan-iddriverimprovementsspandriver-improvements"></a><span id="Driver_Improvements"></span><span id="driver_improvements"></span><span id="DRIVER_IMPROVEMENTS"></span>ドライバの改善


低待機時間をサポートするために、オーディオ ドライバーの順番は、Windows 10 は、次の 3 つの新機能を提供します。

1. \[必須\]各モードでサポートされている最小バッファー サイズを宣言します。
2. \[省略可、ただし推奨\]ドライバーと OS の間のデータ フローの連携を強化します。
3. \[省略可、ただし推奨\]ドライバー リソース (割り込み、スレッド) を登録し、低待機時間シナリオでの OS で保護するようにします。
受信トレイ HDAudio バス ドライバー hdaudbus.sys によって列挙される HDAudio ミニポート関数ドライバーは、hdaudbus.sys によってこれは、既にとして HDAudio 割り込みを登録する必要はありません。 ただし、ミニポート ドライバーでは、独自のスレッドを作成する場合、その必要がありますに登録します。

次の 3 つのセクションには、各新機能についてより詳しくは説明します。

**1.最小バッファー サイズを宣言します。**

ドライバーは、オペレーティング システム、ドライバーとハードウェアの間にオーディオ データを移動するときに、さまざまな制約の下で動作します。 メモリと、ハードウェアの間でデータを移動する物理的なハードウェアのトランスポートのためや、ハードウェアまたは関連付けられている DSP にあるモジュールを処理するシグナルにより、これらの制約があります。

Windows 10 では、ドライバーが、DEVPKEY を使用して、バッファー サイズの機能を表すことが\_KsAudio\_PacketSize\_制約デバイス プロパティ。 このプロパティにより、ユーザーが、ドライバー、および処理モード (モード固有の制約をドライバーの最小バッファー サイズよりも高くする必要がある各シグナルの特定のバッファー サイズの制約によってサポートされている絶対最小バッファー サイズを定義するには、それ以外の場合は、オーディオ スタックによって無視されます)。 たとえば、次のコード スニペットは、ドライバーが絶対最小のサポートされているバッファー サイズが 1 ミリ秒が既定のモードは、(に対応する 3 ミリ秒、48 kHz サンプル速度を仮定した場合) 128 のフレームをサポートしていることを宣言する方法を示します。

```cpp
// Describe constraints for small buffers
static struct
{
    KSAUDIO_PACKETSIZE_CONSTRAINTS TransportPacketConstraints;
    KSAUDIO_PACKETSIZE_PROCESSINGMODE_CONSTRAINT AdditionalProcessingConstraints[1];
} SysvadWaveRtPacketSizeConstraintsRender =
{
    {
        1 * HNSTIME_PER_MILLISECOND,                // 1 ms minimum processing interval
        FILE_256_BYTE_ALIGNMENT,                    // 256 byte packet size alignment
        0,                                          // reserved
        1,                                          // 1 processing constraint below
        {
            STATIC_AUDIO_SIGNALPROCESSINGMODE_DEFAULT,          // constraint for default processing mode
            128,                                  // 128 samples per processing frame
            0,                                    // N/A hns per processing frame    
       },
    },
};
```

これらの構造に関する詳細については、次のトピックを参照してください。

-   [**KSAUDIO\_PACKETSIZE\_制約構造体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)
-   [**KSAUDIO\_PACKETSIZE\_PROCESSINGMODE\_制約構造体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)

Sysvad サンプルではまた、(<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>) 各モードの最小バッファーを宣言するためのドライバーの順序でこれらのプロパティを使用する方法を示しています。

**2.ドライバーと OS 間の調整を改善します。**

このセクションに記載されている Ddi では、ドライバーを許可します。

-   どちらの半分を明確に示す (パケット) バッファーは、OS に使用可能なコーデックに基づいて推測 OS 位置のリンクではなく。 これにより、高速オーディオ問題から復旧する OS です。
-   必要に応じて最適化または WaveRT バッファーとの間のデータ転送を簡略化します。 ここでの特典の量は、DMA エンジン設計または WaveRT バッファーと (場合によっては DSP) の間の他のデータ転送機構によって異なります。 ハードウェア。
-   ドライバーが内部的にキャプチャされたデータを蓄積された場合は、リアルタイムのよりも高速データをキャプチャする「バースト」。 これにより、音声のライセンス認証のシナリオの主な対象しますが、通常ストリーミングも中に適用できます。
-   推測、非常に正確な位置情報の可能性があることができます、OS ではなく、その現在のストリームの位置に関するタイムスタンプ情報を提供します。

この DDI は、DSP が使用されている場合は、非常に便利です。 ただし、標準の HD オーディオ ドライバーやその他の単純な循環 DMA バッファー デザイン可能性がありますが見つかりませんこれら新しい Ddi でメリットがここに表示します。

-   [IMiniportWaveRTInputStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertinputstream)
-   [IMiniportWaveRTOutputStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertoutputstream)

ドライバーのルーチンのいくつかは、Windows パフォーマンス カウンターのタイムスタンプをサンプルのキャプチャまたはデバイスによって提示される時間を反映したを返します。

複雑な DSP がデバイスで困難な場合がありますパイプラインと信号処理では、正確なタイムスタンプを計算して、慎重に行う必要があります。 単に、タイムスタンプでは、サンプル転送された OS との間、DSP に時間を反映する必要がありますされません。

パフォーマンス カウンターの値を計算するには、ドライバーと DSP 可能性がありますを使用して、次のメソッドの一部です。

-   DSP、内では、いくつかの内部の DSP ウォール クロックを使用してサンプルのタイムスタンプを追跡します。
-   ドライバーと DSP、間には、Windows パフォーマンス カウンターと DSP ウォール クロックの間の相関関係を計算します。 この手順のことができます (ただし、精度の低い) 非常に単純なものから非常に複雑なより正確な (ただし奇抜に範囲です。
-   これらの遅延は、それ以外の場合の計上しない限り、信号処理のアルゴリズムまたはパイプライン、またはハードウェアのトランスポートのための定数の遅延を考慮します。

Sysvad サンプル (<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>) 上記の Ddi を使用する方法を示しています。

**3.ドライバー リソースを登録します。**

故障のない動作を保証するために、オーディオ ドライバーは portcls をストリーミングのリソースを登録する必要があります。 これにより、OS をオーディオ ストリーミングとその他の subystems 間の干渉を避けるためにリソースを管理できます。

Stream のリソースとは、オーディオ ストリームを処理するか、またはオーディオ データの流れを確実に、オーディオ ドライバーによって使用されているリソースです。 現時点では、ストリーム リソースの 2 つの種類がサポートされています。 割り込みとドライバーが所有しているスレッド。 オーディオ ドライバーが、リソースの作成後にリソースを登録し、リソースの登録を解除する必要がありますそれを削除する前にします。

オーディオ ドライバー、ドライバーが読み込まれるときに、初期化時、または I/O リソースの再調整がある場合の例については、実行時に、リソースを登録できます。 Portcls では、グローバル状態を使用して、すべてのオーディオのストリーミングのリソースを追跡します。

一部のユース ケース、非常に低待機時間のオーディオを必要とするものなど、OS 他の OS、アプリケーション、およびハードウェアのアクティビティからの干渉から、オーディオ ドライバーの登録済みのリソースを分離しようとしました。 OS とオーディオのサブシステムは、オーディオ ドライバー、オーディオ ドライバーの登録のリソースを除くと対話することがなくこのに応じてを実行します。

ストリームのリソースを登録するには、この要件は、すべてストリーミング パイプライン パス内にある必要がありますを登録すること、リソース直接的または間接的に Portcls でを意味します。 オーディオのミニポート ドライバーでは、これらのオプションがあります。

-   オーディオのミニポート ドライバーは、スタック (インターフェイシングは h または w 直接)、この場合の下部にあるドライバー、ドライバーがそのストリームのリソースを認識および Portcls に登録できます。
-   オーディオのミニポート ドライバーは、他のドライバー (例オーディオ バス ドライバー) を利用してストリーミングは。 これらの他のドライバーでは、リソース Portcls に登録する必要がありますも使用します。 これらの並列/バス ドライバー スタックがパブリックに公開できます (または 1 つのベンダーは、すべてのドライバーを所有している場合、プライベート インターフェイス) オーディオ ミニポート ドライバーを使用してこの情報を収集することです。
-   オーディオのミニポート ドライバーは、その他のドライバー (例 hdaudbus) のヘルプでストリーミングが。 これらの他のドライバーでは、リソース Portcls に登録する必要がありますも使用します。 これらの並列/バスのドライバー Portcls とリンクし、リソースを直接登録できます。 オーディオのミニポート ドライバーが知る他の並列/bus デバイス (Pdo) はこれらのリソースに依存する Portcls をさせる必要がありますに注意してください。 Hd オーディオ インフラストラクチャを使用してこのオプションは、つまり hd オーディオ-バス ドライバー Portcls とリンクに自動的には、次の手順を実行します。
    -   バス ドライバーのリソースを登録し、
    -   親のリソースに依存している子供のリソースを Portcls に通知します。 HD オーディオ アーキテクチャでは、オーディオのミニポート ドライバーは、独自のドライバーが所有しているスレッド リソースを登録するだけが必要です。

注:

-   受信トレイ HDAudio バス ドライバー hdaudbus.sys によって列挙される HDAudio ミニポート関数ドライバーは、hdaudbus.sys によってこれは、既にとして HDAudio 割り込みを登録する必要はありません。 ただし、ミニポート ドライバーでは、独自のスレッドを作成する場合、その必要がありますに登録します。
-   ドライバー Portcls とストリーミングのリソースを登録するためだけのリンクを wdmaudio.inf とコピー portcls.sys (および依存ファイル) の含める/ニーズに合わせて、Inf を更新する必要があります。 新しい INF コピー セクションは、のみそれらのファイルをコピーする wdmaudio.inf で定義されます。
-   Windows 10 でのみ実行されるオーディオ ドライバーへのハード リンクことができます。
    -   [**PcAddStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcaddstreamresource)
    -   [**PcRemoveStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcremovestreamresource)
-   ダウンレベルの OS で実行する必要がありますオーディオ ドライバーは、次のインターフェイスを使用できます (IID の QueryInterface を呼び出すことができます、ミニポート\_IPortClsStreamResourceManager インターフェイスし、PortCls インターフェイスをサポートする場合にのみ、リソースの登録)。
    -   [IPortClsStreamResourceManager](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsstreamresourcemanager)
        -   [**AddStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportclsstreamresourcemanager-addstreamresource)
        -   [**RemoveStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportclsstreamresourcemanager-removestreamresource)
-   これらの Ddi は、この列挙体と構造体を使用します。
    -   [**PcStreamResourceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ne-portcls-_pcstreamresourcetype)
    -   [**PCSTREAMRESOURCE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-_pcstreamresource_descriptor)

最後に、ドライバーをリンク PortCls 用のリソースを登録するための唯一の目的は、inf の DDInstall セクションで次の 2 つの行を追加する必要があります。 オーディオのミニポート ドライバー不要この wdmaudio.inf で含める/ニーズが既にあるためです。

```inf
[<install-section-name>]
Include=wdmaudio.inf
Needs=WDMPORTCLS.CopyFilesOnly
```

上記の行を確認する PortCls とその依存ファイルがインストールされています。

## <a name="span-idmeasurementtoolsspanspan-idmeasurementtoolsspanspan-idmeasurementtoolsspanmeasurement-tools"></a><span id="Measurement_Tools"></span><span id="measurement_tools"></span><span id="MEASUREMENT_TOOLS"></span>評価ツール


ラウンド トリップの待機時間を測定するためには、ユーザーはユーザーは、スピーカーを使用してパルスを再生し、マイクを使用してそれらをキャプチャするツールを利用します。 次のパスの遅延を測定します。

1. アプリケーションが (AudioGraph または WASAPI) パルスを再生する render API を呼び出す
2. スピーカーを使用して、オーディオが再生されます。
3. マイクからオーディオをキャプチャします。
4. パルスが検出されました (AudioGraph または WASAPI) キャプチャ API によって別のバッファー サイズは、ラウンドト リップの待機時間を測定するためにユーザーが小さなバッファーをサポートしているドライバーをインストールする必要があります。 128 のサンプル間のバッファー サイズをサポートする受信トレイ HDAudio ドライバーが更新されました (2.66ms@48kHz) と 480 サンプル (10ms@48kHz)。 次の手順では、受信トレイ HDAudio ドライバー (これは Windows 10 のすべての Sku の一部) をインストールする方法を示します。

-   デバイス マネージャーを起動します。
-   **ビデオ、およびゲーム コント ローラーのサウンド**、内部スピーカーに対応するデバイスをダブルクリックします。
-   次のウィンドウに移動、**ドライバー**タブ。
-   選択**ドライバーの更新** - &gt; **参照コンピューターでドライバー ソフトウェア** - &gt; **内のデバイス ドライバーの一覧から選択このコンピューター**  - &gt; **高定義の [オーディオ デバイス**] をクリック**次**。
-   「ドライバー警告の更新」というタイトルのウィンドウが表示されたら、クリックして**はい**します。
-   選択**閉じます**します。
-   システムの再起動を求められたら場合、選択**はい**を再起動します。
-   再起動後は、受信トレイの Microsoft HDAudio ドライバーおよびサード パーティ製コーデック ドライバーではなく、システムが使用されます。 オーディオ コーデックの最適な設定を使用する場合、ドライバーへのフォールバックを行えるようにする前に、使用していたドライバーに注意してください。

![wasapi とさまざまなバッファー サイズと audiograph では、ラウンドト リップの待機時間の違いを示すグラフ。 ](images/low-latency-audio-roundtrip-latency.png)

WASAPI と AudioGraph では、待機時間の違いは、次の理由は。

-   AudioGraph 同期レンダリングし (WASAPI によって提供されていない) をキャプチャするために、キャプチャ側での待機時間の 1 つのバッファーに追加します。 この追加は、AudioGraph を使用して記述されたアプリケーションのコードを簡略化します。
-   システムを使用する場合は、追加のバッファー AudioGraph のレンダリングの側での待機時間の&gt;六バッファー。
-   AudioGraph には、オーディオ効果のキャプチャを無効にするオプションはありません。

## <a name="span-idsamplesspanspan-idsamplesspanspan-idsamplesspansamples"></a><span id="Samples"></span><span id="samples"></span><span id="SAMPLES"></span>サンプル


-   WASAPI オーディオ サンプル: <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WindowsAudioSession>
-   AudioCreation サンプル (AudioGraph): <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AudioCreation>
-   Sysvad ドライバーのサンプル: <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

## <a name="span-idfaqspanspan-idfaqspanfaq"></a><span id="FAQ"></span><span id="faq"></span>FAQ


**1.ほう、すべてのアプリケーションは、低待機時間の新しい Api を使用する場合ですか。低待機時間は常に、ユーザーのユーザー エクスペリエンスを改善を保証しますか。**

必須ではありません。 低待機時間では、そのトレードオフがあります。

-   低待機時間は、消費電力を意味します。 システムは、10 ミリ秒のバッファーを使用している場合、CPU がウェイク アップすべて 10 ミリ秒、データ バッファーをスリープ状態になります。 ただし、システムが 1 ミリ秒を使用している場合、バッファー、CPU がウェイク アップすべて 1 ミリ秒いることを意味します。 2 番目のシナリオでは、つまり、CPU がより多くの場合、ウェイク、電力消費量が増加します。 これにより、バッテリの残量が低下します。
-   ほとんどのアプリケーションでは、最適なユーザー エクスペリエンスを提供するオーディオ エフェクトを使用します。 たとえば、メディア プレーヤーは高品質な音声を提供するとします。 通信のアプリケーションは、最小のエコーをノイズします。 ストリームにこれらの種類のオーディオ エフェクトを追加すると、その待機時間が増加します。 これらのアプリケーションは、オーディオの待機時間よりも音質に強い関心です。

要約すると、各アプリケーションの種類は、オーディオの待機時間に関するさまざまなニーズがあります。 アプリケーションに低待機時間が必要がない場合使用しないでください、新しい Api の低待機時間。

**2.Windows 10 に更新するすべてのシステムが自動的に更新されます小さなバッファーをサポートするでしょうか。すべてのシステムはまたは同じ最小バッファー サイズをサポートしますか。**

No. 小さなバッファーをサポートするために、システムのためには、ドライバーが更新が必要があります。 小さなバッファーをサポートするためにどのシステムが更新されますかを決定する Oem の責任です。 また、新しいシステムは (つまり、待機時間を新しいシステムで多くの場合よりも低くなります古いシステム) 以前のバージョンのシステムよりも小さなバッファーをサポートする可能性が高くなります。

**3.ドライバーは、小規模バッファー サイズをサポートしている場合 (&lt;10 ミリ秒のバッファー) では Windows 10 のすべてのアプリケーションに自動的を使用して、小さなバッファーをレンダリングし、音声をキャプチャするでしょうか。**

No. 既定では、Windows 10 のすべてのアプリケーションは、レンダリング、オーディオをキャプチャする、10 ミリ秒のバッファーを使用します。 小さなバッファーを使用する場合、アプリケーションは、新しい AudioGraph 設定または WASAPI IAudioClient3 インターフェイスを使用して、そのために、必要があります。 ただし、Windows 10 での 1 つのアプリケーションでは、小さなバッファーの使用を要求している場合、オーディオ エンジンは開始その特定のバッファー サイズを使用してオーディオを転送します。 その場合は、同じエンドポイントとモードを使用するすべてのアプリケーションに自動的にその小さなバッファー サイズに切り替わります。 低待機時間のアプリケーションが終了すると、オーディオ エンジンがもう一度 10 ミリ秒のバッファーに切り替えます。

 

 




