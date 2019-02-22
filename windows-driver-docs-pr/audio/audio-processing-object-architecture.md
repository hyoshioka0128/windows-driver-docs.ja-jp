---
title: オーディオ処理オブジェクト アーキテクチャ
description: オーディオ処理オブジェクト (APOs) は、Windows オーディオ ストリームのカスタマイズ可能なソフトウェア ベースのデジタル信号処理を提供します。
ms.assetid: 2F57B4C7-8C83-4DDF-BFAF-B9308752E91D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd53e46e57783d59ae626835ca0c8ce5f80ad0d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553317"
---
# <a name="audio-processing-object-architecture"></a>オーディオ処理オブジェクト アーキテクチャ


オーディオ処理オブジェクト (APOs) は、Windows オーディオ ストリームのカスタマイズ可能なソフトウェア ベースのデジタル信号処理を提供します。

## <a name="span-idaudioprocessingobjectsoverviewspanspan-idaudioprocessingobjectsoverviewspanspan-idaudioprocessingobjectsoverviewspanaudio-processing-objects-overview"></a><span id="Audio_Processing_Objects_Overview"></span><span id="audio_processing_objects_overview"></span><span id="AUDIO_PROCESSING_OBJECTS_OVERVIEW"></span>オーディオ処理オブジェクトの概要


Windows には、オーディオ ドライバーの付加価値機能の一部としてカスタムのデジタル信号処理の効果を含めるには、Oem およびサード パーティ製のオーディオ ハードウェアの製造元が使用できます。 これらの効果は、ユーザー モード システム エフェクト オーディオ処理オブジェクト (APOs) としてパッケージ化されます。

オーディオ処理オブジェクト (APOs) は、Windows オーディオ ストリームのソフトウェア ベースのデジタル信号処理を提供します。 APO は、特定のデジタル信号処理 (DSP) 効果を提供に書き込まれるアルゴリズムを含む COM ホスト オブジェクトです。 この機能は、「オーディオ効果」として非公式呼ばれます。 以下の例には、グラフィックの調整、リバーブ、トレモロ、アコースティック エコー キャンセル (AEC)、および自動ゲイン制御 (AGC) が含まれます。 APOs は、COM ベース、リアルタイム、プロセス内のオブジェクトです。

**注**  説明およびこのドキュメントでの用語は出力デバイスのほとんどを指します。 ただし、テクノロジは対称であり、入力デバイスの逆の順序で本質的に動作します。

 

**ソフトウェア APOs vs します。ハードウェア DSP**

ハードウェア デジタル シグナル プロセッサ (DSP) は特殊なマイクロプロセッサ (SIP ブロック)、デジタル信号処理の運用ニーズに合わせて最適のアーキテクチャです。 ソフトウェア APO を使用すると、専用ハードウェアでオーディオの処理を実装するために重要な利点があります。 利点の 1 つは DSP を実装する、CPU 使用率と関連付けられている電力消費する可能性があります、ハードウェアを使用します。

あるその他の長所と短所、考慮すべきプロジェクトの目標に特定し、APO ベースのソフトウェアを実装する前に考慮する制約します。

ソフトウェア ベースの効果は、ソフトウェア デバイス パイプ ストリームの初期化時に挿入されます。 これらのソリューションは、メインの CPU の処理のすべての効果を行い、外部のハードウェアに依存しません。 この種のソリューションは、生の処理のみをサポート、ドライバーとハードウェアと HDAudio、USB、Bluetooth デバイスなどの従来の Windows オーディオ ソリューションに最適。 生の処理の詳細については、次を参照してください。[オーディオ信号の処理モード](audio-signal-processing-modes.md)します。

**プロキシ APO ハードウェア DSP**

DSP 必要 APO プロキシ経由で提供されるように、ハードウェアで、効果が適用されます。 Microsoft では、既定のプロキシ APO (MsApoFxProxy.dll) を提供します。 APO、Microsoft を使用するには、このプロパティのセットとプロパティをサポートする必要があります。

-   [KSPROPSETID\_AudioEffectsDiscovery](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audioeffectsdiscovery)
-   [KSPROPERTY\_AUDIOEFFECTSDISCOVERY\_EFFECTSLIST](https://msdn.microsoft.com/library/windows/hardware/dn457706)

必要に応じて、APO 独自のプロキシを実装することができます。

**Windows (システム) のパスワードを指定します。**

Windows では、別のオーディオ エフェクトの番号を提供する、APOs の既定のセットをインストールします。 システムの一覧には、APO 効果が提供されている、参照してください[オーディオ信号の処理モード](audio-signal-processing-modes.md)します。

Oem は、すべてのシステム指定のパスワードを含めるか、それらの一部またはすべてをカスタム APOs に置き換えます。

**カスタム APOs**

その他のオーディオ エフェクトを追加することで、Windows オーディオ エクスペリエンスを強化するためにカスタム パスワードを作成することになります。

OEM は、Windows が出荷されるときに、指定された Windows APOs とカスタム APOs の任意の組み合わせを含めることができます。

カスタム APO は、デバイスを購入した後に、オーディオのエクスペリエンスを向上させるには、OEM またはサード パーティによってインストールできます。 ユーザーは、標準の INF ファイルを使用して、オーディオ デバイス ドライバーをインストールするときに、自動的にシステムの APOs へのアクセスがあります。 独立系ハードウェア ベンダー (Ihv) および相手先ブランド供給 (Oem) は、Microsoft のクラス ドライバーを使用中にその他のカスタム システムの効果を提供できます。 それによって、APOs として DSP アルゴリズムをパッケージ化してオーディオ エンジンの信号処理のグラフにその画像を挿入する、標準の INF ファイルを変更します。

カスタム APOs」を参照して作成の詳細については[オーディオ処理オブジェクトを実装する](implementing-audio-processing-objects.md)します。

**カスタム APO プロパティ UI**

デスクトップ Pc では、カスタム APO に関連付けられている設定を構成するユーザーを許可するには、カスタム APO プロパティ ページを作成できます。 このカスタム APO ページ使用できるユーザーに Windows の標準のオーディオ設定の拡張機能として。

SYSVAD オーディオ サンプルには、例カスタム APO コントロール サンプルが含まれています。 このスクリーン ショットでは、SYSVAD オーディオ スワップ APO サンプルのプロパティ ページを示します。

![sysvad オーディオ スワップ apo コントロールのサンプルのスピーカーのプロパティ ページのスクリーン ショット](images/audio-apo-speaker-properties.png)

APO を追加する方法の詳細については、ダイアログ パネルが参照、 [APO 効果の構成 UI を実装する](implementing-a-ui-for-configuring-apo-effects.md)します。

**カスタム APO テストと要求**

Microsoft HLK APOs で使用できるテストを提供します。 オーディオのテストでは、「の詳細については[Device.Audio テスト](https://msdn.microsoft.com/library/windows/hardware/jj123955.aspx)と[Device.Audio テスト](https://msdn.microsoft.com/library/windows/hardware/jj124726.aspx)します。

これら 2 つのテストは APOs を使用する場合に、特に役立ちます。

[オーディオ EffectsDiscovery (手動) - 証明書を確認します。](https://msdn.microsoft.com/library/windows/hardware/dn456312.aspx)

[SysFX Test](https://msdn.microsoft.com/library/windows/hardware/jj124017.aspx)

APOs をサポートするためのオーディオ要件については、次を参照してください。 [Device.Audio 要件](https://msdn.microsoft.com/library/windows/hardware/jj134354.aspx)します。

**カスタム APO ツールとユーティリティ**

使用可能なオーディオ効果を探索するのに、"オーディオ エフェクト検出 Sample"を使用できます。 このサンプルでは、オーディオ効果のレンダーをクエリして、オーディオ デバイスをキャプチャする方法とオーディオ エフェクトを使用した変更を監視する方法を示します。 SDK サンプルの一部として含めると、このリンクを使用してダウンロードできます。

[オーディオ エフェクトの探索のサンプル](https://code.msdn.microsoft.com/windowsapps/Audio-effects-discovery-5fd65c15)

**アプリケーションは、オーディオ効果の認識**

アプリケーションでは、どのオーディオ効果は、システム上で現在アクティブかを判断する Api を呼び出す機能があります。 オーディオ エフェクト認識 Api の詳細については、次を参照してください。 [AudioRenderEffectsManager クラス](https://msdn.microsoft.com/library/windows/apps/windows.media.effects.audiorendereffectsmanager.aspx)します。

## <a name="span-idaudioprocessingobjectsarchitecturespanspan-idaudioprocessingobjectsarchitecturespanspan-idaudioprocessingobjectsarchitecturespanaudio-processing-objects-architecture"></a><span id="Audio_Processing_Objects_Architecture"></span><span id="audio_processing_objects_architecture"></span><span id="AUDIO_PROCESSING_OBJECTS_ARCHITECTURE"></span>オーディオ処理オブジェクト アーキテクチャ


**オーディオ効果の配置**

APOs として実装されているオーディオ効果の 3 つの場所があります。 これらは、Stream の効果 (SFX)、モードの効果 (MFX) とエンドポイントの効果 (EFX) です。

**Stream の効果 (SFX)**

ストリーム エフェクト APO には、すべてのストリームの効果のインスタンスがあります。 Stream の効果は、特定のモードの tee (キャプチャ) の前後にミックス (レンダー) と、ミキサーの前に、チャネルの数を変更するために使用できます。 Stream の効果は、生のストリームに対しては使用されません。

一部のバージョンの Windows、最適化として、RAW モードで SFX または MFX APOs をロードしません。

-   Windows 8.1 では、生の SFX または生 MFX は読み込まれません
-   Windows 10 は、生 MFX ですがない生 SFX を読み込みます

**モードの効果 (MFX)**

モードの効果 (MFX) は、同じモードにマップされているすべてのストリームに適用されます。 モードの効果は、tee (キャプチャ) が混在 (レンダー) する前に特定のモードの前に、または後 (レンダー) ミックスに、またはすべてのモードの tee (キャプチャ) 後に適用されます。 すべてのシナリオの特定の効果またはストリーム効果の詳細が必要ない効果をここに配置してください。 周期性と形式のような同じ特性を共有する複数のストリームを 1 つのインスタンスであるために、モードの効果を使用する power 効率的になります。

**エンドポイントの効果 (EFX)**

エンドポイントの効果 (EFX) は、同じエンドポイントを使用するすべてのストリームに適用されます。 生のストリームにも、エンドポイント効果が常に適用されています。 これは、すべてのモードの tee (キャプチャ) 前に、または後 (レンダー) の組み合わせがあります。 不明な効果がモードの領域内の場所をなるべきときに、慎重には、エンドポイントの効果を使用してください。 エンドポイント領域に配置する必要がありますをいくつかの効果には、スピーカーの保護とスピーカーの補正です。

この図では、Windows 10 用のストリーム (SFX)、モード (MFX) およびエンドポイント (EFX) の効果の可能な場所を示します。

![windows 10 で、ストリーム、モード、およびエンドポイントの効果の配置を示す図します。](images/audio-apo-software-effects-summary.png)

**複数のカスタム APO 効果**

さまざまなアプリケーションを使用する複数のベース APO 効果を構成することになります。

この図は、ストリーム、モード、およびエンドポイントの APO 効果の複数の組み合わせをアクセスできる複数のアプリケーションを示しています。 すべて、APOs は、COM ベースし、ユーザー モードで実行します。 このシナリオでハードウェアまたはカーネル モードでを実行している効果なし。

![複数のアプリケーションがストリーム、モード、およびエンドポイントの apo 効果の複数の組み合わせにアクセスできるかを示す図](images/audio-apo-software-effects-1.png)

**注**  この図のすべてを表示するこのページの一番下にスクロール バーを使用することができます。

 

**ソフトウェアのモードの効果とレンダリングとキャプチャのハードウェアのエンドポイントの効果**

この図は、ソフトウェア モードの効果とレンダリングとキャプチャのハードウェアのエンドポイントの効果を示しています。

![ソフトウェアのモードの効果とレンダリングとキャプチャのハードウェアのエンドポイントの効果を示す図](images/audio-apo-software-mode-effects-and-hardware-endpoint-effects-2.png)

**DSP には、ハードウェアの効果を持つシステムが搭載されています。**

この図は、ハードウェアの効果を実装する DSP が搭載されているシステムを示しています。 このシナリオでは、プロキシ APO はハードウェアに実装されている効果のアプリを通知するために作成されます。

![dsp を示す図では、ハードウェアの効果を実装するシステムが搭載されています。](images/audio-apo-dsp-equipped-system-with-hardware-effects-3.png)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)  
[APO 効果を構成するための UI を実装します。](implementing-a-ui-for-configuring-apo-effects.md)  



