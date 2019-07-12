---
title: 音声のアクティブ化
description: Cortana、音声のプラットフォームは、音声のすべての電源を使用する Windows は、Cortana、ディクテーションなどの Windows 10 で発生します。
ms.assetid: 0684EF32-AA76-418B-9027-1C067A8140E3
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4e2cb2dfdd00df097ed3af6bbba727e93658bd22
ms.sourcegitcommit: 9bec15f7c262f04160f8e8266f4530a15e0e201c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843190"
---
# <a name="voice-activation"></a>音声のアクティブ化

Cortana、パーソナル アシスタントのテクノロジが 2013年で、Microsoft BUILD Developer Conference で最初に説明します。 Windows の音声のプラットフォームには、Cortana、ディクテーションなどの Windows 10 でのエクスペリエンス、音声のすべての電源を使用します。 音声をアクティブ化は、コルタナさん」- 特定の語句を言うことにより、さまざまなデバイスの電源の状態からの音声認識エンジンを起動できる機能です。 音声のライセンス認証テクノロジをサポートするハードウェアを作成するには、このトピックの情報を確認します。

**注:**  
音声のアクティブ化の実装は重要なプロジェクトと SoC ベンダーによって完了したタスク。 Oem は、音声をアクティブ化の SoC の実装について、SoC、ベンダーにお問い合わせくださいことができます。


## <a name="span-idcortanaenduserexperiencecortana-end-user-experience"></a><span id="cortana_end_user_experience">Cortana のエンド ユーザー エクスペリエンス


Windows で利用できる音声の相互作用エクスペリエンスを理解するには、これらのトピックを確認します。

|                                                                                                   |                                                                       |
|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| **トピック**                                                                                         | **説明**                                                       |
| [Cortana とは何ですか。](https://support.microsoft.com/help/17214/cortana-what-is)      | 提供し、Cortana の概要と使用状況の方向                 |
| [Cortana あなた次第します。](https://support.microsoft.com/help/17178/windows-10-make-cortana-yours) | Cortana の設定 画面で使用できるカスタマイズをについて説明します。 |



## <a name="span-idintroductiontoheycortanavoiceactivationandlearnmyvoicespanintroduction-to-hey-cortana-voice-activation-and-learn-my-voice"></a><span id="introduction_to__hey_cortana__voice_activation_and__learn_my_voice_"></span>コルタナさん」音声をアクティブ化と「自分の音声をについて説明します」の概要


**"こんにちは Cortana"アクティブ化を音声**

コルタナさん」音声アクティベーション (VA) 機能では、自分の音声を使用して自分のアクティブなコンテキストを使用して、(つまり、現在にあるものの画面) の外部での Cortana エクスペリエンスを迅速に情報交換することができます。 ユーザーは、多くの場合、すぐにデバイスにアクセスするエクスペリエンスを物理的にタッチをやり取りしなくてもできるようにします。 電話ユーザーが、車の運転し、可能性があります、注意と手に従事しています、車両の動作します。 Xbox のユーザーの期日を検索し、コント ローラーを接続したくないことが考えられます。 PC のユーザーのことが考えられますエクスペリエンスへの迅速なアクセス、キッチンでコンピューターなどの複数のマウス、タッチやキーボードの操作を実行する必要はありません。

音声をアクティブ化は、定義済みのキーの語句または「アクティブ化句」を使用して常にリッスンの音声入力を提供します。 キー フレーズを段階的なコマンドとして (コルタナさん」) を単独で発音またはなどの音声の操作を続けて可能性があります"Hey の Cortana が次の会議ですか?"、コマンドを連結します。

用語*キーワード検出*、ハードウェアまたはソフトウェアのいずれかによって、キーワードの検出について説明します。

*キーワードのみ*アクティブ化は、Cortana のキーワードのみを言ったときに発生します。、Cortana が開始され、リッスン モードに入ったことを示す、EarCon サウンドを再生します。

A*コマンドを連結*キーワードの直後のコマンドを発行の機能について説明します (のような"Hey Cortana、John を呼び出す") (起動されていない) 場合に開始できるほか、(John から電話を開始) のコマンドは、Cortana があるとします。

この図のチェーンとキーワードの唯一のアクティブ化します。

![チェーンとキーワードのアクティブ化がオーディオのバッファーを示す図しシーケンスを時刻](images/audio-chained-keyword-activation.png)

Microsoft は、OS 既定キーワード spotter (ソフトウェア キーワード spotter) ハードウェア キーワード検出の品質を保証して、ハードウェアのキーワードの検出が存在しないか利用できない場合 Hey Cortana エクスペリエンスを提供するために使用を提供します。 

**「自分の音声の学習」機能**

「自分の音声を説明します」機能は、自分独自の音声を認識する Cortana のトレーニングにユーザーを使用できます。 これをクリックすると、ユーザーによって行われます*コルタナさん」と言った方法について説明します。* [Cortana] 画面で設定します。 ユーザーは、十分なさまざまなユーザーの声の一意の属性を識別する音声のパターンを提供する 6 つの慎重に選択した句を繰り返します。

![hw キーワード spotter のデスクトップの設定を cortana が音声でスリープ解除します。](images/audio-voice-activation-settings-2017.png)

音声とアクティブ化は「自分の音声をについて説明します」と組み合わせて、2 つのアルゴリズムが協力して、ライセンス認証の場合は false を削減します。 これは、貴重なミーティングの部屋シナリオでは、1 人のユーザーが」「コルタナさんいっぱいの部屋でデバイスを表示します。

音声をアクティブ化のキー フレーズが検出された場合に反応するキーワード spotter (KWS) で電源が。 低電源状態からデバイスをウェイクするための KWS の場合は、ソリューションは、Wake on 音声 (WoV) と呼ばれます。 詳細については、次を参照してください。 [Wake on 音声](#wake_on_voice)します。


## <a name="span-idglossaryoftermsspanspan-idglossaryoftermsspanglossary-of-terms"></a><span id="glossary_of_terms"></span><span id="Glossary_Of_Terms"></span>用語集

この用語集は、音声をアクティブ化に関連する用語をまとめたものです。

|                      |                                                                                                                                                           |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ステージングされたコマンド        | 以下に例を示します。こんにちは Cortana < 一時停止、earcon 待つ > 天気とは何ですか? これとも呼ば「2 ショット コマンド」または「キーワードのみ」 |
|チェーンされたコマンド        | 以下に例を示します。こんにちは Cortana、天気とは何ですか? これとも呼ば"ワンショット"コマンド |
| 音声のアクティブ化      | 定義済みのライセンス認証キーフレーズのキーワードの検出を提供するシナリオです。 たとえば、コルタナさん」は、Microsoft の音声のライセンス認証シナリオです。 |
|WoV                    | ウェイク アップに-ボイス – 低電力状態では、オフの画面から、画面の完全な電源状態に音声をアクティブ化を実現するテクノロジ。 |
|最新のスタンバイから WoV| ウェイク アップに-ボイス オフの状態の最新のスタンバイ (S0ix) 画面から (S0) の完全な電源状態で、画面にします。 |
|モダン スタンバイ |Windows 低電力アイドル インフラストラクチャ - に接続されているスタンバイ (CS) で Windows 10 の後継です。 最新のスタンバイ状態の最初の状態は、画面がオフの場合です。 最下位のスリープ状態は、DRIPS/回復性の場合です。 詳細については、次を参照してください[最新スタンバイ。](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)   |
|KWS                    |キーワード spotter – コルタナさん」の検出を提供するアルゴリズム |
| SW KWS                |ソフトウェア キーワード spotter – (CPU) のホストで実行されている KWS の実装。 「コルタナさん、SW KWS は Windows の一部として含まれています。 |
| HW KWS                | ハードウェア オフロード キーワード spotter – 実行 KWS の実装は、ハードウェアのオフロード。 |
|バッファーをバーストします。           | KWS 検出をトリガーしたすべてのオーディオが含まれるように 'がいっぱいになりましたを'、KWS 検出が発生した場合にできる PCM データを格納するために使用する循環バッファー。 |
|キーワード Detector OEM アダプター |Windows と Cortana のスタックと通信する WoV 対応ハードウェアをできるようにするドライバー レベル shim です。 |
|モデル | 音響モデルのデータ ファイルは KWS アルゴリズムで使用します。 データ ファイルは静的です。 モデルをローカライズすると、ロケールごとに 1 つ。|

## <a name="span-idimplementingvoiceactivationspanspan-idimplementingvoiceactivationspanspan-idimplementingvoiceactivationspanintegrating-a-hardware-keyword-spotter"></a><span id="Implementing_Voice_Activation"></span><span id="implementing_voice_activation"></span><span id="IMPLEMENTING_VOICE_ACTIVATION"></span>ハードウェアのキーワード Spotter の統合

ハードウェア キーワード spotter (HW KWS) を実装するには、SoC ベンダーは、次のタスクを完了する必要があります。

-   このトピックの後半で説明されている SYSVAD サンプルに基づくカスタム キーワード検出機能を作成します。 説明されている、COM DLL でこれらのメソッドを実装する[キーワード Detector OEM アダプター インターフェイス](#keyword_detector)します。
-   説明されている WAVE RT 拡張機能の実装[WAVERT 強化](#wavert_enhancements)します。
-   キーワードの検出に使用される任意のカスタム APOs を記述する INF ファイルのエントリを提供します。
    -   [鍵\_FX\_KeywordDetector\_StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-streameffectclsid)
    -   [PKEY\_FX\_KeywordDetector\_ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-modeeffectclsid)
    -   [鍵\_FX\_KeywordDetector\_EndpointEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-endpointeffectclsid)
    -   [鍵\_SFX\_KeywordDetector\_ProcessingModes\_サポート\_の\_ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-keyworddetector-processingmodes-supported-for-streaming)
    -   [鍵\_MFX\_KeywordDetector\_ProcessingModes\_サポート\_の\_ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-keyworddetector-processingmodes-supported-for-streaming)
    -   [鍵\_EFX\_KeywordDetector\_ProcessingModes\_サポート\_の\_ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-efx-keyworddetector-processingmodes-supported-for-streaming)
-   ハードウェアの推奨事項を確認し、テストのガイダンス[オーディオ デバイスの推奨事項](https://docs.microsoft.com/windows-hardware/design/component-guidelines/audio)します。 このトピックでは、ガイダンスおよび設計と開発のオーディオ入力デバイスが Microsoft の音声のプラットフォームで使用するための推奨事項を提供します。
-   サポートは、ステージングし、コマンドを連結します。
-   サポートされている Cortana ロケールのコルタナさん」をサポートします。 
-   APOs (オーディオ処理オブジェクト) には、次の効果を提供する必要があります。 
    -   AEC
    -   AGC
    -   NS
-   MFX APO、音声処理モードの効果を報告する必要があります。
-   APO MFX として形式変換を実行できます。   
-   APO には、次の形式を出力する必要があります。 
    -   16 kHz、mono、浮動小数点数。
-   必要に応じてオーディオ キャプチャ プロセスを強化するために、カスタム画像をデザインします。 詳細については、次を参照してください。 [Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)します。

キーワードのハードウェア オフロード spotter (HW KWS) WoV 要件
- HW KWS WoV は、S0 の操作の状態と S0 スリープ状態とも呼ばれる最新スタンバイ中にサポートされます。  
- HW KWS WoV S3 はサポートされていません。  

HW KWS の AEC の要件

- Windows バージョン 1709
    - S0 の HW KWS WoV をサポートするためにスリープ状態 (最新スタンバイ、AEC) は必要ありません。  
    - Windows バージョン 1709 では、S0 作業状態の HW KWS WoV はサポートされていません。

- Windows バージョン 1803 
    - S0 作業状態の HW KWS WoV がサポートされています。
    - HW KWS WoV S0 作業の状態を有効にするには、APO が AEC をサポートする必要があります。


## <a name="span-idsamplecodeoverviewspansample-code-overview"></a><span id="sample_code_overview"></span>サンプル コードの概要


オーディオ ドライバー SYSVAD 仮想オーディオ アダプター サンプルの一部として、GitHub の音声をアクティブ化を実装するためのサンプル コードがあります。 開始点としてこのコードを使用することをお勧めします。 コードは、この場所で使用できます。

<https://github.com/Microsoft/Windows-driver-samples/blob/master/audio/sysvad/>

SYSVAD サンプル オーディオ ドライバーの詳細については、次を参照してください。[サンプル オーディオ ドライバー](sample-audio-drivers.md)します。

## <a name="span-idkeywordrecognitionsysteminformationspankeyword-recognition-system-information"></a><span id="keyword_recognition_system_information"></span>キーワード認識システム情報


**音声のライセンス認証オーディオ スタックのサポート**

音声をアクティブ化を有効にするため、オーディオ スタックの外部インターフェイスは、音声のプラットフォームとオーディオ ドライバーの通信パイプラインとして機能します。 外部インターフェイスは、3 つの部分に分割されます。

-   *キーワード detector デバイス ドライバー インターフェイス (DDI)* します。 キーワード detector デバイス ドライバー インターフェイスは取り組ま HW キーワード Spotter (KWS) の構成と責任を負います。  検出イベントのシステムに通知する、ドライバーによっても使用されます。
-   *キーワード Detector OEM アダプター DLL*します。 この DLL は、キーワードの検出を支援するために、OS によって使用されるドライバーの特定非透過データを調整する COM インターフェイスを実装します。
-   *ストリーミングの機能強化 WaveRT*します。 拡張機能は、バーストのストリーム バッファー内のオーディオ データにキーワード検出からのオーディオ ドライバーを有効にします。

**オーディオのエンドポイントのプロパティ**

オーディオのエンドポイントのグラフ作成が正常に行われます。 グラフはリアルタイム キャプチャよりも高速に処理するために準備されます。 キャプチャされたバッファーのタイムスタンプはまま true です。 具体的には、タイムスタンプは、過去と、バッファー内でキャプチャされ、ここで「バースト」するデータを正しく反映されます。

**操作の理論を概説します。**

ドライバーは、通常どおりそのキャプチャ デバイスのフィルターを KS を公開します。 このフィルターは、いくつかの KS プロパティと構成の有効化および検出イベントを通知する KS イベントをサポートします。 フィルターには、キーワードの spotter (KWS) ピンとして識別される、追加の pin ファクトリも含まれています。 この pin は、キーワード spotter からオーディオをストリーミングに使用されます。

次のプロパティです。

-   サポートされているキーワードの種類 - [ **KSPROPERTY\_SOUNDDETECTOR\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-patterns)します。 このプロパティは、構成を検出するキーワードにオペレーティング システムによって設定されます。
-   キーワードの一覧パターンの Guid - [ **KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-supportedpatterns)します。 このプロパティを使用して、サポートされているパターンの種類を識別する Guid のリストを取得できます。
-   武装 - [ **KSPROPERTY\_SOUNDDETECTOR\_故障**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-armed)します。 この読み取り/書き込みプロパティは、検出機能が作動するかどうかを示すブール値を単に状態です。 OS では、キーワードの検出機能を使用してこれを設定します。 OS には、これを改ざんをクリアできます。 これは、ドライバーが自動的にクリア キーワードが検出されたパターンのキーワードを設定するとも後。 (OS する必要があります rearm。)
-   -結果と一致する[ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-matchresult)します。 この読み取りプロパティは、検出が行われた後に、結果データを保持します。

キーワードが検出されたときに発生するイベントは、 [ **KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-sounddetector-matchdetected)イベント。

**操作のシーケンス**

*システムの起動*

1. OS では、その形式のキーワードがあることを確認するキーワードがサポートされている型を読み取ります。
2. OS は、検出機能の状態変更イベントを登録します。
3. OS は、キーワードのパターンを設定します。
4. OS は、検出機能を準備します。

*KS イベントを受け取る*

1. ドライバーは disarms、検出機能です。
2. OS は、キーワードの検出機能の状態を読み取り、返されたデータを解析し、どのパターンが検出されましたを決定します。
3. OS は rearms、検出機能です。

**内部のドライバーとハードウェアの操作**

検出機能を活用すると、中に、ハードウェアを継続的にキャプチャおよび小規模な FIFO バッファーにオーディオ データをバッファリングすることができます。 (この FIFO バッファーのサイズは、このドキュメントでは、外部の要件によって決まりますが通常いくつかの秒の 1/10 の単位があります)。検出アルゴリズムは、このバッファーからストリーミング データで動作します。 ドライバーとハードウェアの設計がいるにも腕を操作はありません、ドライバーとハードウェア"application"プロセッサに割り込みとキーワードが検出されるまでです。 これにより、他のアクティビティがない場合は、低電力状態を接続するシステムです。

キーワードが検出されると、ハードウェア割り込みを生成します。 割り込みを処理するドライバーを待っている間には、バッファーのようになるためデータ キーワードがバッファリングの制限内では、失われた後にオーディオをキャプチャする、ハードウェアが続行されます。

**キーワードのタイムスタンプ**

キーワードを検出すると、音声のすべてのアクティブ化ソリューションのすべてのキーワードの開始前に 250 ミリ秒を含む、話し言葉のキーワードをバッファーする必要があります。 オーディオ ドライバーには、先頭と末尾のストリーム内のキー フレーズを識別するタイムスタンプを提供する必要があります。

キーワードの開始/終了タイムスタンプをサポートするために DSP ソフトウェアは、内部的にタイムスタンプ イベントの DSP クロックに基づく必要があります。 キーワードが検出されると、DSP ソフトウェア KS イベントを準備するドライバーと対話します。 ドライバーと DSP ソフトウェアは、Windows パフォーマンス カウンターの値に DSP タイムスタンプをマップする必要があります。 このメソッドは、ハードウェアの設計に固有です。 Current パフォーマンス カウンタの読み取り、DSP の現在のタイムスタンプのクエリ、もう一度、現在のパフォーマンス カウンターを読み取るし、パフォーマンス カウンターと DSP 時刻間の相関関係を推定するドライバーが、ソリューションの 1 つです。 相関関係の指定されたドライバーをマップできますキーワード DSP タイムスタンプ Windows パフォーマンス カウンターのタイムスタンプ。


## <a name="span-idkeyworddetectorspankeyword-detector-oem-adapter-interface"></a><span id="keyword_detector"></span>キーワード Detector OEM アダプター インターフェイス

計算やを使ってオーディオ ドライバーに読み取りし、書き込みは非透過的なデータを解析しやすく、OS およびドライバーの間の媒介として機能する COM オブジェクトの実装を提供する OEM [ **KSPROPERTY\_SOUNDDETECTOR\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-patterns)と[ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-matchresult)します。

COM オブジェクトの CLSID は検出器パターンの種類によって返される GUID、 [ **KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-supportedpatterns)します。 OS の呼び出しパターンを渡して CoCreateInstance キーワード パターンの種類と互換性が、オブジェクトの IKeywordDetectorOemAdapter インターフェイスのメソッドを呼び出して適切な COM オブジェクトをインスタンス化する GUID を入力します。

**COM スレッド処理モデルの要件**

OEM の実装には、COM スレッド モデルのいずれかを選択できます。

**IKeywordDetectorOemAdapter**

インターフェイスのデザインは、オブジェクトの実装をステートレスに保持しようとします。 つまり、実装する必要がありますは必要ありませんメソッド呼び出しの間に格納される状態。 実際には、可能性の高い内部の C++ クラスには、一般に、COM オブジェクトを実装するために必要なもの以外のすべてのメンバー変数は必要ありません。

**メソッド**

次のメソッドを実装します。

-   [**IKeywordDetectorOemAdapter::BuildArmingPatternData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-buildarmingpatterndata)
-   [**IKeywordDetectorOemAdapter::ComputeAndAddUserModelData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-computeandaddusermodeldata)
-   [**IKeywordDetectorOemAdapter::GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-getcapabilities)
-   [**IKeywordDetectorOemAdapter::ParseDetectionResultData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-parsedetectionresultdata)
-   [**IKeywordDetectorOemAdapter::VerifyUserKeyword**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-verifyuserkeyword)

**KEYWORDID**

[ **KEYWORDID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/ne-keyworddetectoroemadapter-__midl_ikeyworddetectoroemadapter_0002)列挙体は、キーワードのフレーズのテキスト/関数を識別し、Windows 生体認証サービス アダプターにも使用します。 詳細については、次を参照してください[生体認証フレームワークの概要 - 基本的なプラットフォーム コンポーネント。](https://docs.microsoft.com/windows/desktop/SecBioMet/biometric-framework-overview)

```cpp
typedef enum  { 
  KwInvalid              = 0,
  KwHeyCortana           = 1,
  KwSelect               = 2
} KEYWORDID;
```

**KEYWORDSELECTOR**

[ **KEYWORDSELECTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/ns-keyworddetectoroemadapter-__midl_ikeyworddetectoroemadapter_0003)構造体は、一連の Id を一意に特定のキーワードおよび言語を選択します。

```cpp
typedef struct
{
    KEYWORDID KeywordId;
    LANGID LangId;
} KEYWORDSELECTOR;
```

**モデル データの処理**

*静的なユーザーの独立したモデル*-OEM DLL には通常製 DLL に含まれている別のデータ ファイルまたは DLL に静的なユーザー依存しないモデル データが含まれます。 Id が GetCapabilities ルーチンによって返される、サポートされているキーワードのセットは、このデータによって異なります。 たとえば、KwHeyCortana がサポートされているキーワード GetCapabilities から返された Id の一覧に含まれている場合、静的なユーザーの独立したモデル データが含まれますデータ コルタナさん」(またはその翻訳) のサポートされているすべての言語。

*動的なユーザー依存モデル*-IStream はランダム アクセス ストレージ モデルを提供します。 OS は、IKeywordDetectorOemAdapter インターフェイスでメソッドの多くに IStream インターフェイス ポインターを渡します。 OS は、最大 1 MB のデータの適切なストレージに IStream 実装をバックアップします。

このストレージ内のデータの構造とコンテンツは、OEM によって定義されます。 使用目的は、計算、または OEM DLL によって取得された、ユーザー依存モデル データの永続的なストレージです。

ユーザーが、キーワードをトレーニングしない場合は特に、OS は、空 istream インターフェイスのメソッドを呼び出すことができます。 OS は、ユーザーごとに個別の IStream ストレージを作成します。 つまり、指定された IStream では、1 つだけのユーザーのモデル データが格納されます。

OEM の DLL の開発者は、独立したユーザーを管理する方法とユーザー依存データを決定します。 ただし、任意の場所、IStream 外のユーザー データは保存しないでください必要があります。 1 つの可能なデザインの OEM の DLL は、IStream と現在のメソッドのパラメーターに応じて静的なユーザーの独立したデータにアクセスするを切り替える内部的にします。 別の設計は可能性があります各メソッド呼び出しの開始時 IStream を確認し、IStream にいない場合は静的なユーザーの独立したデータが存在すると、すべてのモデル データに対して IStream のみにアクセスするメソッドの残りの部分の許可を追加します。

## <a name="span-idtrainingandoperationaudioprocessingspanspan-idtrainingandoperationaudioprocessingspanspan-idtrainingandoperationaudioprocessingspantraining-and-operation-audio-processing"></a><span id="Training_and_Operation_Audio_Processing"></span><span id="training_and_operation_audio_processing"></span><span id="TRAINING_AND_OPERATION_AUDIO_PROCESSING"></span>トレーニングとオーディオの処理の操作


前述のように、オーディオ ストリームが使用可能な豊富な発音で完全な文トレーニング UI フローになります。 各文に個別に渡される[ **IKeywordDetectorOemAdapter::VerifyUserKeyword** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-verifyuserkeyword)予想されるキーワードを含みが許容可能な品質を確認します。 すべての文は収集し、UI で確認した後はすべて渡される 1 つの呼び出しで[ **IKeywordDetectorOemAdapter::ComputeAndAddUserModelData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-computeandaddusermodeldata)します。

オーディオは、音声のアクティブ化のトレーニング用の独自の方法で処理されます。 次の表は、音声のアクティブ化のトレーニングと通常の音声認識の使用量の違いをまとめたものです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><strong>ボイスのトレーニング</strong></td>
<td align="left"><strong>音声認識</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>モード</strong></td>
<td align="left">直接</td>
<td align="left">生または音声</td>
</tr>
<tr class="odd">
<td align="left"><strong>ピン留めします。</strong></td>
<td align="left">標準</td>
<td align="left">KWS</td>
</tr>
<tr class="even">
<td align="left"><strong>オーディオの形式</strong></td>
<td align="left">32 ビット浮動小数点 (種類 = オーディオ、サブタイプ IEEE_FLOAT、サンプリング レートを = 16 kHz、bits を = = 32)</td>
<td align="left">OS のオーディオ スタックによって管理されます。</td>
</tr>
<tr class="odd">
<td align="left"><strong>Mic</strong></td>
<td align="left">Mic 0</td>
<td align="left">すべてのマイク配列、または mono で</td>
</tr>
</tbody>
</table>



## <a name="span-idkeywordrecognitionsystemoverviewspanspan-idkeywordrecognitionsystemoverviewspanspan-idkeywordrecognitionsystemoverviewspankeyword-recognition-system-overview"></a><span id="Keyword_Recognition_System_Overview"></span><span id="keyword_recognition_system_overview"></span><span id="KEYWORD_RECOGNITION_SYSTEM_OVERVIEW"></span>キーワード認識システムの概要


この図では、キーワード認識システムの概要を示します。

![cortana を含め、キーワード認識システム、音声ランタイムと音声のアクティブ化マネージャー](images/audio-simple-voice-recon-diagram1.png)

## <a name="span-idkeywordrecognitionsequencediagramsspanspan-idkeywordrecognitionsequencediagramsspanspan-idkeywordrecognitionsequencediagramsspankeyword-recognition-sequence-diagrams"></a><span id="Keyword_Recognition__Sequence_Diagrams"></span><span id="keyword_recognition__sequence_diagrams"></span><span id="KEYWORD_RECOGNITION__SEQUENCE_DIAGRAMS"></span>キーワード認識シーケンス図


これらの図では、音声ランタイム モジュールは、"speech platform"として表示されます。 前述のように、Windows の音声のプラットフォームは、Cortana、ディクテーションなどの Windows 10 でのエクスペリエンス、音声のすべての電源に使用されます。

使用して、起動中に機能が収集されて[ **IKeywordDetectorOemAdapter::GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-getcapabilities)します。

![スタートアップ時にトレーニング ux 音声のプラットフォームと、oem キーワードの検出機能を示す、キーワード認識シーケンス](images/audio-voice-activation-startup.png)

ときに後で「自分の音声の学習」するユーザーを選択し、トレーニングのフローが呼び出されます。

![キーワード認識シーケンスが表示されたトレーニング ux 音声のプラットフォームと中に、oem キーワード検出機能は、自分の音声を説明します。](images/audio-voice-activation-training.png)

この図では、キーワードの検出に取り組まのプロセスについて説明します。

![キーワードの検出に取り組ま中に音声プラットフォームの oem キーワードの検出機能と、オーディオのドライブの検出機能を示す、キーワード認識シーケンス](images/audio-voice-activation-arming.png)

## <a name="span-idwavertenhancementsspanspan-idwavertenhancementsspanspan-idwavertenhancementsspanwavert-enhancements"></a><span id="WAVERT_Enhancements"></span><span id="wavert_enhancements"></span><span id="WAVERT_ENHANCEMENTS"></span>WAVERT の機能強化


WaveRT ミニポート ドライバーによって実装されるミニポート インターフェイスが定義されます。 これらのインターフェイスは、オーディオ ドライバーを簡略化、OS のオーディオのパイプラインのパフォーマンスと信頼性を向上またはのいずれかの新しいシナリオをサポートするメソッドを提供します。 そのバッファーの静的な式に、OS にサイズの制限を提供するドライバーを許可する新しい PnP デバイス インターフェイスのプロパティが定義されます。

**バッファー サイズ**

ドライバーは、オペレーティング システム、ドライバーとハードウェアの間にオーディオ データを移動するときに、さまざまな制約の下で動作します。 メモリと、ハードウェアの間でデータを移動する物理的なハードウェアのトランスポートのためや、ハードウェアまたは関連付けられている DSP にあるモジュールを処理するシグナルにより、これらの制約があります。

HW KWS ソリューションでは、最大で 200 ミリ秒以上 100 ミリ秒のサイズのオーディオ キャプチャをサポートする必要があります。

ドライバーは、DEVPKEY を設定してバッファー サイズの制約を表します\_KsAudio\_PacketSize\_制約のデバイス プロパティを KSCATEGORY\_KS フィルターを持つ、KS のオーディオ PnP デバイス インターフェイスpin(s) をストリーミングします。 このプロパティを KS フィルター インターフェイスが有効になっているときに有効であり、安定したしておく必要があります。 OS は、ドライバーを識別するハンドルを開くし、ドライバーで呼び出すしなくても、いつでもこの値を読み取ることができます。

**DEVPKEY\_KsAudio\_PacketSize\_Constraints**

DEVPKEY\_KsAudio\_PacketSize\_制約プロパティの値が含まれています、 [ **KSAUDIO\_PACKETSIZE\_制約**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)(つまり、オーディオ ハードウェアに WaveRT バッファーからデータを転送するメカニズム) のための物理ハードウェア制約を記述する構造体。 構造体には、0 以上の配列が含まれています[ **KSAUDIO\_PACKETSIZE\_PROCESSINGMODE\_制約**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)に固有の制約を記述する構造体。処理モードを通知します。 呼び出しの前に、このプロパティを設定して、ドライバー [ **PcRegisterSubdevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregistersubdevice)またはそれ以外の場合、KS のフィルター インターフェイスのピンのストリーミングを有効にします。

**IMiniportWaveRTInputStream**

ドライバーより優れた調整 OS に、ドライバーからオーディオ データ フローのためには、このインターフェイスを実装します。 キャプチャ ストリームでこのインターフェイスが使用可能な場合は、OS は WaveRT バッファー内のデータにアクセスするこのインターフェイスでメソッドを使用します。 詳細については、「 [ **IMiniportWaveRTInputStream::GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)

**IMiniportWaveRTOutputStream**

WaveRT ミニポートは、必要に応じて、OS からの書き込みの進行状況の点に注意し、正確なストリームの位置を取得するため、このインターフェイスを実装します。 詳細については、次を参照してください[ **IMiniportWaveRTOutputStream::SetWritePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertoutputstream-setwritepacket)、 [ **IMiniportWaveRTOutputStream::GetOutputStreamPresentationPosition。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertoutputstream-getoutputstreampresentationposition)と[ **IMiniportWaveRTOutputStream::GetPacketCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertoutputstream-getpacketcount)します。

**パフォーマンス カウンターのタイムスタンプ**

ドライバーのルーチンのいくつかは、Windows パフォーマンス カウンターのタイムスタンプをサンプルのキャプチャまたはデバイスによって提示される時間を反映したを返します。

複雑な DSP がデバイスで困難な場合がありますパイプラインと信号処理では、正確なタイムスタンプを計算して、慎重に行う必要があります。 単に、タイムスタンプでは、サンプル転送された OS との間、DSP に時間を反映する必要がありますされません。

-   DSP、内では、いくつかの内部の DSP ウォール クロックを使用してサンプルのタイムスタンプを追跡します。
-   ドライバーと DSP、間には、Windows パフォーマンス カウンターと DSP ウォール クロックの間の相関関係を計算します。 この手順のことができます (ただし、精度の低い) 非常に単純なものから非常に複雑なより正確な (ただし奇抜に範囲です。
-   これらの遅延は、それ以外の場合の計上しない限り、信号処理のアルゴリズムまたはパイプライン、またはハードウェアのトランスポートのための定数の遅延を考慮します。

**読み取り操作のバースト**

このセクションでは、バーストの読み取りの OS およびドライバーとの対話について説明します。 ドライバーは、パケットのストリーミング WaveRT モデルをサポートしていれば、読み取りバーストが、音声のライセンス認証シナリオ外で再起動できますなど、 [ **IMiniportWaveRTInputStream::GetReadPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)関数。

バーストの 2 つの例の読み取りはシナリオについて説明します。 ミニポート暗証番号 (pin) カテゴリを持つ暗証番号 (pin) をサポートしている場合、1 つのシナリオで[ **KSNODETYPE\_オーディオ\_KEYWORDDETECTOR** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)ドライバーはキャプチャを開始し、内部的にキーワードが検出されたときに、データをバッファリングします。 別のシナリオでドライバーできます必要に応じて内部でバッファー WaveRT バッファーの外部データ場合は、OS は、データを読み込んでいない迅速に呼び出すことによって[ **IMiniportWaveRTInputStream::GetReadPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket).

KSSTATE に移行する前にキャプチャされたバースト データ\_実行するには、ドライバーは、バッファー内のキャプチャのデータと共にサンプルの正確なタイムスタンプ情報を保持する必要があります。 タイムスタンプは、サンプリングを特定のキャプチャされたサンプルのインスタントします。

1. KSSTATE にストリームの遷移後\_これを実行すると、ドライバーすぐにイベントを設定、バッファー通知使用可能なデータが既に存在するためです。
2. このイベントでは、OS は GetReadPacket()、使用できるデータに関する情報を取得を呼び出します。

    a. ドライバーは、有効なキャプチャされたデータのパケット数を返します (KSSTATE からの移行後の最初のパケットの場合は 0\_KSSTATE に停止\_実行)、OS が WaveRT バッファーと、パケット内のパケットの位置を派生できますストリームの先頭位置します。

    b. ドライバーがサンプリングにも対応するパフォーマンス カウンターの値を返します、パケット内の最初のサンプルのインスタントします。 ハードウェアまたはドライバー (外部 WaveRT バッファー) 内でキャプチャ データの量がバッファリングされるに応じて比較的古いこのパフォーマンス カウンターの値である可能性に注意してください。

    c. データがある場合より未読バッファリングされている使用可能なドライバーか: しました。 すぐに、MoreData の WaveRT バッファー (つまりいない GetReadPacket から返されるパケットで使用される領域) の使用可能な領域にデータが true を転送し、このルーチンから戻る前にバッファーの通知イベントを設定します。 または、ii です。 WaveRT バッファーの使用可能な領域に次のパケットをバースト プログラム ハードウェア MoreData の場合は false を返しますおよび後で、転送が完了すると、バッファー イベントを設定します。
3. OS は、GetReadPacket() によって返される情報を使用して WaveRT バッファーからデータを読み取ります。
4. OS は、次のバッファー通知イベントを待機します。 ドライバー (2 c) の手順で、バッファーの通知を設定する場合、待機をすぐに終了があります。
5. ドライバーが WaveRT バッファーにより、キャプチャされたデータを転送し、OS を読み取るに使用できるようにした後に、イベントを設定する場合は、ドライバーでは、イベントはすぐには (2 c) の手順で設定しなかった、
6. (2) に移動します。
[ **KSNODETYPE\_オーディオ\_KEYWORDDETECTOR** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)キーワード detector のピン ドライバー割り当てる必要があります十分なバーストの内部バッファリングのオーディオ データの少なくとも返ります。 OS は、作成が失敗した場合、ストリーム バッファー オーバーフロー ドライバーでは、前に、暗証番号 (pin) を内部バッファリングのアクティビティと関連付けられている無料のリソースになる可能性があります。


## <a name="span-idwakeonvoicespanspan-idwakeonvoicespanspan-idwakeonvoicespanwake-on-voice"></a><span id="Wake_on_Voice"></span><span id="wake_on_voice"></span><span id="WAKE_ON_VOICE"></span>Wake on 音声

音声でスリープを解除 (WoV) をアクティブにして言っておきたいコルタナさん」などの特定のキーワードの完全な電源状態で、画面に低電力状態では、オフの画面から、音声認識エンジンのクエリを実行できます。

この機能により、デバイスのデバイスが、画面がオフと、デバイスがアイドル状態のときなど、低電力状態の間にユーザーの音声を常にリッスンするためです。 この機能を使用するには、低電力量通常マイクの記録中に検出された電源の高い使用と比較した場合は、リッスンしているモードを使用します。 低電力の音声認識は、「コルタナさん後ろにチェーンされた音声フレーズのように定義済みのキー フレーズ単純に、ユーザーなどの"場合は、次予定"ハンズフリーで音声を呼び出す。 デバイスが使用中かどうかに関係なく動作するか、アイドル画面オフこれは。

オーディオ スタックは、キーワードが検出されたことを目的のクライアントに通知すると、ウェイク データ (スピーカー ID、キーワードのトリガー、信頼レベル) の通信を担当します。


**最新のスタンバイ システムでの検証**

システムのアイドル状態から WoV を検証できます[最新スタンバイ](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)システムを使用して、 [AC 電源で音声の基本的なテストで、最新のスタンバイ Wake](https://docs.microsoft.com/windows-hardware/test/hlk/testref/69df7cf2-6024-4eee-92ee-1506480614ee) 、[最新のスタンバイ Wake on 音声の基本的なテストDC 電源の](https://docs.microsoft.com/windows-hardware/test/hlk/testref/614ffb93-eced-45ab-bf7b-e09291a97fd2)で、 [HLK](https://docs.microsoft.com/windows-hardware/test/hlk/)します。 これらのテストでは、システムについて、ハードウェア キーワード spotter (HW KWS) が、最も深いランタイム アイドル プラットフォームの状態 (DRIPS) を入力することし、システム再開の待機時間 1 秒以下の音声コマンドで最新のスタンバイから復帰させることがでことを確認します。 
