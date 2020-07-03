---
title: 音声のアクティブ化
description: Cortana では、windows speech プラットフォームを使用して、Cortana やディクテーションなどの Windows 10 の音声エクスペリエンスをすべて強化します。
ms.assetid: 0684EF32-AA76-418B-9027-1C067A8140E3
ms.date: 05/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 797b27baa8aa4f6fb4208c170ec45fd19e46d68a
ms.sourcegitcommit: a391539e144ffc610db9eec05875568c72878eb2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85854460"
---
# <a name="voice-activation"></a>音声のアクティブ化

> [!NOTE]
> このトピックでは、主に Windows 10 (バージョン1909以前) で提供されているコンシューマーエクスペリエンスについて説明します。

Cortana は、2013の Microsoft BUILD Developer カンファレンスで初めて personal assistant テクノロジをデモンストレーションしました。 Windows speech プラットフォームは、Cortana やディクテーションなど、Windows 10 のすべての音声エクスペリエンスを強化するために使用されます。 音声のアクティブ化は、ユーザーが特定の語句 ("こんにちは Cortana") を伝えて、さまざまなデバイスの電源状態から音声認識エンジンを呼び出せるようにする機能です。 音声アクティブ化テクノロジをサポートするハードウェアを作成するには、このトピックの情報を確認してください。

> [!NOTE]
> 音声のアクティブ化の実装は、重要なプロジェクトであり、SoC ベンダーによって完了したタスクです。 Oem は、soc の実装に関する声のアクティベーションの実装について、SoC ベンダーに問い合わせることができます。

## <a name="cortana-end-user-experience"></a>Cortana エンドユーザーエクスペリエンス

Windows で使用できる音声操作のエクスペリエンスを理解するには、次のトピックを確認してください。

|トピック|説明|
|----|----|
| [Cortana とは](https://support.microsoft.com/help/17214/cortana-what-is)      | Cortana の概要と使用方法について説明します。                 |
| [Cortana を作る](https://support.microsoft.com/help/17178/windows-10-make-cortana-yours) | Cortana の設定画面から使用できるカスタマイズについて説明します。 |

## <a name="introduction-to-hey-cortana-voice-activation-and-learn-my-voice"></a>"Cortana" ボイスアクティベーションと "音声の学習" の概要

### <a name="hey-cortana-voice-activation"></a>Cortana "音声ライセンス認証"

"Cortana" 音声ライセンス認証 (VA) 機能を使用すると、ユーザーは、音声を使用してアクティブなコンテキスト (つまり、現在画面にあるもの) の外部で Cortana エクスペリエンスをすばやく操作できます。 ユーザーは、デバイスに対して物理的に対話することなく、すぐにエクスペリエンスにアクセスできるようにしたいと考えています。 携帯電話のユーザーの場合、車を運転し、車の運転に注意を払っていることが原因である可能性があります。 Xbox ユーザーの場合、コントローラーを見つけて接続しないことが原因である可能性があります。 PC ユーザーの場合、これは、マウス、タッチ、キーボードなどの複数の操作を実行しなくても、簡単にエクスペリエンスにアクセスできることが原因である可能性があります。たとえば、キッチンのコンピューターなどです。

音声のアクティブ化は、事前に定義されたキーフレーズまたは "ライセンス認証語句" を使用して、常に音声入力を待機します。 キーフレーズは、ステージングされたコマンドとして単独で ("発音" として)、その後に音声操作を実行することができます。たとえば、"Cortana は次の会議ですか?" はチェーン化されたコマンドです。

*キーワード検出*という用語は、ハードウェアまたはソフトウェアによってキーワードが検出されたかどうかを示します。

*キーワードのみ*のアクティブ化は、cortana キーワードのみが指定されている場合に行われます。 cortana は、聞き取りモードに入ったことを示すために、そのサウンドを開始して再生します。

チェーン化された*コマンド*では、キーワードの直後にコマンドを発行する機能 (cortana、電話 John など) を記述し、cortana start (まだ開始されていない場合) を使用して、(John との通話を開始する) コマンドに従います。

この図は、チェーンとキーワードのみのアクティベーションを示しています。

![オーディオバッファーとタイムシーケンスを示すチェーンとキーワードのアクティブ化の図](images/audio-chained-keyword-activation.png)

Microsoft では、ハードウェアキーワード検出の品質を保証し、ハードウェアキーワード検出が存在しない場合や使用できない場合に Cortana エクスペリエンスを提供するために使用される、OS の既定のキーワードのスポット設定 (ソフトウェアキーワードのスポットの色を示す) を提供しています。

### <a name="the-learn-my-voice-feature"></a>"音声の学習" 機能

"音声の学習" 機能を使用すると、ユーザーは Cortana をトレーニングして独自の音声を認識することができます。 これは、[Cortana 設定] 画面でユーザーが *"cortana" という言葉*をクリックすると表示されます。 ユーザーは、ユーザーの声の固有の属性を識別するために十分な数の発音パターンを提供する、慎重に選択された6つのフレーズを繰り返します。

![hw キーワードを使用した cortana デスクトップの設定音声によるスリープ解除](images/audio-voice-activation-settings-2017.png)

音声のアクティブ化が "音声の学習" とペアリングされている場合、2つのアルゴリズムが連携して、偽のライセンス認証を軽減します。 これは、会議室のシナリオに特に役立ちます。この場合、1人は、部屋に "Cortana" と書かれています。 この機能は、Windows 10 バージョン1903以前のバージョンでのみ使用できます。

音声のアクティブ化は、キーフレーズが検出された場合に反応するキーワードを使用します。 KWS がデバイスを低電力状態からウェイクアップする場合、このソリューションは Wake on Voice (WoV) と呼ばれます。 詳細については、「 [Wake On Voice](#wake-on-voice)」を参照してください。

## <a name="glossary-of-terms"></a>用語集

この用語集は、音声のアクティブ化に関連する用語をまとめたものです。

|用語|例/定義|
|----|----|
| ステージングコマンド        | 例: Cortana <一時停止し、気象の> を待機しています。 これは、"2 回限りのコマンド" または "キーワードのみ" と呼ばれることもあります。 |
|チェーンコマンド        | 例: Cortana はどのような天気ですか。 これは、"ワンショットコマンド" と呼ばれることもあります。 |
| 音声のアクティブ化      | 事前定義されたアクティベーションのキーワード検出を提供するシナリオ。 たとえば、"コル Cortana" は Microsoft Voice Activation のシナリオです。 |
|WoV                    | Wake on Voice –画面から電源の状態を小さくして、電源状態を最大限にした画面に音声でライセンス認証を行うことができるようにするテクノロジです。 |
|最新のスタンバイからの WoV| 最新のスタンバイ (S0ix) 画面をオフにした状態で、フルパワー (S0) 状態の画面に復帰します。 |
|モダン スタンバイ |Windows 低電力アイドルインフラストラクチャ-Windows 10 のコネクトスタンバイ (CS) の後継。 最新のスタンバイの最初の状態は、画面がオフになっているときです。 最も深いスリープ状態は、DRIPS/回復性にあります。 詳細については、「[最新のスタンバイ](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)」を参照してください。   |
|KWS                    |キーワードのスポットの検出-"コルタナさん" の検出を提供するアルゴリズム |
| SW KWS                |ソフトウェアキーワードのスポットイン-ホスト (CPU) で実行される KWS の実装。 "Cortana" については、SW KWS が Windows の一部として含まれています。 |
| ハードウェア KWS                | ハードウェアオフロードキーワードのスポットライン–ハードウェアでオフロードを実行する KWS の実装。 |
|バーストバッファー           | KWS 検出が発生した場合に "bursted up" できる PCM データを格納するために使用される円形バッファー。 KWS 検出をトリガーしたすべてのオーディオが含まれるようにします。 |
|キーワード検出機能の OEM アダプター |WoV 対応 HW が Windows および Cortana スタックと通信できるようにするドライバーレベルの shim。 |
|モデル | KWS アルゴリズムによって使用される音響モデルデータファイル。 データファイルは静的です。 モデルは、ロケールごとに1つローカライズされます。|

## <a name="integrating-a-hardware-keyword-spotter"></a>ハードウェアキーワードスポットを統合する

ハードウェアキーワードを指定するには、次のタスクを完了する必要があります。

- このトピックで後述する SYSVAD サンプルに基づいて、カスタムキーワード検出機能を作成します。 これらのメソッドは、[キーワード検出機能の OEM アダプターインターフェイス](#keyword-detector-oem-adapter-interface)に記述されている COM DLL に実装します。
- [Wavert の強化](#wavert-enhancements)に関するページで説明されている WAVE RT の機能強化を実装します。
- INF ファイルのエントリを指定して、キーワードの検出に使用するカスタム APOs を記述します。
  - [PKEY \_ FX \_ KeywordDetector \_ StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-streameffectclsid)
  - [PKEY \_ FX \_ KeywordDetector \_ ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-modeeffectclsid)
  - [PKEY \_ FX \_ KeywordDetector \_ EndpointEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-endpointeffectclsid)
  - [\_ \_ \_ \_ ストリーミングでサポートされている PKEY SFX KeywordDetector processingmodes \_ \_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-keyworddetector-processingmodes-supported-for-streaming)
  - [\_ \_ \_ \_ ストリーミングでサポートされている PKEY mfx KeywordDetector processingmodes \_ \_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-keyworddetector-processingmodes-supported-for-streaming)
  - [\_ \_ \_ \_ ストリーミングでサポートされている PKEY EFX KeywordDetector processingmodes \_ \_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-efx-keyworddetector-processingmodes-supported-for-streaming)
- 「[オーディオデバイスの推奨](https://docs.microsoft.com/windows-hardware/design/component-guidelines/audio)事項」のハードウェアの推奨事項とテストガイダンスを確認します。 このトピックでは、Microsoft の Speech プラットフォームでの使用を目的としたオーディオ入力デバイスの設計と開発に関するガイダンスと推奨事項について説明します。
- ステージングコマンドとチェーンコマンドの両方をサポートします。
- サポートされている各 Cortana ロケールについて "Cortana" をサポートします。
- APOs (オーディオ処理オブジェクト) は、次のような影響を与える必要があります。
  - AEC
  - AGC
  - NS
- 音声処理モードの効果は、MFX APO によって報告される必要があります。
- APO は、MFX として形式変換を実行する場合があります。
- APO は、次の形式を出力する必要があります。
  - 16 kHz、mono、FLOAT。
- 必要に応じて、オーディオキャプチャプロセスを拡張するカスタム APOs を設計します。 詳細については、「 [Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)」を参照してください。

ハードウェアオフロードキーワードスポットライン (HW KWS) WoV の要件

- HW KWS WoV は、S0 の動作中にサポートされています。また、S0 スリープ状態は、"最新のスタンバイ" とも呼ばれます。  
- HW KWS WoV は S3 からはサポートされていません。  

ハードウェア KWS の AEC の要件

- Windows バージョン1709の場合
  - S0 スリープ状態 (最新のスタンバイ) の AEC に対して HW KWS WoV をサポートする必要はありません。  
  - Windows バージョン1709では、S0 に対する HW KWS WoV の動作状態はサポートされていません。

- Windows バージョン1803の場合
  - ハードウェア KWS WoV for S0 の動作状態がサポートされています。
  - ハードウェア KWS WoV を S0 の動作状態にするには、APO で AEC がサポートされている必要があります。

## <a name="sample-code-overview"></a>サンプルコードの概要

SYSVAD 仮想オーディオアダプターサンプルの一部として、GitHub で音声アクティベーションを実装するオーディオドライバーのサンプルコードがあります。 このコードを開始点として使用することをお勧めします。 このコードは、この場所で入手できます。

<https://github.com/Microsoft/Windows-driver-samples/blob/master/audio/sysvad/>

SYSVAD サンプルオーディオドライバーの詳細については、「[サンプルオーディオドライバー](sample-audio-drivers.md)」を参照してください。

## <a name="keyword-recognition-system-information"></a>キーワード認識システム情報

### <a name="voice-activation-audio-stack-support"></a>音声アクティブ化オーディオスタックのサポート

音声のアクティブ化を有効にするためのオーディオスタック外部インターフェイスは、音声プラットフォームとオーディオドライバーの通信パイプラインとして機能します。 外部インターフェイスは、3つの部分に分かれています。

- *キーワード検出デバイスドライバーインターフェイス (DDI)*。 キーワード検出機能のデバイスドライバーインターフェイスは、HW キーワード取り組ま (KWS) の構成とを行います。  また、ドライバーは検出イベントをシステムに通知するためにも使用されます。
- *キーワード検出機能 OEM アダプター DLL*。 この DLL は、キーワード検出を支援するために OS によって使用されるドライバー固有の不透明なデータを調整する COM インターフェイスを実装します。
- *Wavert ストリーミングの機能強化*。 拡張機能により、オーディオドライバーは、バッファー内のオーディオデータをキーワード検出からバーストすることができます。

### <a name="audio-endpoint-properties"></a>オーディオエンドポイントのプロパティ

オーディオエンドポイントグラフの作成は正常に行われます。 グラフは、リアルタイムキャプチャよりも高速に処理できるように準備されています。 キャプチャされたバッファーのタイムスタンプは true のままです。 具体的には、タイムスタンプには、過去にキャプチャされ、バッファーに記録され、"バースティング" になっているデータが正しく反映されます。

### <a name="theory-of-operation"></a>操作の理論

ドライバーは、キャプチャデバイスの KS フィルターを通常どおりに公開します。 このフィルターでは、いくつかの KS プロパティと、検出イベントを構成、有効化、および通知するための KS イベントがサポートされています。 また、フィルターには、キーワードのスポット留め (KWS) pin として識別される追加の pin ファクトリも含まれています。 この pin は、キーワードのスポット留めからオーディオをストリーミングするために使用されます。

次のプロパティです。

- サポートされているキーワードの種類- [**Ksk プロパティ \_ sounddetector \_ パターン**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-patterns)。 このプロパティは、検出されるキーワードを構成するためにオペレーティングシステムによって設定されます。
- キーワードパターン Guid- [**Ksk プロパティ \_ sounddetector \_ supportedpatterns**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-supportedpatterns)の一覧。 このプロパティは、サポートされているパターンの種類を識別する Guid の一覧を取得するために使用されます。
- 、 [**Ksproperty の \_ sounddetector \_ 機**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-armed)がありません。 この読み取り/書き込みプロパティは、検出されたかどうかを示す単純なブール値です。 OS は、キーワード検出機能を利用するようにこれを設定します。 OS はこれをオフにしてオフにできます。 キーワードパターンが設定され、キーワードが検出された後に、ドライバーによって自動的にクリアされます。 (OS は rearm する必要があります)。
- 一致結果- [**Ksproperty \_ sounddetector の \_ matchresult**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-matchresult)。 この読み取りプロパティは、検出後に結果データを保持します。

キーワードが検出されたときに発生するイベントは、 [**KSEVENT \_ sounddetector \_ matchdetected**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-sounddetector-matchdetected)イベントです。

### <a name="sequence-of-operation"></a>操作のシーケンス

#### <a name="system-startup"></a>システムの起動

1. OS はサポートされているキーワードの種類を読み取って、その形式のキーワードがあることを確認します。
2. OS によって検出された状態変更イベントが登録されます。
3. OS はキーワードのパターンを設定します。
4. OS は検出を行います。

#### <a name="on-receiving-the-ks-event"></a>KS イベントの受信時

1. ドライバーが検出機能を無効にしています。
2. OS はキーワード検出の状態を読み取り、返されたデータを解析し、検出されたパターンを特定します。
3. OS は検出を再アームします。

### <a name="internal-driver-and-hardware-operation"></a>内部のドライバーとハードウェアの操作

検出が実行されている間、ハードウェアは小さい FIFO バッファーでオーディオデータを継続的にキャプチャしてバッファリングできます。 (この FIFO バッファーのサイズは、このドキュメントの外部の要件によって決まりますが、通常は数秒から数秒である場合があります)。検出アルゴリズムは、このバッファーを介してデータストリームを処理します。 ドライバーとハードウェアの設計は、キーワードが検出されるまで、ドライバーとハードウェア間の相互作用がなく、"アプリケーション" プロセッサに割り込みが発生しないようにするためのものです。 これにより、他のアクティビティが存在しない場合に、システムがより低い電力状態になる可能性があります。

ハードウェアがキーワードを検出すると、割り込みが生成されます。 ドライバーが割り込みを処理するのを待機している間、ハードウェアはオーディオをバッファーにキャプチャし続け、キーワードが失われた後にデータがバッファーに格納されないようにします。

### <a name="keyword-timestamps"></a>キーワードのタイムスタンプ

キーワードを検出した後、すべての音声アクティブ化ソリューションで、キーワードの開始前の250ミリ秒を含む、すべての音声キーワードをバッファーする必要があります。 オーディオドライバーは、ストリーム内のキーフレーズの先頭と末尾を識別するタイムスタンプを提供する必要があります。

キーワードの開始/終了タイムスタンプをサポートするために、dsp ソフトウェアでは、DSP クロックに基づいて内部的にイベントのタイムスタンプを行うことが必要になる場合があります。 キーワードが検出されると、DSP ソフトウェアはドライバーとやり取りして KS イベントを準備します。 ドライバーと DSP ソフトウェアでは、DSP タイムスタンプを Windows パフォーマンスカウンター値にマップする必要があります。 これを行う方法は、ハードウェア設計に固有のものです。 考えられる解決策の1つは、ドライバーが現在のパフォーマンスカウンターを読み取り、現在の DSP タイムスタンプに対してクエリを実行し、現在のパフォーマンスカウンターを再び読み取り、パフォーマンスカウンターと DSP 時間の相関関係を推定することです。 関連付けを指定すると、ドライバーは、キーワード DSP タイムスタンプを Windows パフォーマンスカウンターのタイムスタンプにマップできます。

## <a name="keyword-detector-oem-adapter-interface"></a>キーワード検出機能 OEM アダプターインターフェイス

OEM は、OS とドライバーの仲介役として機能する COM オブジェクトの実装を提供します。これにより、 [**Ksproperty の \_ sounddetector \_ パターン**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-patterns)および[**ksproperty の \_ sounddetector の \_ matchresult**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-matchresult)を通じて、オーディオドライバーに書き込まれた不透明なデータを計算または解析することができます。

COM オブジェクトの CLSID は、 [**Ksproperty \_ sounddetector \_ supportedpatterns**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-supportedpatterns)によって返される検出パターン型 GUID です。 OS は、パターン型 GUID を渡す CoCreateInstance を呼び出して、キーワードパターン型と互換性のある適切な COM オブジェクトをインスタンス化し、オブジェクトの IKeywordDetectorOemAdapter インターフェイスでメソッドを呼び出します。

### <a name="com-threading-model-requirements"></a>COM スレッドモデルの要件

OEM の実装では、任意の COM スレッドモデルを選択できます。

### <a name="ikeyworddetectoroemadapter"></a>IKeywordDetectorOemAdapter

インターフェイスのデザインでは、オブジェクトの実装をステートレスな状態に保ちます。 つまり、実装では、メソッド呼び出しの間に状態を格納する必要がありません。 実際、内部 C++ クラスでは、通常、COM オブジェクトを実装するために必要なものを超えるメンバー変数は必要ありません。

### <a name="methods"></a>メソッド

次のメソッドを実装します。

- [**IKeywordDetectorOemAdapter::BuildArmingPatternData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-buildarmingpatterndata)
- [**IKeywordDetectorOemAdapter:: ComputeAndAddUserModelData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-computeandaddusermodeldata)
- [**IKeywordDetectorOemAdapter:: GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-getcapabilities)
- [**IKeywordDetectorOemAdapter::P arseDetectionResultData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-parsedetectionresultdata)
- [**IKeywordDetectorOemAdapter:: VerifyUserKeyword**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-verifyuserkeyword)

### <a name="keywordid"></a>キーの方法

[**Keywordid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/ne-keyworddetectoroemadapter-__midl_ikeyworddetectoroemadapter_0002)列挙体は、キーワードの語句テキスト/関数を識別し、Windows 生体認証サービスアダプターでも使用されます。 詳細については、「[生体認証フレームワークの概要-コアプラットフォームコンポーネント](https://docs.microsoft.com/windows/desktop/SecBioMet/biometric-framework-overview)」を参照してください。

```cpp
typedef enum  {
  KwInvalid              = 0,
  KwHeyCortana           = 1,
  KwSelect               = 2
} KEYWORDID;
```

### <a name="keywordselector"></a>KEYWORDSELECTOR

[**KEYWORDSELECTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/ns-keyworddetectoroemadapter-__midl_ikeyworddetectoroemadapter_0003)構造体は、特定のキーワードと言語を一意に選択する id のセットです。

```cpp
typedef struct
{
    KEYWORDID KeywordId;
    LANGID LangId;
} KEYWORDSELECTOR;
```

### <a name="handling-model-data"></a>モデルデータの処理

*静的ユーザーに依存しないモデル*-通常、OEM dll には、dll または dll に含まれる別のデータファイルに組み込まれている、静的なユーザーに依存しないモデルデータが含まれます。 GetCapabilities ルーチンによって返されるサポートされているキーワード Id のセットは、このデータに依存します。 たとえば、GetCapabilities によって返されるサポートされているキーワード Id の一覧に KwHeyCortana が含まれている場合、静的なユーザーに依存しないモデルデータには、サポートされているすべての言語の "コルタナ" (またはその翻訳) のデータが含まれます。

*動的なユーザー依存モデル*-IStream はランダムアクセスストレージモデルを提供します。 OS は、IKeywordDetectorOemAdapter インターフェイスの多くのメソッドに IStream インターフェイスポインターを渡します。 OS は、最大 1 MB のデータを格納するために、IStream の実装を適切なストレージにバックアップします。

このストレージ内のデータの内容と構造は、OEM によって定義されます。 目的は、OEM DLL によって計算または取得される、ユーザー依存モデルデータの永続的なストレージです。

特にユーザーがキーワードをトレーニングしたことがない場合、OS は空の IStream でインターフェイスメソッドを呼び出すことができます。 OS は、ユーザーごとに個別の IStream ストレージを作成します。 言い換えると、特定の IStream は1人のユーザーに対してのみモデルデータを格納します。

OEM DLL の開発者は、ユーザーに依存しないデータとユーザー依存データを管理する方法を決定します。 ただし、IStream の外部にユーザーデータが格納されることはありません。 OEM DLL の考えられる1つの設計では、現在のメソッドのパラメーターに応じて、IStream と静的ユーザーに依存しないデータへのアクセスを内部的に切り替えることができます。 代替デザインでは、各メソッド呼び出しの開始時に IStream を確認し、まだ存在していない場合は、メソッドの残りの部分がすべてのモデルデータの IStream にのみアクセスできるようにします。

## <a name="training-and-operation-audio-processing"></a>トレーニングと操作のオーディオ処理

前に説明したように、トレーニング UI フローでは、オーディオストリームですべての発音豊富な文が使用できるようになります。 各文は、 [**IKeywordDetectorOemAdapter:: VerifyUserKeyword**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-verifyuserkeyword)に個別に渡され、予期されるキーワードが含まれており、許容される品質があることを確認します。 すべての文は、UI によって収集および検証された後、 [**IKeywordDetectorOemAdapter:: ComputeAndAddUserModelData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-computeandaddusermodeldata)の1回の呼び出しで渡されます。

音声は、音声アクティブ化トレーニングのための一意の方法で処理されます。 次の表は、ボイスアクティベーショントレーニングと通常の音声認識の使用の違いをまとめたものです。

|<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><strong>音声トレーニング</strong></td>
<td align="left"><strong>音声認識</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>モード</strong></td>
<td align="left">Raw</td>
<td align="left">生または音声</td>
</tr>
<tr class="odd">
<td align="left"><strong>Pin</strong></td>
<td align="left">標準</td>
<td align="left">KWS</td>
</tr>
<tr class="even">
<td align="left"><strong>オーディオ形式</strong></td>
<td align="left">32-ビット float (Type = Audio、Subtype = IEEE_FLOAT、サンプリングレート = 16 kHz、ビット = 32)</td>
<td align="left">OS オーディオスタックで管理</td>
</tr>
<tr class="odd">
<td align="left"><strong>Mic</strong></td>
<td align="left">Mic 0</td>
<td align="left">配列または mono のすべての mic</td>
</tr>
</tbody>
</table>

## <a name="keyword-recognition-system-overview"></a>キーワード認識システムの概要

この図は、キーワード認識システムの概要を示しています。

![cortana を含むキーワード認識システム (音声ランタイムと音声ライセンス認証マネージャー)](images/audio-simple-voice-recon-diagram1.png)

## <a name="keyword-recognition-sequence-diagrams"></a>キーワード認識シーケンス図

これらの図では、speech ランタイムモジュールが "speech platform" として表示されています。 前述のように、windows speech プラットフォームを使用して、Cortana やディクテーションなどの Windows 10 のすべての音声エクスペリエンスを強化します。

起動時には、 [**IKeywordDetectorOemAdapter:: GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-getcapabilities)を使用して機能が収集されます。

![スタートアップ時のトレーニング ux speech プラットフォームと oem キーワード検出機能を示すキーワード認識シーケンス](images/audio-voice-activation-startup.png)

その後、ユーザーが "音声の学習" を選択すると、トレーニングフローが呼び出されます。

![音声の学習中にトレーニング ux speech プラットフォームと oem キーワード検出機能を示すキーワード認識シーケンス](images/audio-voice-activation-training.png)

この図は、キーワード検出の取り組まプロセスを示しています。

![キーワード検出の取り組ま中に音声プラットフォームの oem キーワード検出機能とオーディオドライブ検出機能を示すキーワード認識シーケンス](images/audio-voice-activation-arming.png)

## <a name="wavert-enhancements"></a>WAVERT の機能強化

ミニポートインターフェイスは、WaveRT ミニポートドライバーによって実装されるように定義されています。 これらのインターフェイスは、オーディオドライバーを簡略化し、OS オーディオパイプラインのパフォーマンスと信頼性を向上させるか、新しいシナリオをサポートするメソッドを提供します。 ドライバーがバッファーサイズの制約の静的式を OS に提供できるように、新しい PnP デバイスインターフェイスプロパティが定義されています。

### <a name="buffer-sizes"></a>バッファーサイズ

ドライバーは、OS、ドライバー、およびハードウェア間でオーディオデータを移動するときに、さまざまな制約の下で動作します。 これらの制約は、メモリとハードウェア間でデータを移動する物理ハードウェアトランスポート、またはハードウェアまたは関連する DSP 内の信号処理モジュールによって発生することがあります。

HW-KWS ソリューションでは、少なくとも100ミリ秒から200ミリ秒までのオーディオキャプチャサイズをサポートする必要があります。

ドライバーは、 \_ \_ \_ \_ ks ストリーミングピンがある ks フィルターの KSCATEGORY audio PNP デバイスインターフェイスで DEVPKEY ksaudio PacketSize constraints デバイスプロパティを設定することによって、バッファーサイズの制約を表します。 このプロパティは、KS フィルターインターフェイスが有効になっている間は有効で安定した状態を維持する必要があります。 OS は、ドライバーへのハンドルを開き、ドライバーでを呼び出すことなく、いつでもこの値を読み取ることができます。

### <a name="devpkey_ksaudio_packetsize_constraints"></a>DEVPKEY \_ ksaudio \_ PacketSize の \_ 制約

DEVPKEY \_ ksaudio \_ PacketSize \_ constraints プロパティ値には、物理ハードウェアの制約を説明する[**ksk audio \_ PacketSize \_ constraints**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)構造体が含まれています (たとえば、wavert バッファーからオーディオハードウェアにデータを転送するメカニズムが原因です)。 構造体には、シグナル処理モードに固有の制約を記述する0個以上の[**Ksaudio \_ PACKETSIZE \_ processingmode \_ 制約**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)構造体の配列が含まれています。 ドライバーは、 [**Pcregiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)呼び出す前にこのプロパティを設定します。それ以外の場合は、そのストリームのピンに対して KS フィルターインターフェイスを有効にします。

### <a name="iminiportwavertinputstream"></a>IMiniportWaveRTInputStream

ドライバーは、ドライバーから OS へのオーディオデータフローをより適切に調整するために、このインターフェイスを実装します。 このインターフェイスがキャプチャストリームで使用可能な場合、OS はこのインターフェイスのメソッドを使用して WaveRT バッファー内のデータにアクセスします。 詳細については、「 [ **IMiniportWaveRTInputStream:: GetReadPacket** 」を参照してください。](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)

### <a name="iminiportwavertoutputstream"></a>IMiniportWaveRTOutputStream

WaveRT ミニポートは、必要に応じて、このインターフェイスを実装して、OS からの書き込みの進行状況を通知し、正確なストリーム位置を返します。 詳細については、「 [**IMiniportWaveRTOutputStream:: SetWritePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-setwritepacket)」、「 [**IMiniportWaveRTOutputStream:: Getoutputstreamプレゼンテーション位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-getoutputstreampresentationposition)」、および「 [**IMiniportWaveRTOutputStream:: getpacketcount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-getpacketcount)」を参照してください。

### <a name="performance-counter-timestamps"></a>パフォーマンスカウンターのタイムスタンプ

いくつかのドライバールーチンは、デバイスによってサンプルがキャプチャまたは表示される時刻を反映する Windows パフォーマンスカウンターのタイムスタンプを返します。

複雑な DSP パイプラインと信号処理があるデバイスでは、正確なタイムスタンプを計算することは困難であるため、熟考を行う必要があります。 タイムスタンプには、サンプルが OS と DSP 間で転送された時刻を単に反映させることはできません。

- DSP 内で、一部の内部 DSP ウォールクロックを使用してサンプルタイムスタンプを追跡します。
- ドライバーと DSP の間で、Windows パフォーマンスカウンターと DSP の壁面クロックの間の相関関係を計算します。 この手順は、非常に単純な (ただし、正確ではありませんが) 非常に複雑なものや斬新なもの (より正確です) の範囲です。
- シグナル処理アルゴリズムまたはパイプラインまたはハードウェアトランスポートに起因する一定の遅延を考慮します。ただし、これらの遅延が考慮されない場合は除きます。

### <a name="burst-read-operation"></a>バースト読み取り操作

ここでは、バースト読み取りの OS とドライバーの相互作用について説明します。 バースト読み取りは、ドライバーが[**IMiniportWaveRTInputStream:: GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)関数を含むパケットベースのストリーミング wavert モデルをサポートしている限り、音声ライセンス認証シナリオの外部で発生する可能性があります。

2つのバースト例の読み取りシナリオについて説明します。 1つのシナリオでは、ミニポートが pin カテゴリ[**KSNODETYPE \_ AUDIO \_ KEYWORDDETECTOR**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)を持つ pin をサポートしている場合、ドライバーはキーワードが検出されたときにデータのキャプチャと内部バッファリングを開始します。 別のシナリオでは、 [**IMiniportWaveRTInputStream:: GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)を呼び出すことによって、OS がデータを十分に読み取ることができない場合は、必要に応じて、ドライバーが wastbuffer の外部にあるデータを内部的にバッファーできます。

KSK 状態の実行に移行する前にキャプチャされたデータをバーストするには、 \_ ドライバーは、バッファーキャプチャデータと共に正確なサンプルタイムスタンプ情報を保持する必要があります。 タイムスタンプは、キャプチャしたサンプルのサンプリングの瞬間を識別します。

1. ストリームが KSK 状態の実行に遷移した後 \_ 、ドライバーは、既に使用可能なデータがあるため、バッファー通知イベントを直ちに設定します。
2. このイベントでは、OS は GetReadPacket () を呼び出して、使用可能なデータに関する情報を取得します。

    a. ドライバーは、有効なキャプチャされたデータのパケット番号 (KSK 状態の停止から KSK 状態の実行への移行後の最初のパケットの場合は 0) を返します \_ \_ 。これにより、OS は、wavert バッファー内のパケット位置と、ストリームの開始を基準としたパケットの位置を取得できます。

    b. また、ドライバーは、パケット内の最初のサンプルのサンプリングの瞬間に対応するパフォーマンスカウンターの値を返します。 このパフォーマンスカウンターの値は、ハードウェアまたはドライバー内でバッファーに格納されているキャプチャデータの量によっては、比較的古いものであることに注意してください。

    c. 未読のバッファーデータがある場合は、次のいずれかの方法でドライバーを使用できます。 i. は、そのデータを WaveRT バッファーの使用可能な領域 (GetReadPacket から返されたパケットによって使用されていない領域) に直ちに転送し、さらにデータに対しては true を返し、このルーチンから戻る前にバッファー通知イベントを設定します。 または、ii です。 プログラムハードウェアを使用して、次のパケットを WaveRT バッファーの使用可能な領域にバーストし、さらにデータがある場合は false を返し、後で転送の完了時にバッファーイベントを設定します。
3. OS は、GetReadPacket () によって返された情報を使用して、WaveRT バッファーからデータを読み取ります。
4. OS は、次のバッファー通知イベントを待機します。 ドライバーが手順 (2c) でバッファー通知を設定した場合、待機はすぐに終了する可能性があります。
5. ドライバーが、ステップ (2c) でイベントをすぐに設定しなかった場合、キャプチャされたデータを WaveRT バッファーに転送した後、ドライバーによってイベントが設定され、OS が読み取ることができるようになります。
6. (2) にアクセスします。
[**KSNODETYPE \_ audio \_ KEYWORDDETECTOR**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)キーワード検出ピンの pin では、ドライバーは、少なくとも返り秒のオーディオデータに対して十分な内部バーストバッファリングを割り当てる必要があります。 OS が pin のストリームを作成できなかった場合、バッファーがオーバーフローする前に、ドライバーは内部バッファリングアクティビティを終了し、関連付けられているリソースを解放します。

## <a name="wake-on-voice"></a>電話でのスリープ状態

Wake On Voice (WoV) を使用すると、ユーザーは、"コル Cortana" のような特定のキーワードを言って、音声認識エンジンをアクティブ化したり、画面の電源をオフにしたりできます。

この機能により、デバイスは、画面がオフになってデバイスがアイドル状態になっているときなど、デバイスの電源が切れている間は常にユーザーの音声をリッスンできます。 これは、通常のマイクの記録時に見られる電力使用量の増加と比較して、リッスンモードを使用することによって行われます。 音声認識が低いので、ユーザーは "コル Cortana" のような事前定義されたキーフレーズに続けて、"次の予定があるとき" といったチェーンされた音声フレーズを使用して、自由に音声を呼び出すことができます。 これは、デバイスが使用中であるか、画面がオフの状態であるかに関係なく機能します。

オーディオスタックは、ウェイクアップデータ (スピーカー ID、キーワードトリガー、信頼レベル) の通信と、キーワードが検出されたことを対象のクライアントに通知する役割を担います。

### <a name="validation-on-modern-standby-systems"></a>最新のスタンバイシステムでの検証

システムのアイドル状態からの WoV は、最新のスタンバイ[wake On 音声基本テスト (AC 電源)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/69df7cf2-6024-4eee-92ee-1506480614ee)と、 [HLK](https://docs.microsoft.com/windows-hardware/test/hlk/)の[DC 電源の最新のスタンバイ wake on 音声基本テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/614ffb93-eced-45ab-bf7b-e09291a97fd2)を使用して、[最新のスタンバイ](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)システムで検証できます。 これらのテストでは、システムがハードウェアのキーワードを使用しているかどうかを確認します (HW-KWS)。最も深いランタイムアイドルプラットフォームの状態 (DRIPS) に入ることができます。また、システム再開の待機時間が1秒以下の場合は、音声コマンドの最新のスタンバイから復帰できます。
