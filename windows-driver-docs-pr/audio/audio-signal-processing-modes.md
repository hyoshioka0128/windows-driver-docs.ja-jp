---
title: オーディオ信号の処理モード
description: ドライバーは、各デバイスのサポートされているオーディオシグナル処理モードを宣言します。
ms.assetid: 104275F8-2302-484B-B673-7448CAA1F793
ms.date: 05/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 28fffee7b4fc41648f146e752ea26da51f58780c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831321"
---
# <a name="audio-signal-processing-modes"></a>オーディオ信号の処理モード


ドライバーは、各デバイスのサポートされているオーディオシグナル処理モードを宣言します。

## <a name="span-idavailable_signal_processing_modesspanspan-idavailable_signal_processing_modesspanspan-idavailable_signal_processing_modesspanavailable-signal-processing-modes"></a><span id="Available_Signal_Processing_Modes"></span><span id="available_signal_processing_modes"></span><span id="AVAILABLE_SIGNAL_PROCESSING_MODES"></span>使用可能なシグナル処理モード


オーディオカテゴリ (アプリケーションによって選択されます) は、(ドライバーによって定義された) オーディオモードにマップされます。 Windows では、7つのオーディオ信号処理モードを定義します。 Oem と Ihv は、どのモードを実装するかを決定できます。 Ihv/Oem は、新しいモードを利用して、最適なユーザーエクスペリエンスを提供するためにオーディオ信号を最適化するオーディオ効果を追加することをお勧めします。 これらのモードの概要を次の表に示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>モード</strong></td>
<td align="left"><strong>レンダリング/キャプチャ</strong></td>
<td align="left"><strong>説明</strong></td>
</tr>
<tr class="even">
<td align="left">直接</td>
<td align="left">どちらもオン</td>
<td align="left"><p>Raw モードでは、ストリームにシグナル処理を適用しないことを指定します。</p>
<p>アプリケーションは、まったく手を加えずに独自のシグナル処理を実行する未加工ストリームを要求できます。</p></td>
</tr>
<tr class="odd">
<td align="left">Default</td>
<td align="left">どちらもオン</td>
<td align="left"><p>このモードは、既定のオーディオ処理を定義します。</p></td>
</tr>
<tr class="even">
<td align="left">映像</td>
<td align="left">Render</td>
<td align="left">ムービーオーディオ再生</td>
</tr>
<tr class="odd">
<td align="left">用紙</td>
<td align="left">どちらもオン</td>
<td align="left">音楽オーディオ再生 (ほとんどのメディアストリームでは既定)</td>
</tr>
<tr class="even">
<td align="left">スピーチ</td>
<td align="left">キャプチャ</td>
<td align="left">人間の声のキャプチャ (Cortana への入力など)</td>
</tr>
<tr class="odd">
<td align="left">接続</td>
<td align="left">どちらもオン</td>
<td align="left">VOIP のレンダーとキャプチャ (例: Skype、Lync)</td>
</tr>
<tr class="even">
<td align="left">警告</td>
<td align="left">Render</td>
<td align="left">着信音、アラーム、アラートなど</td>
</tr>
</tbody>
</table>

 

Windows 10 の新 \*。

## <a name="span-idsignal_processing_mode_driver_requirementsspanspan-idsignal_processing_mode_driver_requirementsspanspan-idsignal_processing_mode_driver_requirementsspansignal-processing-mode-driver-requirements"></a><span id="Signal_Processing_Mode_Driver_Requirements"></span><span id="signal_processing_mode_driver_requirements"></span><span id="SIGNAL_PROCESSING_MODE_DRIVER_REQUIREMENTS"></span>シグナル処理モードドライバーの要件


オーディオデバイスドライバは、少なくとも*Raw*モードまたは*Default*モードをサポートしている必要があります。 追加モードのサポートはオプションです。

すべてのモードが特定のシステムで使用できるとは限りません。 ドライバーは、サポートするシグナル処理モード (たとえば、ドライバーの一部としてインストールされる APOs の種類) を定義し、それに応じて OS に通知します。 特定のモードがドライバーでサポートされていない場合、Windows は次の最適な一致モードを使用します。

次の図は、複数のモードをサポートするシステムを示しています。

![複数のオーディオモード ](images/audio-modes-win-10.png)

## <a name="span-idwindows_audio_stream_categoriesspanspan-idwindows_audio_stream_categoriesspanspan-idwindows_audio_stream_categoriesspanwindows-audio-stream-categories"></a><span id="Windows_Audio_Stream_Categories"></span><span id="windows_audio_stream_categories"></span><span id="WINDOWS_AUDIO_STREAM_CATEGORIES"></span>Windows オーディオストリームのカテゴリ


オーディオストリームの使用状況についてシステムに通知するために、アプリケーションでは、特定のオーディオストリームカテゴリを使用してストリームにタグを付けることができます。 オーディオストリームの作成直後にオーディオ Api のいずれかを使用して、アプリケーションでオーディオカテゴリを設定できます。 Windows 10 では、9つのオーディオストリームカテゴリがあります。

|                |                                                                                                       |
|----------------|-------------------------------------------------------------------------------------------------------|
| **カテゴリ**   | **説明**                                                                                       |
| ムービー          | ムービー、ダイアログ付きビデオ (ForegroundOnlyMedia を置換)                                              |
| [Media]          | メディア再生の既定のカテゴリ (BackgroundCapableMedia を置換)                                 |
| ゲーム チャット      | ユーザー間のゲーム内通信 (Windows 10 の新しいカテゴリ)                                      |
| [音声認識]         | 音声入力 (例: personal assistant) と出力 (ナビゲーションアプリなど) (Windows 10 の新しいカテゴリ) |
| Communications | VOIP、リアルタイムチャット                                                                                  |
| [アラート]         | アラーム、リングトーン、通知                                                                       |
| サウンド効果  | ビープ音、dings、その他                                                                                     |
| ゲームメディア     | ゲームミュージック                                                                                         |
| ゲーム効果   | ボールのバウンス、車のエンジンサウンド、箇条書きなど                                                      |
| Other          | 未カテゴリのストリーム                                                                                 |

 

前述のように、オーディオカテゴリ (アプリケーションによって選択されます) は、(ドライバーによって定義された) オーディオモードにマップされます。 アプリケーションでは、各ストリームに、10個のオーディオカテゴリの1つをタグ付けることができます。

アプリケーションには、オーディオカテゴリと信号処理モードの間のマッピングを変更するオプションはありません。 アプリケーションは、"オーディオ処理モード" の概念を認識していません。 各ストリームで使用されるモードを確認することはできません。

**中 API のコードサンプル**

次の中からの API コードでは、中から、さまざまなオーディオカテゴリを設定する方法を示しています。

```cpp
// The ActivateAudioInterfaceAsync is a replacment for IMMDevice::Activate
IActivateAudioInterfaceAsyncOperation *asyncOp = nullptr;
HRESULT hr = S_OK;

String ^defaultRender = Windows::Media::Devices::MediaDevice::GetDefaultAudioRenderId( Windows::Media::Devices::AudioDeviceRole::Default );

hr = ActivateAudioInterfaceAsync( defaultRender->Data(), __uuidof( IAudioClient3 ), nullptr, this, &asyncOp );
if ( FAILED( hr ) ) { … }
…

// the app’s implementation of IActivateAudioInterfaceCompetionHandler is invoked asynchronously
HRESULT ActivateAudioInterfaceCompletionHandler::ActivateCompleted( IActivateAudioInterfaceAsyncOperation *activateOperation ) {
    HRESULT hr = S_OK;
    HRESULT hrActivateResult = S_OK;
    IUnknown *pUnknown = nullptr;
    IAudioClient3 *pAudioClient3 = nullptr;

    hr = activateOperation->GetActivateResult( &hrActivateResult, &pUnknown );
    if ( FAILED( hr ) )  { … }
    if ( FAILED( hrActivateResult ) ) { … }
    
    hr = pUnknown->QueryInterface( IID_PPV_ARGS( &pAudioClient3 ) );
    if ( FAILED( hr ) ) { … }

    // The IAudioClient3::SetClientProperties call needs to happen after activation completes, 
    // but before the call to IAudioClient3::Initialize or IAudioClient3::InitializeSharedAudioStream.
    AudioClientProperties props = {};
    props.cbSize = sizeof(props);
    props.eCategory = AudioCategory_GameEffects;
    pAudioClient3->SetClientProperties( &props );
    if ( FAILED( hr ) ) { … }

    hr = pAudioClient3->InitializeSharedAudioStream( … );
    if ( FAILED( hr ) ) { … }

    …
```

## <a name="span-idsignal_processing_modes_and_effectsspanspan-idsignal_processing_modes_and_effectsspanspan-idsignal_processing_modes_and_effectsspansignal-processing-modes-and-effects"></a><span id="Signal_Processing_Modes_and_Effects"></span><span id="signal_processing_modes_and_effects"></span><span id="SIGNAL_PROCESSING_MODES_AND_EFFECTS"></span>シグナル処理モードと効果


Oem は、各モードで使用する効果を定義します。 Windows では、17個の種類のオーディオ効果の一覧を定義します。

APOs をモードに関連付ける方法については、「[オーディオ処理オブジェクトの実装](implementing-audio-processing-objects.md)」を参照してください。

アプリケーションでは、未加工または非生の処理に対して特定のストリームにどのような影響が適用されるかを確認することができます。 また、アプリケーションは、効果または未処理の処理状態が変化したときに通知を受け取るように要求することもできます。 アプリケーションでは、この情報を使用して、通信などの特定のストリーミングカテゴリが使用可能かどうか、または RAW モードのみが使用されているかどうかを判断できます。 RAW モードのみが使用可能な場合、アプリケーションは、それ自体が追加するオーディオ処理の量を判断できます。

使用できる場合は、アプリケーションでは、特定のストリームに対して "未加工の使用" フラグを設定することもできます。 System.string が supported でサポートされている場合、アプリケーションは "未加工の使用" フラグを設定できません。

アプリケーションは、未加工/非未加工を除き、存在するモードの数を表示できません。

アプリケーションは、オーディオハードウェア構成に関係なく、最適なオーディオ効果処理を要求する必要があります。 たとえば、通信としてストリームにタグを付けて、Windows がバックグラウンドミュージックを一時停止できるようにすることができます。

静的なオーディオストリームのカテゴリの詳細については、「 [AudioCategory enumeration](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.AudioCategory) and [AudioCategory プロパティ](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement#Windows_UI_Xaml_Controls_MediaElement_AudioCategory)」を参照してください。

## <a name="span-idclsids_for_system_effectsspanspan-idclsids_for_system_effectsspanspan-idclsids_for_system_effectsspanclsids-for-system-effects"></a><span id="CLSIDs_for_System_Effects"></span><span id="clsids_for_system_effects"></span><span id="CLSIDS_FOR_SYSTEM_EFFECTS"></span>システム効果の Clsid


**FX\_、APO\_CLSID\_\_効果の検出**

これは、ドライバーに対してクエリを行ってアクティブな効果の一覧を取得する、MsApoFxProxy の "プロキシ効果" の CLSID です。

```cpp
FX_DISCOVER_EFFECTS_APO_CLSID  = "{889C03C8-ABAD-4004-BF0A-BC7BB825E166}"
```

**KSK ATTRIBUTEID\_AUDIOSIGNALPROCESSING\_モード**

KSK ATTRIBUTEID\_AUDIOSIGNALPROCESSING\_MODE は、参照されている特定の属性がシグナル処理モード属性であることを識別するカーネルストリーミングの識別子です。

ここに示す \#define ステートメントは、KSMedia .h ヘッダーファイルで使用できます。

```cpp
#define STATIC_KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE 0xe1f89eb5, 0x5f46, 0x419b, 0x96, 0x7b, 0xff, 0x67, 0x70, 0xb9, 0x84, 0x1
DEFINE_GUIDSTRUCT("E1F89EB5-5F46-419B-967B-FF6770B98401", KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE);
#define KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE DEFINE_GUIDNAMED(KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE)
```

KSK ATTRIBUTEID\_AUDIOSIGNALPROCESSING\_モードは、 [**Ksk 属性\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksattribute_list)を含む[**ksk datarの**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造を持つモードを認識するドライバーによって使用されます。 このリストには、 [**Ksk 属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksattribute)である1つの要素が含まれています。 **Ksk 属性**構造体の属性メンバーが ksk ATTRIBUTEID\_AUDIOSIGNALPROCESSING\_MODE に設定されています。

## <a name="span-idaudio_effectsspanspan-idaudio_effectsspanspan-idaudio_effectsspanaudio-effects"></a><span id="Audio_Effects"></span><span id="audio_effects"></span><span id="AUDIO_EFFECTS"></span>オーディオ効果


Windows 10 では、次のオーディオ効果を利用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">音響エコーキャンセル (AEC)</td>
<td align="left"><p>音響エコーキャンセル (AEC) は、エコーを削除した後、オーディオストリームに既に存在していたオーディオ品質を向上させます。</p></td>
</tr>
<tr class="even">
<td align="left">ノイズ抑制 (NS)</td>
<td align="left"><p>ノイズ抑制 (NS) は、オーディオストリームに存在する場合、humming やブーンなどのノイズを抑制します。</p></td>
</tr>
<tr class="odd">
<td align="left">自動ゲイン制御 (AGC)</td>
<td align="left"><p>自動ゲイン制御 (AGC)-入力信号の振幅の変動に関係なく、出力で制御されるシグナル振幅を提供するように設計されています。 平均またはピーク出力信号レベルは、入力から出力への到達率を適切な値に動的に調整するために使用されます。これにより、さまざまな入力信号レベルでも安定した出力レベルが有効になります。</p></td>
</tr>
<tr class="even">
<td align="left">ビーム成形 (BF)</td>
<td align="left"><p>ビーム成形 (BF) は、方向シグナルの送信または受信に使用されるシグナル処理手法です。 これは、段階的な配列内の要素を組み合わせることによって実現されます。このような方法では、特定の角度での信号は建設的な干渉を受け、他のユーザーは破壊的な干渉を受けます 無指向性の受信/送信と比較した場合の改善点は、受信/送信の利益 (または損失) と呼ばれます。</p></td>
</tr>
<tr class="odd">
<td align="left">定数の削除</td>
<td align="left"><p>固定音の除去は、テープのヒスノイズ、電気ファン、hums など、一定のバックグラウンドノイズを減衰するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left">Equalizer</td>
<td align="left"><p>イコライザー効果は、線形フィルターを使用してオーディオシステムの周波数応答を変更するために使用されます。 これにより、高音や低音の設定と同様に、信号のさまざまな部分をブーストすることができます。</p></td>
</tr>
<tr class="odd">
<td align="left">ラウドネスイコライザー</td>
<td align="left"><p>ラウドネスイコライザー効果は、オーディオ出力を平準化することで、知覚するボリュームの違いを軽減します。これにより、音量が小さく、音が小さくなるほど、平均のレベルがラウドネスに近づきます。</p></td>
</tr>
<tr class="even">
<td align="left">低音ブースト</td>
<td align="left"><p>低音機能が制限されているスピーカーを搭載したラップトップなどのシステムでは、スピーカーでサポートされている周波数の範囲内で低音応答をブーストすることで、音声の知覚品質を向上させることができます。 低音ブーストでは、非常に小さなスピーカーを使用したモバイルデバイスのサウンドを向上させます。</p></td>
</tr>
<tr class="odd">
<td align="left">仮想サラウンド</td>
<td align="left"><p>Virtual サラウンドは、単純なデジタルメソッドを使用して、マルチチャネル信号を2つのチャネルに結合します。 これは、最新のオーディオレシーバーで使用可能な Pro ロジックデコーダーを使用して、変換されたシグナルを元のマルチチャネルシグナルに復元できるようにするために行われます。 Virtual サラウンドは、2チャネルのサウンドハードウェアと、サラウンドサウンド拡張メカニズムを備えたレシーバーを持つシステムに最適です。</p></td>
</tr>
<tr class="even">
<td align="left">仮想ヘッドホン</td>
<td align="left"><p>仮想化されたサラウンドサウンドを使用すると、ヘッドホンを装着しているユーザーが、前後のサウンドと左右の音を区別できるようになります。 これは、脳がサウンドをローカライズし、サウンドフィールドに統合するのに役立つ、空間キューを送信することによって行われます。 これは、ヘッドホンのよりも優先のように聞こえて、"社外の" リスニングエクスペリエンスを作成することによる効果を持ちます。 この効果は、Head 関連の転送関数 (HRTF) と呼ばれる高度なテクノロジを使用して実現されます。 HRTF は、人間の頭の形状に基づいて音響キューを生成します。 これらの手掛かりは、リスナーがサウンドの方向とソースを特定するのを支援するだけでなく、リスナーを囲む音響環境の種類も拡張します。</p></td>
</tr>
<tr class="odd">
<td align="left">スピーカー フィル</td>
<td align="left"><p>ほとんどの音楽は2つのチャネルでのみ生成されます。したがって、一般的なオーディオまたはビデオファンのマルチチャンネルオーディオ機器には最適化されません。 したがって、音楽がフロント左およびフロント右の loudspeakers からのみのものである場合は、オーディオエクスペリエンスが最も低くなります。 スピーカーの塗りつぶしは、マルチチャネル場内のセットアップをシミュレートします。 これにより、部屋のすべての loudspeakers で再生されるように、2つのスピーカーでしか聞こえない音楽を、空間人気を強化することができます。</p></td>
</tr>
<tr class="even">
<td align="left">室内音響補正</td>
<td align="left"><p>部屋の修正では、部屋の中央のクッションなど、部屋の特定の場所に対するリスニングエクスペリエンスが最適化されます。これは、遅延、周波数応答、およびゲイン調整の最適な組み合わせを自動的に計算することによって行われます。</p>
<p>部屋の修正機能は、ビデオ画面上の画像とのサウンドをより適切に照合します。デスクトップスピーカーが非標準の場所に配置されている場合にも役立ちます。 部屋の修正処理は、エンドツーエンドの受信側での同様の機能を改善したものです。これは、人間の耳がどのように音を鳴らすかによってアカウントが適切に処理されるためです。</p>
<p>調整はマイクを使用して実行されます。この手順は、ステレオシステムとマルチチャネルシステムの両方で使用できます。 ユーザーはマイクを置き、ルームの応答を測定するウィザードをアクティブ化します。 このウィザードでは、各場内から特別に設計された一連のトーンを順番に再生し、各場内の距離、頻度の応答、およびマイクの場所からの全体的な利益を測定します。</p></td>
</tr>
<tr class="odd">
<td align="left">低音管理</td>
<td align="left"><p>低音管理モードには、転送低音管理とリバース低音管理の2種類があります。</p>
<p><em>転送低音管理</em>は、オーディオデータストリームの低頻度のコンテンツを除外します。 転送低音管理アルゴリズムでは、ディープ低音周波数を処理できるチャネルに応じて、フィルター処理された出力がサブウーファーまたはフロント左およびフロント右の場内チャネルにリダイレクトされます。 この決定は、LRBig フラグの設定に基づいて行います。 LRBig フラグを設定するために、ユーザーはコントロールパネルの [サウンド] アプレットを使用して、[低音管理の設定] ダイアログボックスにアクセスします。 ユーザーがチェックボックスをオンにすると、たとえばフロント右と左側のスピーカーが完全な範囲であることを示し、このアクションによって LRBig フラグが設定されます。 このフラグをクリアするには、チェックボックスをオンにしてオフにします。</p>
<p><em>リバース低音管理</em>は、サブウーファーチャネルから他の出力チャネルに信号を配布します。 シグナルは、LRBig フラグの設定に応じて、すべてのチャネルまたはフロント左およびフロント右チャネルに送られます。 このプロセスでは、サブウーファーの信号を他のチャネルに混在させると、大幅に削減されます。 使用される低音管理モードは、サブウーハーの可用性とメインスピーカーの低音処理機能によって異なります。 Windows では、ユーザーはコントロールパネルの [サウンド] アプレットを使用してこの情報を提供します。</p></td>
</tr>
<tr class="even">
<td align="left">環境効果</td>
<td align="left"><p>環境効果は、実際のオーディオ環境をより正確にシミュレートすることで、オーディオ再生の現実を向上させるために機能します。 さまざまな環境を選択できます。たとえば、"スタジアム" はスポーツスタジアムの acoustics をシミュレートします。</p></td>
</tr>
<tr class="odd">
<td align="left">スピーカーの保護</td>
<td align="left"><p>スピーカーを保護する目的は、スピーカーが Pc のシステムコンポーネントに物理的に害を及ぼすです周波数を抑制することです。 たとえば、一部の物理ハードドライブは、適切な頻度で音を鳴らすことによって破損する場合があります。 基準は、特定の値を超えたときに信号を attenuating して、スピーカーの破損を最小限に抑えることができます。</p></td>
</tr>
<tr class="even">
<td align="left">スピーカーの補正</td>
<td align="left"><p>スピーカーによっては、他の人よりもサウンドを再現する方が優れています。 たとえば、特定のスピーカーが 100 Hz 未満のサウンドを減衰する場合があります。 オーディオドライバーやファームウェア DSP ソリューションには、再生しているスピーカーの特定のパフォーマンス特性に関する知識がある場合があります。また、スピーカーの制限を補うために設計された処理を追加することもできます。 たとえば、100 Hz 未満の周波数にゲインを適用するエンドポイント効果 (EFX) を作成できます。 この効果は、物理的なスピーカーの減衰と組み合わせると、オーディオの忠実性が向上します。</p></td>
</tr>
<tr class="odd">
<td align="left">ダイナミックレンジ圧縮</td>
<td align="left"><p>動的範囲圧縮では、オーディオ信号の動的な範囲を縮小または "圧縮" することによって、静かなサウンドを増幅します。 オーディオ圧縮では、特定のしきい値を下回る音を増幅しますが、音の小さいサウンドは影響を受けません。</p></td>
</tr>
</tbody>
</table>

 

ここに示す \#define ステートメントは、KSMedia .h ヘッダーファイルで使用できます。

DEFAULT

```cpp
#define STATIC_AUDIO_SIGNALPROCESSINGMODE_DEFAULT 0xc18e2f7e, 0x933d, 0x4965, 0xb7, 0xd1, 0x1e, 0xef, 0x22, 0x8d, 0x2a, 0xf3
DEFINE_GUIDSTRUCT("C18E2F7E-933D-4965-B7D1-1EEF228D2AF3", AUDIO_SIGNALPROCESSINGMODE_DEFAULT);
#define AUDIO_SIGNALPROCESSINGMODE_DEFAULT DEFINE_GUIDNAMED(AUDIO_SIGNALPROCESSINGMODE_DEFAULT)
```

素材

```cpp
#define STATIC_AUDIO_SIGNALPROCESSINGMODE_RAW 0x9e90ea20, 0xb493, 0x4fd1, 0xa1, 0xa8, 0x7e, 0x13, 0x61, 0xa9, 0x56, 0xcf
DEFINE_GUIDSTRUCT("9E90EA20-B493-4FD1-A1A8-7E1361A956CF", AUDIO_SIGNALPROCESSINGMODE_RAW);
#define AUDIO_SIGNALPROCESSINGMODE_RAW DEFINE_GUIDNAMED(AUDIO_SIGNALPROCESSINGMODE_RAW)
```

音響エコーのキャンセル

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION 0x6f64adbe, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adbe-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION);
#define AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION)
```

ノイズ抑制

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_NOISE_SUPPRESSION          0x6f64adbf, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adbf-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_NOISE_SUPPRESSION);
#define AUDIO_EFFECT_TYPE_NOISE_SUPPRESSION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_NOISE_SUPPRESSION)
```

自動ゲイン制御

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_AUTOMATIC_GAIN_CONTROL     0x6f64adc0, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc0-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_AUTOMATIC_GAIN_CONTROL);
#define AUDIO_EFFECT_TYPE_AUTOMATIC_GAIN_CONTROL DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_AUTOMATIC_GAIN_CONTROL)
```

BEAMFORMING

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_BEAMFORMING                0x6f64adc1, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc1-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_BEAMFORMING);
#define AUDIO_EFFECT_TYPE_BEAMFORMING DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_BEAMFORMING)
```

定数の削除

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL      0x6f64adc2, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc2-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL);
#define AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_CONSTANT_TONE_REMOVAL)
```

イコライザー

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_EQUALIZER                  0x6f64adc3, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc3-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_EQUALIZER);
#define AUDIO_EFFECT_TYPE_EQUALIZER DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_EQUALIZER)
```

ラウドネスイコライザー

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER         0x6f64adc4, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc4-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER);
#define AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER)
```

低音ブースト

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_BASS_BOOST                 0x6f64adc5, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc5-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_BASS_BOOST);
#define AUDIO_EFFECT_TYPE_BASS_BOOST DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_BASS_BOOST)
```

仮想サラウンド

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_VIRTUAL_SURROUND           0x6f64adc6, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc6-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_VIRTUAL_SURROUND);
#define AUDIO_EFFECT_TYPE_VIRTUAL_SURROUND DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_VIRTUAL_SURROUND)
```

仮想ヘッドホン

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_VIRTUAL_HEADPHONES         0x6f64adc7, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc7-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_VIRTUAL_HEADPHONES);
#define AUDIO_EFFECT_TYPE_VIRTUAL_HEADPHONES DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_VIRTUAL_HEADPHONES)
```

部屋の修正

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_ROOM_CORRECTION            0x6f64adc9, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc9-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_ROOM_CORRECTION);
#define AUDIO_EFFECT_TYPE_ROOM_CORRECTION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_ROOM_CORRECTION)
```

低音管理

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_BASS_MANAGEMENT            0x6f64adca, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adca-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_BASS_MANAGEMENT);
#define AUDIO_EFFECT_TYPE_BASS_MANAGEMENT DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_BASS_MANAGEMENT)
```

環境効果

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_ENVIRONMENTAL_EFFECTS      0x6f64adcb, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adcb-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_ENVIRONMENTAL_EFFECTS);
#define AUDIO_EFFECT_TYPE_ENVIRONMENTAL_EFFECTS DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_ENVIRONMENTAL_EFFECTS)
```

スピーカーの保護

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION         0x6f64adcc, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adcc-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION);
#define AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_SPEAKER_PROTECTION)
```

スピーカーの補正

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION       0x6f64adcd, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adcd-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION);
#define AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION)
```

ダイナミックレンジ圧縮

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION  0x6f64adce, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adce-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION);
#define AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION)
```

 

 




