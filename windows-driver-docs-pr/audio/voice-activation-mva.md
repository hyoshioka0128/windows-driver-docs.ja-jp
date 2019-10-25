---
title: 複数の音声アシスタント
description: 複数の音声アシスタントプラットフォームでは、Cortana 以外の追加の音声アシスタントがサポートされています。
ms.assetid: 48a7e96b-58e8-4a49-b673-14036d4108d5
ms.date: 09/26/2019
ms.localizationpriority: medium
ms.openlocfilehash: 54f9aadf0546915e0eab08aeeecee3d0ef470896
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829994"
---
# <a name="multiple-voice-assistant"></a>複数の音声アシスタント

複数の音声アシスタントプラットフォームでは、Cortana 以外の追加の音声アシスタントがサポートされています。 これにより、Pc やウェアラブルなどの Windows デバイスで他のアシスタントを使用できるようになります。 サポートされているキーワードパターンのセットを使用して、複数の音声アシスタントを同じデバイス上でアクティブにすることができます。

Windows Cortana の実装の詳細については、「[音声ライセンス認証](voice-activation.md)」を参照してください。

> [!NOTE]
> 複数の音声アシスタントは、Windows 10 バージョン1903以降でサポートされています。
>

## <a name="voice-activation"></a>音声のアクティブ化

音声のアクティブ化は、ユーザーが特定の語句を指定してさまざまなデバイスの電源状態から音声認識エンジンを呼び出せるようにする機能です。

音声のアクティブ化の実装は、重要なプロジェクトであり、SoC ベンダーによって完了したタスクです。 Oem は、soc の実装に関する声のアクティベーションの実装について、SoC ベンダーに問い合わせることができます。

音声ライセンス認証を使用すると、ユーザーは自分の声を使って、自分のアクティブなコンテキスト (つまり現在画面にあるもの) の外部で音声アシスタントエクスペリエンスをすばやく操作できます。 ユーザーは、デバイスとの物理的な対話やタッチ操作を行わなくても、すぐにエクスペリエンスにアクセスできるようにしたいと考えています。 Xbox ユーザーの場合、コントローラーを検出して接続することはできません。 PC ユーザーは、キッチンのコンピューターのように、マウス、タッチ、キーボードなどの操作を複数回実行しなくても、簡単にエクスペリエンスにアクセスすることができます。

音声のアクティブ化は、キーフレーズが検出された場合に反応するキーワードを使用します。 キーフレーズには、"こんにちは Contoso" などのキーワードが含まれる場合があります。 *キーワード検出*では、ハードウェアまたはソフトウェアによるキーワードの検出について説明します。
キーフレーズは、ステージングされたコマンドとして、またはチェーン化されたコマンドを作成する音声アクション ("こんにちは、次の会議がどこにあるか" という) によって発音されることがあります。

Microsoft では、ハードウェアキーワード検出が使用できない場合に、音声アシスタントを提供するために、OS の既定のキーワードのスポット設定 (ソフトウェアキーワードのスポット処理) を提供しています。 この機能は現在 Cortana で利用可能ですが、2段階のキーワード検出を実行するために他の音声アシスタントをオンボードするには、追加の Microsoft 構成が必要になる場合があります。 詳細については `AskMVA@Microsoft.com`を参照してください。  

KWS がデバイスを低電力状態からウェイクアップする場合、ソリューションは "Wake on Voice (WoV)" と呼ばれます。 詳細については、「 [Wake On Voice](#wake_on_voice)」を参照してください。

## <a name="span-idglossary_of_termsspanspan-idglossary_of_termsspanglossary-of-terms"></a><span id="glossary_of_terms"></span><span id="Glossary_Of_Terms"></span>用語集

この用語集は、音声のアクティブ化に関連する用語をまとめたものです。

|                      |                                                                                                                                                           |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ステージングコマンド | 例: Contoso < 一時停止し、アシスタントの UI が天気の > を待機しています。 これは、"2 回限りのコマンド" または "キーワードのみ" と呼ばれることもあります。 |
| チェーンコマンド | 例: 天気は Contoso さん、 これは、"ワンショットコマンド" と呼ばれることもあります。 |
| 音声のアクティブ化 | 例: 定義済みのアクティブ化キーフレーズでキーワードが検出されたシナリオ |
| Wake on Voice (WoV) | 画面の電源をオフにして電源状態を下げることで、電源状態がすべての画面に表示されるようにするテクノロジ |
|最新のスタンバイからの WoV| 最新のスタンバイ (S0ix) 画面のオフ状態から、フルパワー (S0) 状態の画面への復帰 |
| モダン スタンバイ | Windows 低電力アイドルインフラストラクチャ-Windows 10 のコネクトスタンバイ (CS) の後継。 最新のスタンバイの最初の状態は、画面がオフになっているときです。 最も深いスリープ状態は、DRIPS/回復性にあります。 詳細については、「[最新のスタンバイ](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)」を参照してください。|
| KWS | キーワードのスポットの検出-"こんにちは Contoso" の検出を提供するアルゴリズム |
| SW KWS | ソフトウェアキーワードのスポットイン-ホスト (CPU) で実行される KWS の実装。 "Cortana" については、SW KWS が Windows の一部として含まれています。 |
| ハードウェア KWS | ハードウェアのキーワードのスポットが、ハードウェアでオフロードを実行する KWS の実装 |
| バーストバッファー | KWS 検出が発生した場合に bursted できる PCM データを格納するために使用される循環バッファー。 KWS 検出をトリガーしたすべてのオーディオが含まれるようにします。 |
| イベント検出 OEM アダプター | Windows 音声アシスタントスタックとドライバーの仲介役として機能するユーザーモードコンポーネント |
| モデル | KWS アルゴリズムによって使用される音響モデルデータファイル。 データファイルは静的です。 モデルは、ロケールごとに1つローカライズされます。|
| MVA | 複数の音声エージェント-複数のエージェントをサポートする新しい HWKWS DDI |
| SVA | シングルボイスエージェント-1 つのエージェントのみをサポートする前の HWKWS DDI (Cortana) |

## <a name="span-idimplementing_voice_activationspanspan-idimplementing_voice_activationspanspan-idimplementing_voice_activationspanintegrating-a-hardware-keyword-spotter"></a><span id="Implementing_Voice_Activation"></span><span id="implementing_voice_activation"></span><span id="IMPLEMENTING_VOICE_ACTIVATION"></span>ハードウェアキーワードスポットを統合する

ハードウェアキーワードを指定するには、次のタスクを完了する必要があります。

- このトピックで後述する SYSVAD サンプルに基づいて、カスタムキーワード検出機能を作成します。 これらのメソッドは、 [Ievent 検出機能の OEM アダプターインターフェイス](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/eventdetectoroemadapter/nn-eventdetectoroemadapter-ieventdetectoroemadapter)に記述されている COM DLL に実装します。
- [Wavert の強化](#wavert_enhancements)に関するページで説明されている WAVE RT の機能強化を実装します。
- INF ファイルのエントリを指定して、キーワードの検出に使用するカスタム APOs を記述します。
    - [PKEY\_FX\_KeywordDetector\_StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-streameffectclsid)
    - [PKEY\_FX\_KeywordDetector\_ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-modeeffectclsid)
    - [PKEY\_FX\_KeywordDetector\_EndpointEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-endpointeffectclsid)
    - [PKEY\_SFX\_KeywordDetector\_ProcessingModes\_\_Streaming でサポートされている\_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-keyworddetector-processingmodes-supported-for-streaming)
    - [PKEY\_MFX\_KeywordDetector\_ProcessingModes\_\_Streaming でサポートされている\_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-keyworddetector-processingmodes-supported-for-streaming)
    - [PKEY\_EFX\_KeywordDetector\_ProcessingModes\_\_Streaming でサポートされている\_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-efx-keyworddetector-processingmodes-supported-for-streaming)
- 「[オーディオデバイスの推奨](https://docs.microsoft.com/windows-hardware/design/component-guidelines/audio)事項」のハードウェアの推奨事項とテストガイダンスを確認します。 このトピックでは、Microsoft の Speech プラットフォームでの使用を目的としたオーディオ入力デバイスの設計と開発に関するガイダンスと推奨事項について説明します。
- ステージングコマンドとチェーンコマンドの両方をサポートします。
- 音声アシスタントのロケール要件を満たす
- APOs (オーディオ処理オブジェクト) は、次のような影響を与える必要があります。 
    -   AEC
    -   AGC
    -   STATION
-   音声処理モードの効果は、MFX APO によって報告される必要があります。
-   APO は、MFX として形式変換を実行する場合があります。   
-   APO は、次の形式を出力する必要があります。 
    -   16 kHz、mono、FLOAT。
-   必要に応じて、オーディオキャプチャプロセスを拡張するカスタム APOs を設計します。 詳細については、「 [Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)」を参照してください。

ハードウェアオフロードキーワードスポットライン (HW KWS) WoV の要件
- HW KWS WoV は、S0 の動作中にサポートされています。また、S0 スリープ状態は、"最新のスタンバイ" とも呼ばれます。  
- HW KWS WoV は S3 からはサポートされていません。  

**AEC**

AEC は、バーストオーディオがキャプチャされたときに DSP によって実行されるか、ソフトウェア APO を介して後で実行できます。 KWS バーストデータを含むソフトウェア AEC を実行するには、バーストデータがキャプチャされた時点から対応するループバックオーディオを用意する必要があります。 これを行うために、バースト出力に対してカスタムオーディオ形式が作成されました。これにより、ループバックオーディオはバーストオーディオデータになります。 Microsoft AEC APO は、このインターリーブ形式を認識し、それを使用して AEC を実行できます。 詳細については、「 [KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION](https://docs.microsoft.com/en-us/windows-hardware/drivers/audio/ksproperty-interleavedaudio-formatinformation)」を参照してください。 

**検査**

[Voice Activation Manager 2 テスト](https://docs.microsoft.com/en-us/windows-hardware/test/hlk/testref/5119a80f-8aae-49bb-aa59-8eaa7e7b1fad)を使用して、 [KSPROPSETID_SOUNDDETECTOR2](kspropsetid-sounddetector2.md)プロパティの HW サポートを検証します。

## <a name="span-idsample_code_overviewspansample-code-overview"></a><span id="sample_code_overview"></span>サンプルコードの概要

SYSVAD 仮想オーディオアダプターサンプルの一部として、GitHub で音声アクティベーションを実装するオーディオドライバーのサンプルコードがあります。 [このコード](https://github.com/Microsoft/Windows-driver-samples/blob/master/audio/sysvad/)を開始点として使用することをお勧めします。 

SYSVAD サンプルオーディオドライバーの詳細については、「[サンプルオーディオドライバー](https://docs.microsoft.com/en-us/windows-hardware/drivers/audio/sample-audio-drivers)」を参照してください。

## <a name="span-idkeyword_recognition_system_informationspankeyword-recognition-system-information"></a><span id="keyword_recognition_system_information"></span>キーワード認識システム情報

**音声アクティブ化オーディオスタックのサポート**

音声のアクティブ化を有効にするためのオーディオスタック外部インターフェイスは、音声プラットフォームとオーディオドライバーの通信パイプラインとして機能します。 外部インターフェイスは、3つの部分に分かれています。

- [*イベント検出デバイスドライバーインターフェイス (DDI)* ](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/eventdetectoroemadapter/nn-eventdetectoroemadapter-ieventdetectoroemadapter)。 イベント検出デバイスドライバーインターフェイスは、HW キーワード取り組ま (KWS) の構成とを行います。  また、ドライバーは検出イベントをシステムに通知するためにも使用されます。
- [*Ievent 探知 OEM ADAPTER DLL*](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/eventdetectoroemadapter/nn-eventdetectoroemadapter-ieventdetectoroemadapter)。 この DLL は、キーワード検出を支援するために OS によって使用されるドライバー固有の不透明なデータを調整する COM インターフェイスを実装します。
-  *Wavert ストリーミングの機能強化*。 拡張機能により、オーディオドライバーは、バッファー内のオーディオデータをキーワード検出からバーストすることができます。

**オーディオエンドポイントのプロパティ**

オーディオエンドポイントグラフの作成は正常に行われます。 グラフは、リアルタイムキャプチャよりも高速に処理できるように準備されています。 キャプチャされたバッファーのタイムスタンプは true のままです。 具体的には、タイムスタンプには、過去にキャプチャされてバッファーに記録されたデータが正しく反映され、バースティングになります。

**操作の理論**

ドライバーは、キャプチャデバイスの KS フィルターを通常どおりに公開します。 このフィルターでは、いくつかの KS プロパティと、検出イベントを構成、有効化、および通知するための KS イベントがサポートされています。 また、フィルターには、キーワードのスポット留め (KWS) pin として識別される追加の pin ファクトリも含まれています。 この pin は、キーワードのスポット留めからオーディオをストリーミングするために使用されます。

プロパティは次のとおりです: [ **KSPROPSETID_SoundDetector2**](kspropsetid-sounddetector2.md)

すべての[**KSPROPSETID_SoundDetector2**](kspropsetid-sounddetector2.md)プロパティは、 [KSSOUNDDETECTORPROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty)データ構造体を使用して呼び出されます。 このデータ構造には、KSK プロパティと、設定、リセット、検出などを行うキーワードのイベント id が含まれています。

- サポートされているキーワードの種類- [**Ksk プロパティ\_SOUNDDETECTOR\_パターン**](https://docs.microsoft.com/en-us/windows-hardware/drivers/audio/ksproperty-sounddetector)。 このプロパティは、検出されるキーワードを構成するためにオペレーティングシステムによって設定されます。
-   キーワードパターン Guid- [**Ksk プロパティ\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](https://docs.microsoft.com/en-us/windows-hardware/drivers/audio/ksproperty-sounddetector)の一覧。 このプロパティは、サポートされているパターンの種類を識別する Guid の一覧を取得するために使用されます。
- [ **\_SOUNDDETECTOR 器\_武装**](https://docs.microsoft.com/en-us/windows-hardware/drivers/audio/ksproperty-sounddetector)しています。 この読み取り/書き込みプロパティは、検出されたかどうかを示す単純なブール値です。 OS は、キーワード検出機能を利用するようにこれを設定します。 OS はこれをオフにしてオフにできます。 キーワードパターンが設定され、キーワードが検出された後に、ドライバーによって自動的にクリアされます。 (OS は rearm する必要があります)。
- 一致結果- [**Ksproperty\_サウンド検出**](ksproperty-sounddetector-reset.md)機能を使用して、起動時にサウンド検出機能をリセット\_ます。

キーワード検出時には、KSNOTIFICATIONID_SoundDetector を含む PNP 通知が送信されます。 注: これは KSEvent ではなく、IoReportTargetDeviceChangeAsynchronous を介してペイロードと共に送信される PNP イベントです。

KSNOTIFICATIONID_SoundDetector は、次に示すように、ksmedia. h で定義されています。

```
// The payload of this notification is a SOUNDDETECTOR_DETECTIONHEADER
#define STATIC_KSNOTIFICATIONID_SoundDetector\
    0x6389d844, 0xbb32, 0x4c4c, 0xa8, 0x2, 0xf4, 0xb4, 0xb7, 0x7a, 0xfe, 0xad
DEFINE_GUIDSTRUCT("6389D844-BB32-4C4C-A802-F4B4B77AFEAD", KSNOTIFICATIONID_SoundDetector);
#define KSNOTIFICATIONID_SoundDetector DEFINE_GUIDNAMED(KSNOTIFICATIONID_SoundDetector)
```

**操作のシーケンス**

*システムの起動*

1. OS は[**Ksk プロパティ\_SOUNDDETECTOR\_リセット**](ksproperty-sounddetector-reset.md)して以前の検出状態をクリアし、すべての検出機能をリセットして以前のパターンセットをクリアします。
2. OS クエリの[**Ksproperty\_SOUNDDETECTOR 器\_パターン**](https://docs.microsoft.com/en-us/windows-hardware/drivers/audio/ksproperty-sounddetector)を使用して、イベント検出用の OEM アダプターの clsid を取得します。
3. OS は、イベント検出機能の oem アダプターを使用して、サポートされているキーワードと言語の一覧を取得します。
4. ドライバーによって送信されたカスタム PNP 通知を OS が登録する
5. OS は、必要なキーワードパターンを設定します。
6. OS によって検出されました

**内部のドライバーとハードウェアの操作**

検出が実行されている間、ハードウェアは小さい FIFO バッファーでオーディオデータを継続的にキャプチャしてバッファリングできます。 (この FIFO バッファーのサイズは、このドキュメントの外部の要件によって決まりますが、通常は数秒から数秒である場合があります)。検出アルゴリズムは、このバッファーを介してデータストリームを処理します。 ドライバーとハードウェアの設計は、キーワードが検出されるまで、ドライバーとハードウェア間の相互作用がなく、"アプリケーション" プロセッサに割り込みが発生しないようにするためのものです。 これにより、他のアクティビティが存在しない場合に、システムがより低い電力状態になる可能性があります。

ハードウェアがキーワードを検出すると、割り込みが生成されます。 ドライバーが割り込みを処理するのを待機している間、ハードウェアはオーディオをバッファーにキャプチャし続け、キーワードが失われた後にデータがバッファーに格納されないようにします。

**キーワードのタイムスタンプ**

キーワードを検出した後、すべての音声アクティブ化ソリューションは、キーワードの開始前に 1.6 s を含む、すべての音声キーワードをバッファーする必要があります。 オーディオドライバーは、ストリーム内のキーフレーズの先頭と末尾を識別するタイムスタンプを提供する必要があります。

キーワードの開始/終了タイムスタンプをサポートするために、dsp ソフトウェアでは、DSP クロックに基づいて内部的にイベントのタイムスタンプを行うことが必要になる場合があります。 キーワードが検出されると、DSP ソフトウェアはドライバーとやり取りして KS イベントを準備します。 ドライバーと DSP ソフトウェアでは、DSP タイムスタンプを Windows パフォーマンスカウンター値にマップする必要があります。 これを行う方法は、ハードウェア設計に固有のものです。 考えられる解決策の1つは、ドライバーが現在のパフォーマンスカウンターを読み取り、現在の DSP タイムスタンプに対してクエリを実行し、現在のパフォーマンスカウンターを再び読み取り、パフォーマンスカウンターと DSP 時間の相関関係を推定することです。 関連付けを指定すると、ドライバーは、キーワード DSP タイムスタンプを Windows パフォーマンスカウンターのタイムスタンプにマップできます。


## <a name="span-idievent_detectorspanievent-detector-oem-adapter-interface"></a><span id="ievent_detector"></span>IEvent 探知 OEM アダプターインターフェイス

OEM は、OS とドライバーの仲介役として機能する COM オブジェクトの実装を提供します。これは、 [**Ksk プロパティ\_SOUNDDETECTOR\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-patterns)によって、オーディオドライバーに書き込まれて読み取られる不透明なデータを計算または解析するのに役立ちます。および[**Ksproperty\_SOUNDDETECTOR\_matchresult**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-matchresult)です。

COM オブジェクトの CLSID は、Ksproperty によって返される検出パターン型の GUID であり、 [**SUPPORTEDPATTERNS\_\_SOUNDDETECTOR 器**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-supportedpatterns)によって返されます。 OS は、パターン型 GUID を渡す CoCreateInstance を呼び出して、キーワードパターン型と互換性のある適切な COM オブジェクトをインスタンス化し、オブジェクトの IEventDetectorOemAdapter インターフェイスでメソッドを呼び出します。

**COM スレッドモデルの要件**

OEM の実装では、任意の COM スレッドモデルを選択できます。

**IEventDetectorOemAdapter**

インターフェイスのデザインでは、オブジェクトの実装をステートレスな状態に保ちます。 つまり、実装では、メソッド呼び出しの間に状態を格納する必要がありません。 実際、内部C++クラスは、一般に COM オブジェクトを実装するために必要な以外のメンバー変数を必要としません。

**メソッド**

次のメソッドを実装します。

-   [**IEventDetectorOemAdapter::BuildArmingPatternData**](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-buildarmingpatterndata)
-   [**IEventDetectorOemAdapter:: ComputeAndAddUserModelData**](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-computeandaddusermodeldata)
-   [**IEventDetectorOemAdapter:: GetCapabilities**](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-getcapabilities)
-   [**IEventDetectorOemAdapter::GetCapabilitiesForLanguage**](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-getcapabilitiesforlanguage)
-   [**IEventDetectorOemAdapter::P arseDetectionResultData**](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-parsedetectionresultdata)
-   [**IEventDetectorOemAdapter::ReportOSDetectionResult**](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-parsedetectionresultdata)
-   [**IEventDetectorOemAdapter::VerifyUserEventData**](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-verifyusereventdata)

## <a name="span-idwavert_enhancementsspanspan-idwavert_enhancementsspanspan-idwavert_enhancementsspanwavert-enhancements"></a><span id="WAVERT_Enhancements"></span><span id="wavert_enhancements"></span><span id="WAVERT_ENHANCEMENTS"></span>WAVERT の機能強化

ミニポートインターフェイスは、WaveRT ミニポートドライバーによって実装されるように定義されています。 これらのインターフェイスは、オーディオドライバーを簡略化し、OS オーディオパイプラインのパフォーマンスと信頼性を向上させるか、新しいシナリオをサポートするメソッドを提供します。 ドライバーがバッファーサイズの制約の静的式を OS に提供できるように、新しい PnP デバイスインターフェイスプロパティが定義されています。

**バッファーサイズ**

ドライバーは、OS、ドライバー、およびハードウェア間でオーディオデータを移動するときに、さまざまな制約の下で動作します。 これらの制約は、メモリとハードウェア間でデータを移動する物理ハードウェアトランスポート、またはハードウェアまたは関連する DSP 内の信号処理モジュールによって発生することがあります。

HW-KWS ソリューションでは、少なくとも100ミリ秒から200ミリ秒までのオーディオキャプチャサイズをサポートする必要があります。

ドライバーは、KS ストリーミングピンがある KS フィルターの KSCATEGORY\_AUDIO PnP デバイスインターフェイスで、DEVPKEY\_KsAudio\_PacketSize\_Constraints デバイスプロパティを設定することによって、バッファーサイズの制約を表します。 このプロパティは、KS フィルターインターフェイスが有効になっている間は有効で安定した状態を維持する必要があります。 OS は、ドライバーへのハンドルを開き、ドライバーでを呼び出すことなく、いつでもこの値を読み取ることができます。

**DEVPKEY\_KsAudio\_PacketSize\_制約**

DEVPKEY\_KsAudio\_PacketSize\_Constraints プロパティ値には、物理ハードウェアの制約を説明する[**Ksk audio\_PacketSize\_制約**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)構造が含まれます (つまり、WaveRT バッファーからオーディオハードウェアにデータを転送する。 構造体には、0個以上の[**Ksaudio\_PACKETSIZE\_PROCESSINGMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)の配列が含まれています。これは、任意のシグナル処理モードに固有の制約を記述する制約構造\_ます。 ドライバーは、 [**Pcregiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)呼び出す前にこのプロパティを設定します。それ以外の場合は、そのストリームのピンに対して KS フィルターインターフェイスを有効にします。

**IMiniportWaveRTInputStream**

ドライバーは、ドライバーから OS へのオーディオデータフローをより適切に調整するために、このインターフェイスを実装します。 このインターフェイスがキャプチャストリームで使用可能な場合、OS はこのインターフェイスのメソッドを使用して WaveRT バッファー内のデータにアクセスします。 詳細については、「 [ **IMiniportWaveRTInputStream:: GetReadPacket** 」を参照してください。](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)

**IMiniportWaveRTOutputStream**

WaveRT ミニポートは、必要に応じて、このインターフェイスを実装して、OS からの書き込みの進行状況を通知し、正確なストリーム位置を返します。 詳細については、「 [**IMiniportWaveRTOutputStream:: SetWritePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-setwritepacket)」、「 [**IMiniportWaveRTOutputStream:: Getoutputstreamプレゼンテーション位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-getoutputstreampresentationposition)」、および「 [**IMiniportWaveRTOutputStream:: getpacketcount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-getpacketcount)」を参照してください。

**パフォーマンスカウンターのタイムスタンプ**

いくつかのドライバールーチンは、デバイスによってサンプルがキャプチャまたは表示される時刻を反映する Windows パフォーマンスカウンターのタイムスタンプを返します。

複雑な DSP パイプラインと信号処理があるデバイスでは、正確なタイムスタンプを計算することは困難であるため、熟考を行う必要があります。 タイムスタンプには、サンプルが OS と DSP 間で転送された時刻を単に反映させることはできません。

- DSP 内で、一部の内部 DSP ウォールクロックを使用してサンプルタイムスタンプを追跡します。
- ドライバーと DSP の間で、Windows パフォーマンスカウンターと DSP の壁面クロックの間の相関関係を計算します。 この手順は、非常に単純な (ただし、正確ではありませんが) 非常に複雑なものや斬新なもの (より正確です) の範囲です。
- シグナル処理アルゴリズムまたはパイプラインまたはハードウェアトランスポートに起因する一定の遅延を考慮します。ただし、これらの遅延が考慮されない場合は除きます。

**バースト読み取り操作**

ここでは、バースト読み取りの OS とドライバーの相互作用について説明します。 バースト読み取りは、ドライバーが[**IMiniportWaveRTInputStream:: GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)関数を含むパケットベースのストリーミング wavert モデルをサポートしている限り、音声ライセンス認証シナリオの外部で発生する可能性があります。

2つのバースト例の読み取りシナリオについて説明します。 1つのシナリオでは、ピン留めカテゴリ[ **\_KSNODETYPE AUDIO\_KEYWORDDETECTOR**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)を持つピンがミニポートでサポートされている場合、ドライバーはキーワードが検出されると、データのキャプチャと内部バッファリングを開始します。 別のシナリオでは、 [**IMiniportWaveRTInputStream:: GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)を呼び出すことによって、OS がデータを十分に読み取ることができない場合は、必要に応じて、ドライバーが wastbuffer の外部にあるデータを内部的にバッファーできます。

KSSTATE\_実行される前にキャプチャされたデータをバーストするには、ドライバーはバッファーされたキャプチャデータと共に正確なサンプルタイムスタンプ情報を保持する必要があります。 タイムスタンプは、キャプチャしたサンプルのサンプリングの瞬間を識別します。

1. ストリームが KSK 状態に遷移し\_実行された後、ドライバーは、既に使用可能なデータがあるため、バッファー通知イベントを直ちに設定します。
2. このイベントでは、OS は GetReadPacket () を呼び出して、使用可能なデータに関する情報を取得します。

    」を参照します。 ドライバーは、有効なキャプチャされたデータのパケット番号を返します (KSK\_状態から KSK 状態に移行した後の最初のパケットの場合は 0\_実行)。これにより、OS は WaveRT バッファー内のパケット位置とパケット位置を取得できます。ストリームの先頭からの相対。

    b. また、ドライバーは、パケット内の最初のサンプルのサンプリングの瞬間に対応するパフォーマンスカウンターの値を返します。 このパフォーマンスカウンターの値は、ハードウェアまたはドライバー内でバッファーに格納されているキャプチャデータの量によっては、比較的古いものであることに注意してください。

    c. 未読のバッファーデータがある場合は、次のいずれかの方法でドライバーを使用できます。 i. は、そのデータを WaveRT バッファーの使用可能な領域 (GetReadPacket から返されたパケットによって使用されていない領域) に直ちに転送し、さらにデータに対しては true を返し、このルーチンから戻る前にバッファー通知イベントを設定します。 または、ii です。 プログラムハードウェアを使用して、次のパケットを WaveRT バッファーの使用可能な領域にバーストし、さらにデータがある場合は false を返し、後で転送の完了時にバッファーイベントを設定します。
3. OS は、GetReadPacket () によって返された情報を使用して、WaveRT バッファーからデータを読み取ります。
4. OS は、次のバッファー通知イベントを待機します。 ドライバーが手順 (2c) でバッファー通知を設定した場合、待機はすぐに終了する可能性があります。
5. ドライバーが、ステップ (2c) でイベントをすぐに設定しなかった場合、キャプチャされたデータを WaveRT バッファーに転送した後、ドライバーによってイベントが設定され、OS が読み取ることができるようになります。
6. (2) にアクセスします。

[**KSNODETYPE\_audio\_KEYWORDDETECTOR**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)キーワード検出ピンの pin では、ドライバーは、少なくとも返り秒のオーディオデータに対して十分な内部バーストバッファリングを割り当てる必要があります。 OS が pin のストリームを作成できなかった場合、バッファーがオーバーフローする前に、ドライバーは内部バッファリングアクティビティを終了し、関連付けられているリソースを解放します。

## <a name="span-idwake_on_voicespanspan-idwake_on_voicespanspan-idwake_on_voicespanwake-on-voice"></a><span id="Wake_on_Voice"></span><span id="wake_on_voice"></span><span id="WAKE_ON_VOICE"></span>電話でのスリープ状態

"WoV" を使用すると、ユーザーは "こんにちは Contoso" のような特定のキーワードを言って、音声認識エンジンをアクティブ化し、低電力状態から全電源状態にすることができます。

この機能を使用すると、デバイスがアイドル状態で画面がオフになっている間、デバイスは常にユーザーの音声をリッスンできます。 これは、通常のマイクの録音と比較して電力消費がはるかに少ないリッスンモードに起因します。 WoV を使用すると、音声アシスタントからの応答をハンドフリー方式で呼び出すことができます。 "こんにちは Contoso さんは次の予定です" のような、チェーン化された音声句を使用できます。

オーディオスタックは、ウェイクアップデータ (スピーカー ID、キーワードトリガー、信頼レベルのコンテキスト情報) の通信、およびキーワードが検出されたことを対象のクライアントへの通知を行います。

**最新のスタンバイシステムでの検証**

システムのアイドル状態からの WoV は、最新のスタンバイ[wake On 音声基本テスト (AC 電源)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/69df7cf2-6024-4eee-92ee-1506480614ee)と、 [HLK](https://docs.microsoft.com/windows-hardware/test/hlk/)の[DC 電源の最新のスタンバイ wake on 音声基本テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/614ffb93-eced-45ab-bf7b-e09291a97fd2)を使用して、[最新のスタンバイ](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)システムで検証できます。 これらのテストでは、システムがハードウェアのキーワードを使用しているかどうかを確認します (HW-KWS)。最も深いランタイムアイドルプラットフォームの状態 (DRIPS) に入ることができます。また、システム再開の待機時間が1秒以下の場合は、音声コマンドの最新のスタンバイから復帰できます。