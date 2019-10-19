---
title: オーディオ処理オブジェクトのアーキテクチャ
description: オーディオ処理オブジェクト (APOs) は、Windows オーディオストリーム用のカスタマイズ可能なソフトウェアベースのデジタル信号処理を提供します。
ms.assetid: 2F57B4C7-8C83-4DDF-BFAF-B9308752E91D
ms.date: 10/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: f4b69cb56c80ec3f9be2c66bc4e880d01b17848f
ms.sourcegitcommit: 36b7db40d5a91d8726feb2e2d9d4ece1fb484051
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72591012"
---
# <a name="audio-processing-object-architecture"></a>オーディオ処理オブジェクトのアーキテクチャ

オーディオ処理オブジェクト (APOs) は、Windows オーディオストリーム用のカスタマイズ可能なソフトウェアベースのデジタル信号処理を提供します。

## <a name="span-idaudio_processing_objects_overviewspanspan-idaudio_processing_objects_overviewspanspan-idaudio_processing_objects_overviewspanaudio-processing-objects-overview"></a><span id="Audio_Processing_Objects_Overview"></span><span id="audio_processing_objects_overview"></span><span id="AUDIO_PROCESSING_OBJECTS_OVERVIEW"></span>オーディオ処理オブジェクトの概要

Windows では、Oem およびサードパーティのオーディオハードウェア製造元が、オーディオドライバーの付加価値機能の一部としてカスタムデジタル信号処理効果を組み込むことができます。 これらの効果は、ユーザーモードのシステム効果のオーディオ処理オブジェクト (APOs) としてパッケージ化されます。

オーディオ処理オブジェクト (APOs) は、Windows オーディオストリームに対してソフトウェアベースのデジタル信号処理を提供します。 APO は、特定のデジタル信号処理 (DSP) 効果を提供するために記述されたアルゴリズムを含む COM ホストオブジェクトです。 この機能は、"オーディオ効果" として非公式に知られています。 APOs には、グラフィック equalizers、リバーブ、tremolo、音響エコーキャンセル (AEC)、自動ゲイン制御 (AGC) などがあります。 APOs は、COM ベースのリアルタイムのインプロセスオブジェクトです。

このドキュメントに記載されている説明と用語は、ほとんどの場合、出力デバイスを指し**て    ます**。 ただし、テクノロジは対称であり、基本的には入力デバイスに対して逆に機能します。

**ソフトウェア APOs とハードウェア DSP**

ハードウェアデジタル信号プロセッサ (DSP) は、特殊なマイクロプロセッサ (または SIP ブロック) で、デジタル信号処理の運用上のニーズに合わせて最適化されたアーキテクチャを備えています。 専用のハードウェアにオーディオ処理を実装することと、ソフトウェア APO を使用するという大きな利点があります。 1つの利点は、ハードウェアによって実装された DSP で CPU 使用量と関連する電力消費が少なくなる可能性があることです。

他にも考慮すべき長所と欠点があります。これは、ソフトウェアベースの APO を実装する前に検討する必要があるプロジェクトの目標と制約に固有です。

ソフトウェアベースの効果は、ストリームの初期化時にソフトウェアデバイスパイプに挿入されます。 これらのソリューションは、メイン CPU 上でのすべての影響処理を行い、外部ハードウェアに依存することはありません。 この種のソリューションは、ドライバーとハードウェアが生の処理のみをサポートしている場合に、HDAudio、USB、Bluetooth デバイスなどの従来の Windows オーディオソリューションに最適です。 未処理処理の詳細については、「[オーディオシグナル処理モード](audio-signal-processing-modes.md)」を参照してください。

**ハードウェア DSP のプロキシ APO**

ハードウェア DSP に適用されたすべての効果は、プロキシ APO 経由でアドバタイズされる必要があります。 Microsoft では、既定のプロキシ APO (MsApoFxProxy) を提供しています。 Microsoft が提供する APO を使用するには、このプロパティセットとプロパティがサポートされている必要があります。

-   [KSPROPSETID \_AudioEffectsDiscovery](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audioeffectsdiscovery)
-   [KSK プロパティ \_AUDIOEFFECTSDISCOVERY \_EFFECTSLIST](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn457706(v=vs.85))

必要に応じて、独自のプロキシ APO を実装することもできます。

**Windows 提供 (システム) APOs**

Windows では、さまざまなオーディオ効果を提供する APOs の既定のセットがインストールされます。 システムが提供する APO 効果の一覧については、「[オーディオ信号処理モード](audio-signal-processing-modes.md)」を参照してください。

Oem は、指定されたすべてのシステムを含めることも、一部またはすべてをカスタム APOs に置き換えることもできます。

**カスタム APOs**

カスタム APOs を作成して、オーディオ効果を追加することによって Windows オーディオエクスペリエンスを向上させることができます。

OEM には、Windows の出荷時に提供される Windows APOs と custom APOs の任意の組み合わせを含めることができます。

カスタム APO は、デバイスを購入した後にオーディオエクスペリエンスを向上させるために、OEM またはサードパーティによってインストールすることができます。 ユーザーが標準の INF ファイルを使用してオーディオデバイスドライバーをインストールすると、システムの APOs に自動的にアクセスできるようになります。 独立系ハードウェアベンダー (Ihv) と相手先ブランド供給業者 (Oem) は、Microsoft クラスドライバーを引き続き使用しながら、追加のカスタムシステム効果を提供できます。 そのためには、DSP アルゴリズムを APOs としてパッケージ化し、標準の INF ファイルを変更して、オーディオエンジンのシグナル処理グラフに APOs を挿入します。

カスタム APOs を作成する方法の詳細については、「[オーディオ処理オブジェクトの実装](implementing-audio-processing-objects.md)」を参照してください。

**カスタム APO サポートアプリ**

ユーザーがカスタム APO に関連付けられている設定を構成できるようにするには、ハードウェアサポートアプリを作成することをお勧めします。 詳細については、「[ハードウェアサポートアプリ (HSA): ドライバー開発者向けの手順](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-support-app--hsa--steps-for-driver-developers)」を参照してください。

**カスタム APO テストと要件**

Microsoft HLK は、APOs で使用できるテストを提供します。 オーディオテストの詳細については、「[デバイス. オーディオ](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj123955(v=vs.85))テスト」および「[デバイスのオーディオテスト](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124726(v=vs.85))」を参照してください。

この2つのテストは、APOs を使用する場合に特に便利です。

[オーディオの効果検出の確認 (手動)-認定](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn456312(v=vs.85))

[SysFX テスト](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124017(v=vs.85))

APOs のサポートに関するオーディオの要件については、「[デバイスのオーディオ要件](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/deviceaudio-requirements)」を参照してください。

**カスタム APO ツールとユーティリティ**

"オーディオ効果検出サンプル" を使用して、利用可能なオーディオ効果を調べることができます。 このサンプルでは、オーディオデバイスのレンダリングとキャプチャに関するオーディオ効果を照会する方法と、オーディオ効果を使用して変更を監視する方法を示します。 SDK サンプルの一部として含まれており、次のリンクを使用してダウンロードできます。

[オーディオエフェクト検出のサンプル](https://code.msdn.microsoft.com/windowsapps/Audio-effects-discovery-5fd65c15)

**アプリケーションオーディオ効果の認識**

アプリケーションでは、Api を呼び出して、どのオーディオ効果がシステムで現在アクティブであるかを判断することができます。 オーディオ効果認識 Api の詳細については、「 [Audiorendereffects manager クラス](https://docs.microsoft.com/uwp/api/Windows.Media.Effects.AudioRenderEffectsManager)」を参照してください。

## <a name="span-idaudio_processing_objects_architecturespanspan-idaudio_processing_objects_architecturespanspan-idaudio_processing_objects_architecturespanaudio-processing-objects-architecture"></a><span id="Audio_Processing_Objects_Architecture"></span><span id="audio_processing_objects_architecture"></span><span id="AUDIO_PROCESSING_OBJECTS_ARCHITECTURE"></span>オーディオ処理オブジェクトのアーキテクチャ

**オーディオ効果の配置**

オーディオエフェクトには、APOs として実装されている3つの異なる場所があります。 これらは、ストリーム効果 (SFX)、モード効果 (MFX)、およびエンドポイント効果 (EFX) に含まれています。

**ストリーム効果 (SFX)**

ストリーム効果 APO には、すべてのストリームに対する効果のインスタンスがあります。 ストリーム効果は、特定のモードではミックス (render) の前または t (capture) の後にあり、ミキサーの前にチャネル数を変更するために使用できます。 ストリームの効果は、生のストリームには使用されません。

一部のバージョンの Windows は、最適化として、RAW モードでは SFX または MFX APOs を読み込みません。

-   Windows 8.1 は RAW SFX または RAW MFX を読み込みません
-   Windows 10 は未加工の MFX を読み込みますが、RAW SFX は読み込みません

**Mode 効果 (MFX)**

モードの効果 (MFX) は、同じモードにマップされているすべてのストリームに適用されます。 モードの効果は、指定されたモードでは、ミックス (レンダリング) の後、またはすべてのモードの t (キャプチャ) の後に適用されます。 ストリーム効果の詳細を必要としないシナリオ固有の効果や効果は、ここに配置する必要があります。 周期性や形式などの同じ特性を共有する複数のストリームに対して1つのインスタンスが存在するため、モード効果を使用する方が効率的です。

**エンドポイント効果 (EFX)**

エンドポイント効果 (EFX) は、同じエンドポイントを使用するすべてのストリームに適用されます。 エンドポイント効果は、未加工のストリームに対しても常に適用されます。 つまり、混合 (レンダリング) の後、またはすべてのモードの t (キャプチャ) の前にあります。 エンドポイントの効果は、注意して使用する必要があります。また、不明な場合は、効果をモード領域に配置する必要があります。 エンドポイント領域に配置する必要がある効果には、スピーカーの保護とスピーカーの補正があります。

この図は、Windows 10 のストリーム (SFX)、モード (MFX)、およびエンドポイント (EFX) の影響の可能性のある場所を示しています。

![windows 10 のストリーム、モード、およびエンドポイント効果の配置を示す図](images/audio-apo-software-effects-summary.png)

**複数のカスタム APO 効果**

さまざまなアプリケーションで動作するように、複数の APO ベースの効果を構成することができます。

この図は、複数のアプリケーションが、ストリーム、モード、およびエンドポイントの APO 効果の複数の組み合わせにアクセスする方法を示しています。 すべての APOs は COM ベースであり、ユーザーモードで実行されます。 このシナリオでは、どのような効果もハードウェアまたはカーネルモードで実行されていません。

![複数のアプリケーションが、ストリーム、モード、およびエンドポイントの apo 効果の複数の組み合わせにアクセスする方法を示す図](images/audio-apo-software-effects-1.png)

このページの一番下にあるスクロールバーを使用して、この図のすべてを**表示   You こと**ができます。

**レンダリングとキャプチャのためのソフトウェアモード効果とハードウェアエンドポイント効果**

この図は、ソフトウェアモードの効果と、レンダリングとキャプチャに対するハードウェアエンドポイントの効果を示しています。

![レンダリングとキャプチャに関するソフトウェアモードの効果とハードウェアエンドポイントの効果を示す図](images/audio-apo-software-mode-effects-and-hardware-endpoint-effects-2.png)

**ハードウェアに影響する DSP 装備システム**

この図は、ハードウェアへの影響を実装する DSP 搭載システムを示しています。 このシナリオでは、ハードウェアに実装されている効果をアプリに通知するためにプロキシ APO を作成する必要があります。

![ハードウェアへの影響を実装する dsp 搭載システムを示す図。](images/audio-apo-dsp-equipped-system-with-hardware-effects-3.png)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)  
