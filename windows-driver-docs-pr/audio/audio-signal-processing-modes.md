---
title: オーディオ信号の処理モード
description: ドライバーは、サポートされているオーディオ信号の各デバイスの処理モードを宣言します。
ms.assetid: 104275F8-2302-484B-B673-7448CAA1F793
ms.date: 05/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: da363a5b00d061bd18f97d11cf7b37c66c25f985
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464382"
---
# <a name="audio-signal-processing-modes"></a>オーディオ信号の処理モード


ドライバーは、サポートされているオーディオ信号の各デバイスの処理モードを宣言します。

## <a name="span-idavailablesignalprocessingmodesspanspan-idavailablesignalprocessingmodesspanspan-idavailablesignalprocessingmodesspanavailable-signal-processing-modes"></a><span id="Available_Signal_Processing_Modes"></span><span id="available_signal_processing_modes"></span><span id="AVAILABLE_SIGNAL_PROCESSING_MODES"></span>使用可能なシグナル処理モード


オーディオのカテゴリ (アプリケーションで選択) は、オーディオのモード (ドライバーによって定義される) にマップされます。 Windows では、7 つのオーディオ信号処理モードを定義します。 Oem および ihv 側では、どのモードを実装するかを判断できます。 Ihv と Oem が最適なユーザー エクスペリエンスを提供するオーディオ信号を最適化するオーディオ効果を追加する新しいモードを利用することをお勧めします。 モードは、次の表にまとめます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>モード</strong></td>
<td align="left"><strong>レンダー/キャプチャ</strong></td>
<td align="left"><strong>[説明]</strong></td>
</tr>
<tr class="even">
<td align="left">直接</td>
<td align="left">どちらもオン</td>
<td align="left"><p>Raw モードでは、存在しないことをストリームに適用される、信号処理を指定します。</p>
<p>アプリケーションは完全に変更されず、生のストリームを要求し、独自の信号処理を実行できます。</p></td>
</tr>
<tr class="odd">
<td align="left">既定</td>
<td align="left">どちらもオン</td>
<td align="left"><p>このモードでは、既定のオーディオの処理を定義します。</p></td>
</tr>
<tr class="even">
<td align="left">映画 *</td>
<td align="left">Render</td>
<td align="left">ムービー オーディオを再生</td>
</tr>
<tr class="odd">
<td align="left">メディア *</td>
<td align="left">どちらもオン</td>
<td align="left">音楽のオーディオ再生 (多くのメディア ストリームの既定値)</td>
</tr>
<tr class="even">
<td align="left">音声 *</td>
<td align="left">キャプチャ</td>
<td align="left">人間の音声のキャプチャ (Cortana への入力など)</td>
</tr>
<tr class="odd">
<td align="left">通信 *</td>
<td align="left">どちらもオン</td>
<td align="left">VOIP レンダリングとキャプチャ (Skype、Lync など)</td>
</tr>
<tr class="even">
<td align="left">通知 *</td>
<td align="left">Render</td>
<td align="left">着信音、アラーム、アラートなど。</td>
</tr>
</tbody>
</table>

 

\* Windows 10 の新機能です。

## <a name="span-idsignalprocessingmodedriverrequirementsspanspan-idsignalprocessingmodedriverrequirementsspanspan-idsignalprocessingmodedriverrequirementsspansignal-processing-mode-driver-requirements"></a><span id="Signal_Processing_Mode_Driver_Requirements"></span><span id="signal_processing_mode_driver_requirements"></span><span id="SIGNAL_PROCESSING_MODE_DRIVER_REQUIREMENTS"></span>信号処理モードのドライバーの要件


オーディオ デバイス ドライバーをサポートする必要がありますが、少なくとも*Raw*または*既定*モード。 追加モードをサポートするは省略可能です。

可能性の特定のシステムの使用可能なすべてのモードである可能性があります。 ドライバーは、どの信号処理モードをサポートする (つまり APOs の種類からドライバーの一部としてインストールされます) を定義し、それに応じて、OS を通知します。 特定のモードが、ドライバーによってサポートされていない場合、Windows では [次へ] の最適な一致のモードが使用されます。

次の図は、複数のモードをサポートするシステムを示しています。

![複数のオーディオ モード ](images/audio-modes-win-10.png)

## <a name="span-idwindowsaudiostreamcategoriesspanspan-idwindowsaudiostreamcategoriesspanspan-idwindowsaudiostreamcategoriesspanwindows-audio-stream-categories"></a><span id="Windows_Audio_Stream_Categories"></span><span id="windows_audio_stream_categories"></span><span id="WINDOWS_AUDIO_STREAM_CATEGORIES"></span>Windows オーディオ Stream カテゴリ


アプリケーションでは、オーディオ ストリームの使用方法について、システムを通知するために、ストリームを特定のオーディオ ストリームのカテゴリとタグ付けするオプションがあります。 アプリケーションでは、オーディオ ストリームを作成した直後のオーディオの Api を使用して、オーディオのカテゴリを設定できます。 Windows 10 では、9 つのオーディオ ストリームのカテゴリがあります。

|                |                                                                                                       |
|----------------|-------------------------------------------------------------------------------------------------------|
| **カテゴリ**   | **[説明]**                                                                                       |
| ムービー          | ムービー、ビデオのダイアログ ボックス (ForegroundOnlyMedia が置き換えられます)                                              |
| メディア          | メディアの再生 (BackgroundCapableMedia が置き換えられます) の既定のカテゴリ                                 |
| ゲーム チャット      | ユーザー (Windows 10 の新しいカテゴリ) 間のゲーム内の通信                                      |
| 音声認識         | 音声入力 (例: パーソナル アシスタント) と出力 (例: アプリのナビゲーション) (Windows 10 の新しいカテゴリ) |
| Communications | VOIP、リアルタイムのチャット                                                                                  |
| オブジェクト エクスプローラーには         | アラーム、着信音、通知                                                                       |
| サウンド効果  | ビープ音など                                                                                     |
| ゲームのメディア     | ゲームの音楽                                                                                         |
| ゲーム効果   | 車のエンジン音、箇条書きなどをはずむボールです。                                                      |
| その他          | カテゴリ化されていないストリーム                                                                                 |

 

前述のように、(アプリケーションで選択) オーディオのカテゴリは、オーディオのモード (ドライバーによって定義される) にマップされます。 アプリケーションは、10 個のオーディオのカテゴリの 1 つのストリームの各のタグを付けることができます。

アプリケーションでは、オーディオのカテゴリと信号処理モード間のマッピングを変更するオプションはありません。 「オーディオ処理モード」の概念を認識にしているアプリケーションがありません。 そのストリームの各モードが使用されるアウトが見つけられない。

**WASAPI コード サンプル**

WASAPIAudio サンプルを次の WASAPI コードでは、さまざまなオーディオのカテゴリを設定する方法を示します。

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

## <a name="span-idsignalprocessingmodesandeffectsspanspan-idsignalprocessingmodesandeffectsspanspan-idsignalprocessingmodesandeffectsspansignal-processing-modes-and-effects"></a><span id="Signal_Processing_Modes_and_Effects"></span><span id="signal_processing_modes_and_effects"></span><span id="SIGNAL_PROCESSING_MODES_AND_EFFECTS"></span>信号処理モードと影響


Oem 定義の効果がどのようになるか各モードで使用します。 Windows では、オーディオ効果の 17 種類の一覧を定義します。

モードと APOs を関連付ける方法については、次を参照してください。[オーディオ処理オブジェクトを実装する](implementing-audio-processing-objects.md)します。

どのような影響が要求するアプリケーションは RAW または RAW 以外の処理のいずれかの特定のストリームに適用します。 アプリケーションに問い合わせることもできるときに通知の効果または生の処理状態を変更します。 アプリケーションは、通信などの特定のストリーミング カテゴリがある場合、または使用されて、RAW モードだけの場合を判断するこの情報を使用することがあります。 RAW モードにしか使用できない場合、アプリケーションは、追加するための独自のオーディオの処理量を判断できます。

System.Devices.AudioDevice.RawProcessingSupported が true の場合は、アプリケーションではも特定のストリームに「RAW を使用して、」フラグを設定するオプションがあります。 System.Devices.AudioDevice.RawProcessingSupported が false の場合、アプリケーションは「RAW を使用して、」フラグを設定できません。

アプリケーションがあるない数モードが存在する、RAW/非 RAW を除きを可視化します。

アプリケーションでは、処理、オーディオ ハードウェア構成に関係なく最適なオーディオ効果を要求する必要があります。 たとえば、通信と、Windows のバック グラウンド ミュージックの一時停止するようにストリームをタグ付けします。

オーディオ ストリームの静的なカテゴリの詳細については、次を参照してください。 [AudioCategory 列挙](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.media.audiocategory.aspx)と[MediaElement.AudioCategory プロパティ](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.mediaelement.audiocategory.aspx)します。

## <a name="span-idclsidsforsystemeffectsspanspan-idclsidsforsystemeffectsspanspan-idclsidsforsystemeffectsspanclsids-for-system-effects"></a><span id="CLSIDs_for_System_Effects"></span><span id="clsids_for_system_effects"></span><span id="CLSIDS_FOR_SYSTEM_EFFECTS"></span>システムの効果の Clsid


**[FX]\_DISCOVER\_効果\_APO\_CLSID**

これは、アクティブな効果の一覧を取得するドライバーを照会する「プロキシ効果」MsApoFxProxy.dll の CLSID

```cpp
FX_DISCOVER_EFFECTS_APO_CLSID  = "{889C03C8-ABAD-4004-BF0A-BC7BB825E166}"
```

**KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_モード**

KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_モードは、カーネルがストリーミング参照されている特定の属性が、信号処理の mode 属性を識別するための識別子。

\#ここで示すようにステートメントを定義、KSMedia.h ヘッダー ファイルで利用できます。

```cpp
#define STATIC_KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE 0xe1f89eb5, 0x5f46, 0x419b, 0x96, 0x7b, 0xff, 0x67, 0x70, 0xb9, 0x84, 0x1
DEFINE_GUIDSTRUCT("E1F89EB5-5F46-419B-967B-FF6770B98401", KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE);
#define KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE DEFINE_GUIDNAMED(KSATTRIBUTEID_AUDIOSIGNALPROCESSING_MODE)
```

KSATTRIBUTEID\_AUDIOSIGNALPROCESSING\_モード対応のドライバーをでモードを使用して、 [ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)を含む構造体、 [ **KSATTRIBUTE\_一覧**](https://msdn.microsoft.com/library/windows/hardware/mt727894)します。 この一覧では、1 つの要素には、 [ **KSATTRIBUTE**](https://msdn.microsoft.com/library/windows/hardware/ff560987)します。 属性のメンバー、 **KSATTRIBUTE** KSATTRIBUTEID に構造体が設定されている\_AUDIOSIGNALPROCESSING\_モード。

## <a name="span-idaudioeffectsspanspan-idaudioeffectsspanspan-idaudioeffectsspanaudio-effects"></a><span id="Audio_Effects"></span><span id="audio_effects"></span><span id="AUDIO_EFFECTS"></span>オーディオ特殊効果


次のオーディオ効果は、Windows 10 で使用可能な。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">アコースティック エコー キャンセル (AEC)</td>
<td align="left"><p>アコースティック エコー キャンセル (AEC) は、後がオーディオ ストリーム内に存在した後に、エコーを削除することで、オーディオの品質を向上します。</p></td>
</tr>
<tr class="even">
<td align="left">ノイズの抑制 (NS)</td>
<td align="left"><p>ノイズの抑制 (NS) は、ブンブン窓辺、オーディオ ストリーム内に存在する場合などのノイズを抑制します。</p></td>
</tr>
<tr class="odd">
<td align="left">自動ゲイン制御 (AGC)</td>
<td align="left"><p>自動ゲイン制御 (AGC) には、入力信号に amplitude のバリエーションに関係なく、その出力の制御シグナル amplitude を提供する設計されています。 平均やピーク時は、信号レベルを使用して、入出力のゲインが多様な入力信号のレベルでも、出力の安定したレベルを有効にすると、適切な値を動的に調整して出力します。</p></td>
</tr>
<tr class="even">
<td align="left">(BF) を形成ビーム</td>
<td align="left"><p>ビーム形成 (BF) は、シグナル処理方向シグナル送信または受信に使用される手法です。 これは、破壊的な障害が発生する他のユーザーに特定の角度で信号で建設的な障害が発生するように段階的配列内の要素を組み合わせることによって実現されます。 全方向受信/送信と比較して向上は、受信/送信利益 (または損失) と呼ばれます。</p></td>
</tr>
<tr class="odd">
<td align="left">定数のトーンの削除</td>
<td align="left"><p>定数のトーンの削除は、テープのヒスノイズ、電気ファン業者などの定数のバック グラウンド ノイズの減衰に使用されます。</p></td>
</tr>
<tr class="even">
<td align="left">イコライザー</td>
<td align="left"><p>線形のフィルターを使用して、オーディオ システムの周波数の応答を変更するには、イコライザーの効果を使用します。 これにより、ブースト、高音または低音の設定と同様に、信号のさまざまな部分です。</p></td>
</tr>
<tr class="odd">
<td align="left">ラウドネス イコライザー</td>
<td align="left"><p>ラウドネス イコライザーの効果は、大きくより静かサウンドが平均ラウドネスのレベルに近い方になるようにオーディオ出力を平準化によって認識されるボリュームの相違点を削減します。</p></td>
</tr>
<tr class="even">
<td align="left">低音ブースト</td>
<td align="left"><p>低音機能が制限付きのスピーカーがあるラップトップなどのシステムで低音スピーカーでサポートされる周波数の範囲で応答を混ぜてオーディオの知覚品質を向上させることがあります。 音は、中間低音の範囲のゲインを増やすことで非常に小さなスピーカーのモバイル デバイスで音を向上します。</p></td>
</tr>
<tr class="odd">
<td align="left">仮想サラウンド</td>
<td align="left"><p>仮想サラウンドでは、デジタルの単純なメソッドを使用して、マルチ チャンネルの信号を 2 つのチャネルに結合します。 これは、ほとんどの最新オーディオ受信機で利用できる Pro ロジック デコーダーを使用して、元のマルチ チャンネル信号に復元する変換された信号を許可する方法で行います。 仮想サラウンドでは、2 チャンネルのサウンドのハードウェアおよびサラウンド サウンドの拡張機能のメカニズムである受信者を持つシステムに最適です。</p></td>
</tr>
<tr class="even">
<td align="left">仮想ヘッドホン</td>
<td align="left"><p>仮想サラウンド サウンドは、前からにサイド バイ サイドの後ろにサウンドを区別するためにヘッドホンを着用はユーザーを許可します。 これは、サウンドをローカライズし、サウンド フィールドに統合したり、脳に役立つ空間のキュー送信することで行います。 "外部-、-head"をリッスンしているエクスペリエンスを作成、ヘッドホンを越えるように、サウンドの操作の効果があります。 この効果は、Head 関連 Transfer Functions (HRTF) と呼ばれる高度なテクノロジを使用して実現されます。 HRTF では、人間の頭の図形に基づく音響的な手掛かりが生成されます。 方向を検索するリスナーだけでなく手掛かりしています。 とサウンドのソースは、リスナーを囲む音響環境の種類も向上します。</p></td>
</tr>
<tr class="odd">
<td align="left">スピーカー フィル</td>
<td align="left"><p>音楽の大部分は、チャネルを 2 つだけが発生し、一般的なオーディオまたはビデオの愛好家のマルチ チャンネル オーディオ機器の最適化されていないため。 前面左右 loudspeakers のみから音楽ことは、あまり理想的オーディオ エクスペリエンスです。 スピーカー フィルは、マルチ チャネルのスピーカーのセットアップをシミュレートします。 これにより、すべての空間感覚の強化、部屋に loudspeakers で再生できるように 2 つだけのスピーカーでが聞こえるそれ以外の場合は音楽ができます。</p></td>
</tr>
<tr class="even">
<td align="left">室内音響補正</td>
<td align="left"><p>ルーム コレクションでは、待ち時間、周波数の応答の最適な組み合わせを自動的に計算することで、リッスンしている、部屋は、ソファ center クッションなどの特定の場所のエクスペリエンスを最適化し、ゲイン調整します。</p>
<p>ルームの修正機能はよりサウンド、ビデオ画面のイメージに一致して、デスクトップのスピーカーの非標準の場所に配置する場所の場合にも役立ちます。 ルーム修正処理はハイエンドの受信側で同様の機能のためにより人間の耳がサウンドを処理する方法のアカウントします。</p>
<p>調整は、マイクのヘルプで実行され、プロシージャをステレオとマルチ チャネルの両方のシステムで使用できます。 ユーザーは、ユーザーが配置しようとした、マイクを配置し、ルームの応答を測定するウィザードをアクティブにし。 ウィザードでは、さらに、一連の各スピーカーから特別に設計されたトーンを再生し、距離、周波数の応答、および各スピーカー、マイクの場所からの全体的な利益を測定します。</p></td>
</tr>
<tr class="odd">
<td align="left">低音管理</td>
<td align="left"><p>2 つのベースの管理モード: ベースの管理を転送し、低音の管理を反転します。</p>
<p><em>低音の管理を転送</em>オーディオ データ ストリームの頻度の低いコンテンツをフィルター処理します。 前方の低音管理アルゴリズムは、サブウーファー、または詳細な音の周波数を処理できるチャネルによって、前面左右のスピーカー チャネルに絞り込まれた出力をリダイレクトします。 この決定は、LRBig フラグの設定に基づきます。 LRBig フラグを設定するには、ユーザーは、コントロール パネルの [低音管理設定] ダイアログ ボックスにアクセスするのにサウンド アプレットを使用します。 ユーザーが示すには、たとえば、前面左右のスピーカーは完全な範囲をこのアクションは LRBig フラグを設定する チェック ボックスを選択します。 このフラグをクリアするには、チェック ボックスをオフをクリックします。</p>
<p><em>低音の管理を反転</em>を他の出力チャネル サブウーファー チャンネルの信号を配布します。 信号が LRBig フラグの設定に応じて、すべてのチャネルまたは左フロントのいずれかに有向とフロント右側のチャンネルになります。 このプロセスは、サブウーファー シグナル、他のチャネルに混在している場合に大幅な向上削減を使用します。 使用されるベースの管理モードは、サブウーファーの可用性、およびメインのスピーカーの音処理機能に依存します。 、Windows では、ユーザーは、コントロール パネルの サウンド アプレットを使用してこの情報を提供します。</p></td>
</tr>
<tr class="even">
<td align="left">環境からの影響</td>
<td align="left"><p>環境の効果より正確に模したの実際のオーディオ環境でのオーディオ再生の現実を強化する機能します。 選択できるさまざまな環境がいくつか、たとえば"stadium"がスポーツ スタジアムの騒音をシミュレートします。</p></td>
</tr>
<tr class="odd">
<td align="left">スピーカーの保護</td>
<td align="left"><p>スピーカーの保護の目的は、Pc のシステム コンポーネントのいずれかに物理的に損なわを実行するスピーカーを原因となる共振の周波数を抑制するのには。 たとえば、いくつかの物理ハード ドライブの場合は、適切な頻度で大きなサウンドを再生して破損していることができます。 また、スピーカー保護では、特定の値を超えたときに、信号の減衰でスピーカーへの損害を最小限に抑えます。</p></td>
</tr>
<tr class="even">
<td align="left">講演者報酬</td>
<td align="left"><p>一部のスピーカーでは、他よりもサウンドの再生に優れています。 たとえば、特定の speaker では、100 Hz の下のサウンドを減衰可能性があります。 オーディオ ドライバーとファームウェア DSP ソリューションは、再生、スピーカーの特定のパフォーマンス特性に関する知識を持っているし、講演者の制限については、補正するために設計されています。 処理を追加することができます。 たとえば、エンドポイントの効果 (EFX) 作成でした 100 Hz 未満の周波数に利益を適用します。 物理のスピーカーの減衰と組み合わせたときに、この効果は、強化されたオーディオの忠実性の結果します。</p></td>
</tr>
<tr class="odd">
<td align="left">ダイナミック レンジ圧縮</td>
<td align="left"><p>ダイナミック レンジ圧縮では、サウンドを非表示を増幅して縮小またはオーディオ信号のダイナミック レンジを「圧縮」。 オーディオの圧縮は、サウンドの音量が影響を受けていないまま、特定のしきい値を下回るは非表示のサウンドを増幅します。</p></td>
</tr>
</tbody>
</table>

 

\#ここで示すようにステートメントを定義、KSMedia.h ヘッダー ファイルで利用できます。

DEFAULT

```cpp
#define STATIC_AUDIO_SIGNALPROCESSINGMODE_DEFAULT 0xc18e2f7e, 0x933d, 0x4965, 0xb7, 0xd1, 0x1e, 0xef, 0x22, 0x8d, 0x2a, 0xf3
DEFINE_GUIDSTRUCT("C18E2F7E-933D-4965-B7D1-1EEF228D2AF3", AUDIO_SIGNALPROCESSINGMODE_DEFAULT);
#define AUDIO_SIGNALPROCESSINGMODE_DEFAULT DEFINE_GUIDNAMED(AUDIO_SIGNALPROCESSINGMODE_DEFAULT)
```

生

```cpp
#define STATIC_AUDIO_SIGNALPROCESSINGMODE_RAW 0x9e90ea20, 0xb493, 0x4fd1, 0xa1, 0xa8, 0x7e, 0x13, 0x61, 0xa9, 0x56, 0xcf
DEFINE_GUIDSTRUCT("9E90EA20-B493-4FD1-A1A8-7E1361A956CF", AUDIO_SIGNALPROCESSINGMODE_RAW);
#define AUDIO_SIGNALPROCESSINGMODE_RAW DEFINE_GUIDNAMED(AUDIO_SIGNALPROCESSINGMODE_RAW)
```

アコースティック エコー キャンセル

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION 0x6f64adbe, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adbe-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION);
#define AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_ACOUSTIC_ECHO_CANCELLATION)
```

ノイズの抑制

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

定数のトーンの削除

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

ラウドネス イコライザー

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER         0x6f64adc4, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc4-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER);
#define AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_LOUDNESS_EQUALIZER)
```

低音ブーストします。

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

ルーム コレクション

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_ROOM_CORRECTION            0x6f64adc9, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adc9-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_ROOM_CORRECTION);
#define AUDIO_EFFECT_TYPE_ROOM_CORRECTION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_ROOM_CORRECTION)
```

低音の管理

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_BASS_MANAGEMENT            0x6f64adca, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adca-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_BASS_MANAGEMENT);
#define AUDIO_EFFECT_TYPE_BASS_MANAGEMENT DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_BASS_MANAGEMENT)
```

環境からの影響

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

講演者報酬

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION       0x6f64adcd, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adcd-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION);
#define AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_SPEAKER_COMPENSATION)
```

ダイナミック レンジ圧縮

```cpp
#define STATIC_AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION  0x6f64adce, 0x8211, 0x11e2, 0x8c, 0x70, 0x2c, 0x27, 0xd7, 0xf0, 0x01, 0xfa
DEFINE_GUIDSTRUCT("6f64adce-8211-11e2-8c70-2c27d7f001fa", AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION);
#define AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION DEFINE_GUIDNAMED(AUDIO_EFFECT_TYPE_DYNAMIC_RANGE_COMPRESSION)
```

 

 




