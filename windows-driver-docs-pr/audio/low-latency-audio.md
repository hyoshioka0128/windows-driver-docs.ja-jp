---
title: 低待機時間オーディオ
description: このトピックでは、Windows 10 でのオーディオの待機時間の変化について説明します。 アプリケーション開発者向けの API オプションに加え、低待機時間のオーディオをサポートするために実行できるドライバーの変更についても説明します。
ms.assetid: 888AEF01-271D-41CD-8372-A47551348959
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfe4dc6f31faa90789e9718bbec65b2f3911bf32
ms.sourcegitcommit: 57b649e59a2be2055413982035d89bc85e3e425d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2020
ms.locfileid: "85133286"
---
# <a name="low-latency-audio"></a>低待機時間オーディオ

このトピックでは、Windows 10 でのオーディオの待機時間の変化について説明します。 アプリケーション開発者向けの API オプションに加え、低待機時間のオーディオをサポートするために実行できるドライバーの変更についても説明します。

このトピックは、次のセクションで構成されています。

- [概要](#overview)
- [定義](#definitions)
- [Windows オーディオスタック](#windows_audio_stack)
- [Windows 10 でのオーディオスタックの強化](#audio_stack_improvements_in_windows_10)
- [API の機能強化](#api_improvements)
- [AudioGraph](#audiograph)
- [Windows Audio Session API (中 API)](#windows_audio_session_api_wasapi)
- [ドライバーの機能強化](#driver_improvements)
- [測定ツール](#measurement_tools)
- [サンプル](#samples)
- [FAQ](#faq)

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要

オーディオ待機時間とは、サウンドが作成されてから聞こえたときまでの遅延です。 次のようないくつかの主要なシナリオでは、オーディオの待機時間を短くすることが非常に重要です。

- Pro オーディオ
- 音楽の作成
- 通信
- 仮想現実
- ゲーム

Windows 10 には、オーディオの待機時間を短縮するための変更が含まれています。 このドキュメントの目的は次のとおりです。

1. Windows でのオーディオ待機時間の原因について説明します。
2. Windows 10 オーディオスタックでのオーディオの待機時間を短縮する変更について説明します。
3. アプリケーション開発者とハードウェアメーカーが新しいインフラストラクチャを活用し、オーディオの待機時間が短いアプリケーションやドライバーを開発するための参考資料を提供します。 このトピックでは、次の項目について説明します。
4. 対話型およびメディア作成シナリオ用の新しい[**Audiograph**](https://docs.microsoft.com/uwp/api/Windows.Media.Audio.AudioGraph) API。
5. 低待機時間をサポートするために、変更が発生しています。
6. ドライバー DDIs の機能強化。

## <a name="span-iddefinitionsspanspan-iddefinitionsspanspan-iddefinitionsspandefinitions"></a><span id="Definitions"></span><span id="definitions"></span><span id="DEFINITIONS"></span>定義

|||
|--- |--- |
|用語|説明|
|レンダー待機時間|アプリケーションが音声データのバッファーをレンダー Api に送信するまでの遅延時間。この時間が、スピーカーから聞こえるようになります。|
|キャプチャの待機時間|サウンドがマイクからキャプチャされてから、アプリケーションによって使用されているキャプチャ Api に送信されるまでの遅延時間。|
|ラウンドトリップの待機時間|マイクからサウンドがキャプチャされてから、アプリケーションによって処理され、スピーカーにレンダリングするためにアプリケーションによって送信されるまでの遅延。 これは、レンダリングの待機時間 + キャプチャの待機時間とほぼ同じです。|
|タッチツーアプリの待機時間|通知がアプリケーションに送信されるまでにユーザーが画面をタップするまでの遅延時間。|
|タッチツーサウンド待機時間|ユーザーが画面をタップするまでの待ち時間。イベントはアプリケーションに送信され、スピーカーを介してサウンドが聞こえます。 これは、レンダリングの待機時間とタッチツーアプリの待機時間と同じです。|

## <a name="span-idwindows_audio_stackspanspan-idwindows_audio_stackspanspan-idwindows_audio_stackspanwindows-audio-stack"></a><span id="Windows_Audio_Stack"></span><span id="windows_audio_stack"></span><span id="WINDOWS_AUDIO_STACK"></span>Windows オーディオスタック

次の図は、Windows オーディオスタックの簡略化されたバージョンを示しています。

![アプリ、オーディオエンジンドライバー、および h/w を示す低待機時間オーディオスタック図](images/low-latency-audio-stack-diagram-1.png)

レンダリングパスの待機時間の概要を次に示します。

1. アプリケーションがデータをバッファーに書き込みます。
2. オーディオエンジンは、バッファーからデータを読み取り、処理します。 また、オーディオ処理オブジェクト (APOs) の形式でオーディオ効果を読み込みます。 APOs の詳細については、「 [Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)」を参照してください。
3. Apos の待機時間は、APOs 内の信号処理によって異なります。
4. Windows 10 より前の場合、オーディオエンジンの待機時間は、浮動小数点データを使用するアプリケーションでは約12ミリ秒、整数データを使用するアプリケーションでは ~ 6ms になりました。
5. Windows 10 では、すべてのアプリケーションで待機時間が1.3 ミリ秒に短縮されました。

6. オーディオエンジンは、処理されたデータをバッファーに書き込みます。
7. Windows 10 より前の場合、このバッファーは常に ~ 10 ミリ秒に設定されていました。
8. Windows 10 以降では、オーディオドライバーによってバッファーサイズが定義されます (詳細については、このトピックの後半で説明します)。

9. オーディオドライバーは、バッファーからデータを読み取り、H/W に書き込みます。
10. H/W には、(追加のオーディオ効果の形式で) データを再度処理するオプションもあります。
11. ユーザーはスピーカーからオーディオを聞くことができます。

キャプチャパスの待機時間の概要を次に示します。

1. オーディオはマイクからキャプチャされます。
2. H/W には、データを処理する (つまり、オーディオ効果を追加する) オプションがあります。
3. ドライバーは、H/W からデータを読み取り、データをバッファーに書き込みます。
4. Windows 10 より前の場合、このバッファーは常に10ミリ秒に設定されていました。
5. Windows 10 以降では、オーディオドライバーによってバッファーサイズが定義されます (詳細については、以下を参照してください)。

6. オーディオエンジンは、バッファーからデータを読み取り、処理します。 また、オーディオ処理オブジェクト (APOs) の形式でオーディオ効果を読み込みます。
7. Apos の待機時間は、APOs 内の信号処理によって異なります。
8. Windows 10 より前の場合、オーディオエンジンの待機時間は、浮動小数点データを使用するアプリケーションの場合は ~ 6ms、整数データを使用するアプリケーションの場合は約6ミリ秒となりました。
9. Windows 10 では、すべてのアプリケーションに対して待機時間が ~ 0ms に短縮されています。

10. オーディオエンジンが処理を完了するとすぐに、データを読み取ることができることがアプリケーションに通知されます。
    オーディオスタックには、排他モードのオプションも用意されています。 この場合、データはオーディオエンジンをバイパスし、アプリケーションからドライバーが読み取るバッファーに直接移動します。 ただし、アプリケーションが排他モードでエンドポイントを開いた場合、そのエンドポイントを使用してオーディオをレンダリングしたりキャプチャしたりできるアプリケーションはありません。

低待機時間を必要とするアプリケーションのもう1つの一般的な方法は、排他モードを利用する ASIO (オーディオストリーム入力/出力) モデルを使用することです。 ユーザーがサードパーティ製の ASIO ドライバーをインストールすると、アプリケーションから ASIO ドライバーにデータを直接送信できるようになります。 ただし、アプリケーションは、ASIO ドライバーと直接通信するように記述する必要があります。

どちらの方法 (exclusive モードと ASIO) にも独自の制限があります。 待機時間は短くなりますが、独自の制限があります (上記で説明したものもあります)。 その結果、柔軟性を維持しながら、待機時間を短くするためにオーディオエンジンが変更されています。

## <a name="span-idaudio_stack_improvements_in_windows_10spanspan-idaudio_stack_improvements_in_windows_10spanspan-idaudio_stack_improvements_in_windows_10spanaudio-stack-improvements-in-windows-10"></a><span id="Audio_Stack_Improvements_in_Windows_10"></span><span id="audio_stack_improvements_in_windows_10"></span><span id="AUDIO_STACK_IMPROVEMENTS_IN_WINDOWS_10"></span>Windows 10 でのオーディオスタックの強化

待機時間を短縮するために、次の3つの領域で Windows 10 が強化されています。

1. オーディオを使用するすべてのアプリケーションでは、Windows 8.1 と比較して、コードの変更やドライバーの更新を行わずに、ラウンドトリップの待機時間 (前のセクションで説明したように) で 4.5-16ms を減らすことができます。
   a. 浮動小数点データを使用するアプリケーションでは、160ミリ秒未満の待機時間が発生します。
   b. 整数データを使用するアプリケーションでは、4.5 ミリ秒未満の待機時間が発生します。
2. ドライバーが更新されたシステムでは、さらに短いラウンドトリップ待機時間が提供されます。 ドライバーは、新しい DDIs を使用して、OS と H/W の間でデータを転送するために使用されるバッファーのサポートされているサイズを報告できます。 つまり、データ転送では、以前のバージョンの OS の場合と同じように、常に10ミリ秒バッファーを使用する必要がありません。 代わりに、ドライバーで小さなバッファーを使用できるかどうかを指定できます。たとえば、5ms、3ms、1ミリ秒などです。 低待機時間を必要とするアプリケーションでは、新しいオーディオ Api (AudioGraph または "API") を使用して、ドライバーでサポートされているバッファーサイズを照会し、H/W との間のデータ転送に使用されるバッファーサイズを選択できます。
3. アプリケーションが特定のしきい値を下回るバッファーサイズを使用してオーディオをレンダリングしてキャプチャする場合、OS は特殊モードに入ります。このモードでは、オーディオストリーミングとその他のサブシステム間の干渉を回避する方法でリソースが管理されます。 これにより、オーディオサブシステムの実行の中断を減らし、オーディオの異常の可能性を最小限に抑えることができます。 アプリケーションがストリーミングを停止すると、OS は通常の実行モードに戻ります。 オーディオサブシステムは、次のリソースで構成されています。 a. 低待機時間のオーディオを処理するオーディオエンジンスレッド。
   b. ドライバーによって登録されたすべてのスレッドと割り込み (ドライバーリソースの登録に関するセクションで説明されている新しい DDIs を使用)。
   c. 小さいバッファーを要求するアプリケーションの一部またはすべてのオーディオスレッドと、小さいバッファーを要求したアプリケーションと同じオーディオデバイスグラフを共有するすべてのアプリケーション (同じシグナル処理モードなど)。
4. ストリーミングパスの AudioGraph コールバック。
5. アプリケーションで使用している API が、[リアルタイムの作業キュー API](https://docs.microsoft.com/windows/desktop/ProcThread/platform-work-queue-api)または[**MFCreateMFByteStreamOnStreamEx**](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfcreatemfbytestreamonstreamex)に送信され、"Audio" または "proaudio" とタグ付けされている作業項目のみ。

## <a name="span-idapi_improvementsspanspan-idapi_improvementsspanspan-idapi_improvementsspanapi-improvements"></a><span id="API_Improvements"></span><span id="api_improvements"></span><span id="API_IMPROVEMENTS"></span>API の機能強化

次の2つの Windows 10 Api は、低待機時間機能を提供します。

- [**AudioGraph**](https://docs.microsoft.com/uwp/api/Windows.Media.Audio.AudioGraph)
- [Windows Audio Session API (中 API)](https://docs.microsoft.com/windows/desktop/CoreAudio/wasapi)

アプリケーション開発者は、次の2つの Api のどれを使用するかを決定できます。

- 新しいアプリケーション開発で可能な限り、AudioGraph を優先します。
- 次の場合にのみ、使用している API を使用します。
    - AudioGraph で提供されているものよりも追加の制御が必要です。
    - AudioGraph で提供される待ち時間よりも待機時間が短くなります。

このトピックの「[測定ツール](#measurement_tools)」セクションでは、受信トレイ hdaudio ドライバーを使用して、haswell なシステムからの特定の測定値を示します。

以下のセクションでは、各 API の待機時間の短い機能について説明します。 前のセクションで述べたように、システムが最小待機時間を達成するためには、小さいバッファーサイズをサポートする更新されたドライバーが必要です。

### <a name="span-idaudiographspanspan-idaudiographspanspan-idaudiographspanaudiograph"></a><span id="AudioGraph"></span><span id="audiograph"></span><span id="AUDIOGRAPH"></span>AudioGraph

AudioGraph は、対話型の音楽作成シナリオを簡単に実現することを目的とした、Windows 10 の新しいユニバーサル Windows プラットフォーム API です。 AudioGraph は、いくつかのプログラミング言語 (C++、C#、JavaScript) で使用でき、シンプルで機能豊富なプログラミングモデルを備えています。

低待機時間のシナリオを対象とするために、AudioGraph には[Audiographsettings:: QuantumSizeSelectionMode プロパティ](https://docs.microsoft.com/uwp/api/Windows.Media.Audio.AudioGraphSettings#Windows_Media_Audio_AudioGraphSettings_QuantumSizeSelectionMode)が用意されています。 このプロパティは、次の表に示す値のいずれかになります。

|||
|--- |--- |
|値|[説明]|
|SystemDefault|バッファーを既定のバッファーサイズ (~ 10 ミリ秒) に設定します。|
|LowestLatency|バッファーをドライバーでサポートされている最小値に設定します。|
|ClosestToDesired|バッファーサイズを、DesiredSamplesPerQuantum プロパティで定義された値に等しいか、ドライバーでサポートされている DesiredSamplesPerQuantum の近くにある値に設定します。|

 AudioCreation サンプル (GitHub からダウンロード可能) では、 <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AudioCreation> オーディオグラフを使用して待機時間を短くする方法を示しています。 次のコードスニペットは、最小バッファーサイズを設定する方法を示しています。

```csharp
AudioGraphSettings settings = new AudioGraphSettings(AudioRenderCategory.Media);
settings.QuantumSizeSelectionMode = QuantumSizeSelectionMode.LowestLatency;
CreateAudioGraphResult result = await AudioGraph.CreateAsync(settings);
```

### <a name="span-idwindows_audio_session_api_wasapispanspan-idwindows_audio_session_api_wasapispanspan-idwindows_audio_session_api_wasapispanwindows-audio-session-api-wasapi"></a><span id="Windows_Audio_Session_API_WASAPI"></span><span id="windows_audio_session_api_wasapi"></span><span id="WINDOWS_AUDIO_SESSION_API_WASAPI"></span>Windows Audio Session API (中 API)

Windows 10 以降では、次のように、の中で API が強化されています。

- 特定のオーディオデバイスのオーディオドライバーでサポートされているバッファーサイズ (周期性値) の範囲をアプリケーションが検出できるようにします。 これにより、 &lt; 共有モードでストリームを開くときに、アプリケーションが既定のバッファーサイズ (10 ミリ秒) または小さいバッファー (10 ミリ秒) のいずれかを選択できるようになります。 アプリケーションでバッファーサイズが指定されていない場合は、既定のバッファーサイズが使用されます。
- オーディオエンジンの現在の形式と周期性をアプリケーションが検出できるようにします。 これにより、アプリケーションはオーディオエンジンの現在の設定にスナップできます。
- オーディオエンジンによって再サンプリングされることなく、指定した形式でレンダリングまたはキャプチャするようにアプリに指定できます。

上記の機能は、すべての Windows デバイスで使用できるようになります。 ただし、リソースが十分にあり、ドライバーが更新されている特定のデバイスでは、他よりも優れたユーザーエクスペリエンスが提供されます。

上記の機能は、 [**IAudioClient2**](https://docs.microsoft.com/windows/desktop/api/audioclient/nn-audioclient-iaudioclient2)から派生した[**IAudioClient3**](https://docs.microsoft.com/windows/desktop/api/audioclient/nn-audioclient-iaudioclient3)という新しいインターフェイスによって提供されます。

[**IAudioClient3**](https://docs.microsoft.com/windows/desktop/api/audioclient/nn-audioclient-iaudioclient3)は、次の3つのメソッドを定義します。

|||
|--- |--- |
|メソッド|説明|
|GetCurrentSharedModeEnginePeriod|オーディオエンジンの現在の形式と周期性を返します。|
|GetSharedModeEnginePeriod|エンジンによってサポートされる、指定されたストリーム形式の周期性の範囲を返します|
|InitializeSharedAudioStream|指定した周期性を使用して共有ストリームを初期化します|

(GitHub で利用可能な) IAudioClient3 オーディオサンプルは、 <https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WindowsAudioSession> 低待機時間に対してを使用する方法を示しています。

次のコードスニペットは、システムでサポートされている最も短い待機時間設定で音楽作成アプリを操作する方法を示しています。

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

また、MFCreateMFByteStreamOnStreamEx API を使用するアプリケーションでは、[リアルタイムの作業キュー API](https://docs.microsoft.com/windows/desktop/ProcThread/platform-work-queue-api)または[**MFCreateMFByteStreamOnStreamEx**](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfcreatemfbytestreamonstreamex)を使用して作業項目を作成し、独自のスレッドではなく、オーディオまたは Pro オーディオとしてタグ付けすることもお勧めします。 これにより、干渉しない非オーディオサブシステムを回避する方法で OS が管理できるようになります。 これに対して、すべての AudioGraph スレッドは、OS によって自動的に適切に管理されます。 次のコードスニペットでは、メインフレームのワークキュー Api を使用する方法を示しています。

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

また、次のコードスニペットは、RT ワークキュー Api を使用する方法を示しています。

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

最後に、中の API を使用するアプリケーション開発者は、各ストリームの機能に基づいて、オーディオカテゴリでストリームにタグを付ける必要があります。また、生のシグナル処理モードを使用するかどうかを指定する必要があります。 影響が認識されない限り、すべてのオーディオストリームで未加工のシグナル処理モードを使用しないことをお勧めします。 Raw モードでは、OEM によって選択されたすべてのシグナル処理がバイパスされるため、次のようになります。

- 特定のエンドポイントのレンダー信号は、非常に最適化されている場合があります。
- キャプチャシグナルは、アプリケーションが理解できない形式になる場合があります。
- 待機時間が改善される可能性があります。

## <a name="span-iddriver_improvementsspanspan-iddriver_improvementsspanspan-iddriver_improvementsspandriver-improvements"></a><span id="Driver_Improvements"></span><span id="driver_improvements"></span><span id="DRIVER_IMPROVEMENTS"></span>ドライバーの機能強化

オーディオドライバーで低待機時間をサポートするために、Windows 10 には次の3つの新機能が用意されています。

1. \[必須 \] 各モードでサポートされている最小バッファーサイズを宣言します。
2. \[省略可能ですが、 \] ドライバーと OS の間のデータフローの調整を向上させることをお勧めします。
3. \[省略可能ですが、 \] 低待機時間シナリオで OS によって保護できるように、ドライバーリソース (割り込み、スレッド) を登録することをお勧めします。
hdaudbus.sys によって既に実行されているため、受信トレイ HDAudio bus ドライバー hdaudbus.sys によって列挙される HDAudio ミニポート関数ドライバーは、HDAudio 割り込みを登録する必要がありません。 ただし、ミニポートドライバーが独自のスレッドを作成する場合は、それを登録する必要があります。

次の3つのセクションでは、新しい機能の詳細について説明します。

**1. 最小バッファーサイズを宣言します。**

ドライバーは、OS、ドライバー、およびハードウェア間でオーディオデータを移動するときに、さまざまな制約の下で動作します。 これらの制約は、メモリとハードウェア間でデータを移動する物理ハードウェアトランスポート、またはハードウェアまたは関連する DSP 内の信号処理モジュールによって発生することがあります。

Windows 10 では、ドライバーは DEVPKEY \_ ksaudio \_ PacketSize Constraints デバイスプロパティを使用してバッファーサイズ機能を表現でき \_ ます。 このプロパティを使用すると、ユーザーは、ドライバーによってサポートされる絶対最小バッファーサイズと、各シグナル処理モードの特定のバッファーサイズ制約を定義できます (モード固有の制約は、ドライバーの最小バッファーサイズよりも大きくする必要があります。それ以外の場合は、オーディオスタックによって無視されます)。 たとえば、次のコードスニペットは、サポートされている絶対バッファーサイズが1ミリ秒であることをドライバーが宣言する方法を示していますが、既定のモードでは128フレーム (48 kHz サンプルレートを想定している場合は3ミリ秒に対応) がサポートされています。

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

これらの構造に関する詳細な情報については、次のトピックを参照してください。

-   [**KSAUDIO \_ PACKETSIZE \_ CONSTRAINTS 構造体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)
-   [**KSAUDIO \_ PACKETSIZE \_ processingmode \_ 制約構造体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)

また、sysvad サンプル () は、 <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad> ドライバーが各モードの最小バッファーを宣言するために、これらのプロパティの使用方法を示しています。

**2. ドライバーと OS の調整を改善します。**

このセクションで説明されている DDIs を使用すると、ドライバーは次のことを実行できます。

-   コーデックのリンク位置に基づいて OS が推測するのではなく、OS で使用できるバッファーのハーフ (パケット) を明確に示します。 これにより、OS はオーディオの処理速度を向上させることができます。
-   必要に応じて、WaveRT バッファーとの間でのデータ転送を最適化または簡素化します。 ここでの利点は、DMA エンジンの設計や、WaveRT バッファーと (場合によっては DSP) ハードウェア間のその他のデータ転送メカニズムによって異なります。
-   キャプチャされたデータが、ドライバーによって内部的に蓄積された場合、リアルタイムでキャプチャされたデータを "バースト" します。 これは、主に音声ライセンス認証のシナリオを対象としていますが、通常のストリーミングでも適用できます。
-   OS の推測ではなく、現在のストリームの位置に関するタイムスタンプ情報を指定します。これにより、正確な位置情報が得られる可能性があります。

この DDI は、DSP が使用されている場合に非常に便利です。 ただし、standard HD Audio driver またはその他の単純な DMA バッファーの設計では、ここに記載されている新しい DDIs ではあまりメリットが得られない場合があります。

-   [IMiniportWaveRTInputStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertinputstream)
-   [IMiniportWaveRTOutputStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertoutputstream)

いくつかのドライバールーチンは、デバイスによってサンプルがキャプチャまたは表示される時刻を反映する Windows パフォーマンスカウンターのタイムスタンプを返します。

複雑な DSP パイプラインと信号処理があるデバイスでは、正確なタイムスタンプを計算することは困難であるため、熟考を行う必要があります。 タイムスタンプには、サンプルが OS と DSP 間で転送された時刻を単に反映させることはできません。

パフォーマンスカウンターの値を計算するために、ドライバーと DSP は次のいずれかの方法を使用する場合があります。

-   DSP 内で、一部の内部 DSP ウォールクロックを使用してサンプルタイムスタンプを追跡します。
-   ドライバーと DSP の間で、Windows パフォーマンスカウンターと DSP の壁面クロックの間の相関関係を計算します。 この手順は、非常に単純な (ただし、正確ではありませんが) 非常に複雑なものや斬新なもの (より正確です) の範囲です。
-   シグナル処理アルゴリズムまたはパイプラインまたはハードウェアトランスポートに起因する一定の遅延を考慮します。ただし、これらの遅延が考慮されない場合は除きます。

Sysvad サンプル () は、 <https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad> 上記の DDIs を使用する方法を示しています。

**3. ドライバーリソースを登録する**

エラーのない操作を確実に行うために、オーディオドライバーは portcls にストリーミングリソースを登録する必要があります。 これにより、OS はリソースを管理して、オーディオストリーミングとその他のオペレーティングシステム間の干渉を回避できます。

ストリームリソースは、オーディオストリームを処理したり、オーディオデータフローを確認したりするためにオーディオドライバーによって使用される任意のリソースです。 現時点では、2種類のストリームリソース (割り込みとドライバー所有のスレッド) のみがサポートされています。 オーディオドライバーは、リソースの作成後にリソースを登録し、削除する前にリソースの登録を解除する必要があります。

オーディオドライバーは、ドライバーが読み込まれたとき、または実行時 (たとえば i/o リソースの再調整が発生したとき) に、初期化時にリソースを登録できます。 Portcls はグローバル状態を使用して、すべてのオーディオストリーミングリソースを追跡します。

待機時間が非常に短いオーディオを必要とする場合など、一部のユースケースでは、OS は、他の OS、アプリケーション、およびハードウェアのアクティビティからの干渉から、オーディオドライバーの登録済みリソースを分離しようとします。 この操作は、オーディオドライバーのリソースの登録を除き、オーディオドライバーと対話することなく、必要に応じて行うことができます。

ストリームリソースを登録するための要件は、ストリーミングパイプラインパス内のすべてのドライバーが、Portcls を使用して直接または間接的にリソースを登録する必要があることを意味します。 オーディオミニポートドライバーには、次のオプションがあります。

-   オーディオミニポートドライバーは、スタックの一番下にあるドライバー (h/w を直接インターフェイス) です。この場合、ドライバーはストリームリソースを認識し、Portcls に登録することができます。
-   オーディオミニポートドライバーは、他のドライバー (例のオーディオバスドライバー) を使用してオーディオをストリーミングします。 これらの他のドライバーは、Portcls に登録する必要があるリソースも使用します。 これらの並列/バスドライバースタックは、オーディオミニポートドライバーがこの情報を収集するために使用するパブリック (または、1つのベンダーがすべてのドライバーを所有している場合はプライベートインターフェイス) を公開できます。
-   オーディオミニポートドライバーは、他のドライバー (hdaudbus など) のヘルプを使用してオーディオをストリーミングします。 これらの他のドライバーは、Portcls に登録する必要があるリソースも使用します。 これらの並列/バスドライバーは、Portcls とリンクして、リソースを直接登録できます。 オーディオミニポートドライバーは、これらの他の並列/バスデバイス (PDOs) のリソースに依存していることを Portcls に知らせる必要があることに注意してください。 Hd-audio infrastructure は、このオプションを使用します。つまり、Portcls とリンクされている hd オーディオバスドライバーは、次の手順を自動的に実行します。
    -   バスドライバーのリソースを登録します。
    -   子のリソースが親のリソースに依存していることを Portcls に通知します。 HD オーディオアーキテクチャでは、オーディオミニポートドライバーが独自のドライバー所有のスレッドリソースを登録するだけで済みます。

メモ:

-   hdaudbus.sys によって既に実行されているため、受信トレイ HDAudio bus ドライバー hdaudbus.sys によって列挙される HDAudio ミニポート関数ドライバーは、HDAudio 割り込みを登録する必要がありません。 ただし、ミニポートドライバーが独自のスレッドを作成する場合は、それを登録する必要があります。
-   ストリーミングリソースを登録する目的でのみ Portcls とリンクするドライバーでは、が含まれている必要があります。また、必要に応じて、(および依存ファイル) を portcls.sys コピーします。 新しい INF copy セクションは、これらのファイルのみをコピーするために、wdmaudio に定義されています。
-   Windows 10 でのみ実行されるオーディオドライバーは、次のようなハードリンクを行うことができます。
    -   [**PcAddStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddstreamresource)
    -   [**PcRemoveStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcremovestreamresource)
-   ダウンレベルの OS で実行する必要があるオーディオドライバーは、次のインターフェイスを使用できます (ミニポートは、IID \_ iportclsstreamresourcemanager インターフェイスの QueryInterface を呼び出し、PortCls がインターフェイスをサポートしている場合にのみそのリソースを登録できます)。
    -   [IPortClsStreamResourceManager](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsstreamresourcemanager)
        -   [**AddStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsstreamresourcemanager-addstreamresource)
        -   [**RemoveStreamResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsstreamresourcemanager-removestreamresource)
-   これらの DDIs は、次の列挙型と構造体を使用します。
    -   [**PcStreamResourceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ne-portcls-_pcstreamresourcetype)
    -   [**PCSTREAMRESOURCE \_ 記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcstreamresource_descriptor)

最後に、リソースの登録のみを目的として PortCls を使用するドライバーは、その inf の DDInstall セクションに次の2行を追加する必要があります。 オーディオミニポートドライバーは、既に wdmaudio にインクルード/ニーズがあるため、これを必要としません。

```inf
[<install-section-name>]
Include=wdmaudio.inf
Needs=WDMPORTCLS.CopyFilesOnly
```

上記の行では、PortCls とその依存ファイルがインストールされていることを確認します。

## <a name="span-idmeasurement_toolsspanspan-idmeasurement_toolsspanspan-idmeasurement_toolsspanmeasurement-tools"></a><span id="Measurement_Tools"></span><span id="measurement_tools"></span><span id="MEASUREMENT_TOOLS"></span>測定ツール

ユーザーは、ラウンドトリップの待機時間を測定するために、スピーカーを介してパルスを再生し、マイク経由でキャプチャするツールを使用できます。 次のパスの遅延を測定します。

1. アプリケーションは、render API (AudioGraph または ' という) を呼び出して、パルスを再生します。
2. 音声はスピーカー経由で再生されます。
3. オーディオはマイクからキャプチャされます。
4. さまざまなバッファーサイズのラウンドトリップの待機時間を測定するために、キャプチャ API (AudioGraph または ' 中 API) によってパルスが検出されます。ユーザーは、小さなバッファーをサポートするドライバーをインストールする必要があります。 受信トレイ HDAudio ドライバーは、128サンプル ( 2.66ms@48kHz ) と480サンプル () の間のバッファーサイズをサポートするように更新されました 10ms@48kHz 。 次の手順は、受信トレイ HDAudio ドライバー (すべての Windows 10 Sku の一部) をインストールする方法を示しています。

- デバイス マネージャーを開始します。
- [**サウンドビデオとゲームコントローラー**] で、内部スピーカーに対応するデバイスをダブルクリックします。
- 次のウィンドウで、[**ドライバー** ] タブにアクセスします。
- [**ドライバーの更新**] を選択し  - &gt; **て [コンピューターを参照してドライバーソフトウェアを検索**する] [  - &gt; **このコンピューターのデバイスドライバーの一覧から選択する**] [  - &gt; **高解像度オーディオデバイス] を選択**し、[**次へ**] をクリックします。
- [ドライバーの警告を更新する] というタイトルのウィンドウが表示されたら、[**はい]** をクリックします。
- [**閉じる**] を選択します。
- システムの再起動を求められた場合は、[**はい**] を選択して再起動します。
- 再起動後、システムは、サードパーティ製のコーデックドライバーではなく、受信トレイ Microsoft HDAudio ドライバーを使用します。 オーディオコーデックに最適な設定を使用する場合は、以前に使用していたドライバーを忘れないようにしてください。

![異なるバッファーサイズを持つ、中規模の api と audiograph 間のラウンドトリップの待機時間の差を示すグラフ。 ](images/low-latency-audio-roundtrip-latency.png)

次の理由により、中 API と AudioGraph の間の待機時間の違いがわかります。

- AudioGraph は、レンダリングとキャプチャを同期するために、キャプチャ側に1つの待機時間バッファーを追加します (これは、' 中 API ' では提供されません)。 この追加により、AudioGraph を使用して作成されたアプリケーションのコードが簡略化されます。
- システムが6ms バッファーを使用しているときに、AudioGraph のレンダリング側に待機時間の追加バッファーがあり &gt; ます。
- AudioGraph には、オーディオ効果のキャプチャを無効にするオプションがありません

## <a name="span-idsamplesspanspan-idsamplesspanspan-idsamplesspansamples"></a><span id="Samples"></span><span id="samples"></span><span id="SAMPLES"></span>Samples

- 中 API Audio のサンプル:<https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WindowsAudioSession>
- AudioCreation サンプル (Audiocreation):<https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AudioCreation>
- Sysvad driver サンプル:<https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad>

## <a name="span-idfaqspanspan-idfaqspanfaq"></a><span id="FAQ"></span><span id="faq"></span>FAQ

**1. すべてのアプリケーションで新しい Api を使用して待機時間を短縮することはできませんか。低待機時間では、ユーザーの操作性が向上していることを常に保証しますか。**

必ずしもその必要はありません。 待機時間を短くすると、トレードオフが発生します。

- 低待機時間は、電力消費量が高くなることを意味します。 システムで10ミリ秒バッファーが使用されている場合は、CPU がすべての10ミリ秒をウェイクアップし、データバッファーにデータを入力して、スリープ状態に移行することを意味します。 ただし、システムで1ミリ秒バッファーが使用されている場合は、CPU がすべての1ミリ秒をウェイクアップすることを意味します。 2番目のシナリオでは、CPU が頻繁にウェイクアップし、電力消費量が増加することを意味します。 これにより、バッテリの寿命が減少します。
- ほとんどのアプリケーションは、最適なユーザーエクスペリエンスを提供するためにオーディオ効果に依存しています。 たとえば、メディアプレーヤーでは、再現性の高いオーディオを提供する必要があります。 通信アプリケーションは、最小限のエコーとノイズを必要とします。 これらの種類のオーディオ効果をストリームに追加すると、待機時間が長くなります。 これらのアプリケーションは、オーディオの待ち時間よりもオーディオ品質に関心があります。

要約すると、各アプリケーションの種類には、オーディオの待機時間に関するさまざまなニーズがあります。 アプリケーションの待機時間を短くする必要がない場合、待機時間を短くするために新しい Api を使用しないでください。

**2. Windows 10 に更新されるすべてのシステムは、小さいバッファーをサポートするように自動的に更新されますか。また、すべてのシステムで同じ最小バッファーサイズがサポートされますか。**

いいえ。 システムで小さなバッファーをサポートするためには、ドライバーを更新する必要があります。 どのシステムが小さなバッファーをサポートするように更新されるかは、Oem によって決定されます。 また、より新しいシステムは、古いシステムよりも小さなバッファーをサポートするためにより多くの likey です (つまり、新しいシステムの待機時間が古いシステムよりも低い可能性があります)。

**3. ドライバーが小さいバッファーサイズ (10 ミリ秒バッファー) をサポートしている場合 &lt; 、Windows 10 のすべてのアプリケーションは自動的に小さいバッファーを使用してオーディオをレンダリングし、キャプチャしますか。**

いいえ。 既定では、Windows 10 のすべてのアプリケーションは、10ミリ秒バッファーを使用してオーディオのレンダリングとキャプチャを行います。 アプリケーションで小さなバッファーを使用する必要がある場合は、そのために、新しい AudioGraph 設定または IAudioClient3 インターフェイスを使用する必要があります。 ただし、Windows 10 の1つのアプリケーションが小さなバッファーの使用を要求した場合、オーディオエンジンはその特定のバッファーサイズを使用してオーディオの転送を開始します。 その場合、同じエンドポイントとモードを使用するすべてのアプリケーションは、その小さいバッファーサイズに自動的に切り替わります。 低待機時間のアプリケーションが終了すると、オーディオエンジンは10ミリ秒バッファーに再び切り替えます。
