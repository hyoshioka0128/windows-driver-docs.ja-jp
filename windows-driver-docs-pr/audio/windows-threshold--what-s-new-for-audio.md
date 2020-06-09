---
title: Windows 10 オーディオドライバーの新機能
description: このトピックでは、Windows 10 の audio の新機能の概要について説明します。
ms.assetid: 9005966A-CCC2-478C-9221-56007B7FADFB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 690b278052dd2c46a558208d8961a4f4eaa913be
ms.sourcegitcommit: 8097a09d2f989a9b3dca250c4e2ffd4cec2172e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84563154"
---
# <a name="windows-10-whats-new-for-audio-drivers"></a>Windows 10: オーディオドライバーの新機能


このトピックでは、Windows 10 の audio の新機能の概要について説明します。

## <a name="span-idfeature_summaryspanspan-idfeature_summaryspanspan-idfeature_summaryspanfeature-summary"></a><span id="Feature_Summary"></span><span id="feature_summary"></span><span id="FEATURE_SUMMARY"></span>機能の概要


Windows 10 の新しいオーディオ機能を次に示します。

-   [オーディオ モジュール通信の実装](implementing-audio-module-communication.md)

-   [低待機時間のオーディオの改善](#lowlatency)

-   [シグナル処理モードとオーディオカテゴリ](#signalprocessing)

-   [ハードウェアオフロード APO 効果](#hardwareoffloaded)

-   [Cortana 音声のアクティブ化](#cortanavoice)

-   [オーディオ用 Windows ユニバーサルドライバー](#windowsuniversal)

-   [オーディオドライバーのリソース管理](#resourcemanagement)

-   [オーディオドライバーの PNP 再調整](#pnprebalance)

## <a name="span-idlowlatencyspanspan-idlowlatencyspanspan-idlowlatencyspanlow-latency-audio-improvements"></a><span id="LowLatency"></span><span id="lowlatency"></span><span id="LOWLATENCY"></span>低待機時間のオーディオの改善


オーディオ待機時間とは、サウンドが作成されてから聞こえたときまでの遅延です。 次のようないくつかの主要なシナリオでは、オーディオの待機時間を短くすることが非常に重要です。

-   Pro オーディオ
-   音楽の作成とミックス
-   Skype などの通信
-   仮想および拡張された現実
-   ゲーム

デバイスの待機時間の合計は、次のコンポーネントの待機時間の合計です。

-   オペレーティング システム
-   オーディオ処理オブジェクト
-   オーディオドライバー
-   オーディオハードウェア

Windows 10 では、OS の待機時間を短縮するために作業が行われました。 ドライバーを変更しないと、Windows 10 のアプリケーションでは 4.5-16ms の待機時間が減少します。 さらに、小さなバッファーを使用してオーディオデータを処理する新しい低待機時間 DDIs を利用するようにドライバーが更新されている場合は、待機時間がさらに短縮されます。 ドライバーが3ミリ秒オーディオバッファーをサポートしている場合、ラウンドトリップの待機時間は ~ 10 ミリ秒です。

![アプリ、オーディオエンジンドライバー、および h/w を示す低待機時間オーディオスタック図](images/low-latency-audio-stack-diagram-1.png)

オーディオスタックでは、ユーザーのシナリオに基づいて待機時間と電力のトレードオフを最適化するために、複数のパケットサイズと動的なパケットサイズ変更がサポートされています。 さらに、優先順位の高いストリーム (電話など) が専用のリソースを持つようにするために、ストリームに優先順位が付けられます。

オーディオドライバーで低待機時間をサポートするために、Windows 10 には次の3つの新機能が用意されています。

1. \[必須 \] 各モードでサポートされている最小バッファーサイズを宣言します。
2. \[省略可能ですが、 \] ドライバーと OS の間のデータフローの調整を向上させることをお勧めします。
3. \[省略可能ですが、 \] 低待機時間シナリオで OS によって保護できるように、ドライバーリソース (割り込み、スレッド) を登録することをお勧めします。
詳細については、「[低待機時間のオーディオ](low-latency-audio.md)」を参照してください。

## <a name="span-idsignalprocessingspanspan-idsignalprocessingspanspan-idsignalprocessingspansignal-processing-modes-and-audio-categories"></a><span id="SignalProcessing"></span><span id="signalprocessing"></span><span id="SIGNALPROCESSING"></span>シグナル処理モードとオーディオカテゴリ


**シグナル処理モード**

ドライバーは、各デバイスのサポートされているオーディオシグナル処理モードを宣言します。

オーディオカテゴリ (アプリケーションによって選択されます) は、(ドライバーによって定義された) オーディオモードにマップされます。 Windows では、7つのオーディオ信号処理モードを定義します。 Oem と Ihv は、どのモードを実装するかを決定できます。 これらのモードの概要を次の表に示します。

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
<td align="left">Raw</td>
<td align="left">両方</td>
<td align="left"><p>Raw モードでは、ストリームにシグナル処理を適用しないことを指定します。</p>
<p>アプリケーションは、まったく手を加えずに独自のシグナル処理を実行する未加工ストリームを要求できます。</p></td>
</tr>
<tr class="odd">
<td align="left">Default</td>
<td align="left">両方</td>
<td align="left"><p>このモードは、既定のオーディオ処理を定義します。</p></td>
</tr>
<tr class="even">
<td align="left">映像</td>
<td align="left">レンダー</td>
<td align="left">ムービーオーディオ再生</td>
</tr>
<tr class="odd">
<td align="left">用紙</td>
<td align="left">両方</td>
<td align="left">音楽オーディオ再生 (ほとんどのメディアストリームでは既定)</td>
</tr>
<tr class="even">
<td align="left">スピーチ</td>
<td align="left">キャプチャ</td>
<td align="left">人間の声のキャプチャ (Cortana への入力など)</td>
</tr>
<tr class="odd">
<td align="left">接続</td>
<td align="left">両方</td>
<td align="left">VOIP のレンダーとキャプチャ (例: Skype、Lync)</td>
</tr>
<tr class="even">
<td align="left">警告</td>
<td align="left">レンダー</td>
<td align="left">着信音、アラーム、アラートなど</td>
</tr>
</tbody>
</table>

 

オーディオデバイスドライバは、少なくとも Raw モードまたは Default モードをサポートしている必要があります。 追加モードのサポートはオプションです。

音声、ムービー、音楽、および通信用の専用モード。 オーディオドライバーでは、ストリームの種類に基づいて、さまざまな種類のオーディオ形式と処理を定義できます。

**オーディオカテゴリ**

次の表は、Windows 10 のオーディオカテゴリを示しています。

オーディオストリームの使用状況についてシステムに通知するために、アプリケーションでは、特定のオーディオストリームカテゴリを使用してストリームにタグを付けることができます。 Windows 10 では、9つのオーディオストリームカテゴリがあります。

|                |                                                                                                       |
|----------------|-------------------------------------------------------------------------------------------------------|
| **カテゴリ**   | **説明**                                                                                       |
| 映画\*        | ムービー、ダイアログ付きビデオ (ForegroundOnlyMedia を置換)                                              |
| メディア\*        | メディア再生の既定のカテゴリ (BackgroundCapableMedia を置換)                                 |
| ゲームチャット\*    | ユーザー間のゲーム内通信 (Windows 10 の新しいカテゴリ)                                      |
| 音声\*       | 音声入力 (例: personal assistant) と出力 (ナビゲーションアプリなど) (Windows 10 の新しいカテゴリ) |
| 通信 | VOIP、リアルタイムチャット                                                                                  |
| 警告         | アラーム、リングトーン、通知                                                                       |
| サウンド効果  | ビープ音、dings、その他                                                                                     |
| ゲームメディア     | ゲームミュージック                                                                                         |
| ゲーム効果   | ボールのバウンス、車のエンジンサウンド、箇条書きなど                                                      |
| その他          | 未カテゴリのストリーム                                                                                 |

 

\*Windows 10 の新。

詳細については、「[オーディオ信号処理モード](audio-signal-processing-modes.md)」と「[オーディオ処理オブジェクトのアーキテクチャ](audio-processing-object-architecture.md)」を参照してください。

## <a name="span-idhardwareoffloadedspanspan-idhardwareoffloadedspanspan-idhardwareoffloadedspanhardware-offloaded-apo-effects"></a><span id="HardwareOffloaded"></span><span id="hardwareoffloaded"></span><span id="HARDWAREOFFLOADED"></span>ハードウェアオフロード APO 効果


Windows 10 では、ハードウェアオフロードの APO 効果がサポートされています。 APOs はオフロード pin の上に読み込むことができます。 これにより、ソフトウェアとハードウェアの両方でオーディオ処理を行うことができます。 また、処理は動的に変更される可能性があります。 十分なハードウェアリソースがあり、DSP の負荷が増加したときにソフトウェア APO に戻されると、一部またはすべての処理をソフトウェア APO から DSP に移動できます。

詳細については、「[ハードウェアオフロード APO 効果の実装](implementing-hardware-offloaded-apo-effects.md)」を参照してください。

## <a name="span-idcortanavoicespanspan-idcortanavoicespanspan-idcortanavoicespancortana-voice-activation---wake-on-voice"></a><span id="CortanaVoice"></span><span id="cortanavoice"></span><span id="CORTANAVOICE"></span>Cortana ボイスアクティベーション-音声でのスリープ解除

Cortana は、2013の Microsoft BUILD Developer カンファレンスで、パーソナルアシスタントテクノロジを初めて使い始めました。 音声のアクティブ化は、ユーザーが特定の語句 ("こんにちは Cortana") を伝えて、さまざまなデバイスの電源状態から音声認識エンジンを呼び出せるようにする機能です。 "Cortana" ボイスアクティベーション (VA) 機能を使用すると、ユーザーは自分の声を使って、アクティブなコンテキスト (つまり、現在画面に表示されているもの) の外部で操作 (Cortana など) をすばやく行うことができます。 この機能は、画面がオフになっている場合、アイドル状態のとき、または完全にアクティブになっている場合のシナリオを対象としています。 ハードウェアでバッファリングがサポートされている場合、ユーザーはキーフレーズとコマンドフレーズを一緒にチェーンすることができます。 これにより、エンドツーエンドの wake on のユーザーエクスペリエンスが向上します。 詳細については、「[音声ライセンス認証](voice-activation.md)」を参照してください。

## <a name="span-idwindowsuniversalspanspan-idwindowsuniversalspanspan-idwindowsuniversalspanwindows-universal-drivers-for-audio"></a><span id="WindowsUniversal"></span><span id="windowsuniversal"></span><span id="WINDOWSUNIVERSAL"></span>オーディオ用 Windows ユニバーサルドライバー


Windows 10 でサポートされているドライバーモデルは、PC と 2: 1 と Windows 10 のスマートフォン用および小型の画面タブレット用です。 つまり、Ihv は、ドライバーを1つのプラットフォームで開発し、そのドライバーをすべてのデバイス (デスクトップ、ラップトップ、タブレット、携帯電話) で動作させることができます。 その結果、開発時間とコストが削減されます。

ユニバーサルオーディオドライバーを開発するには、次のツールを使用します。

1. Visual Studio 2015: 新しいドライバー設定では、"ターゲットプラットフォーム" を "Universal" に設定して、マルチプラットフォームドライバーを作成できます。
2. APIValidator: これは、ドライバーが universal であるかどうかを確認し、更新が必要な呼び出しを強調表示する WDK ツールです。
3. GitHub のオーディオサンプル: sysvad と SwapAPO は、ユニバーサルドライバーに変換されました。
GitHub サンプルコードの詳細とポインターについては、「[ユニバーサル Windows Drivers For Audio](audio-universal-drivers.md)」を参照してください。

## <a name="span-idresourcemanagementspanspan-idresourcemanagementspanspan-idresourcemanagementspanresource-management-for-audio-drivers"></a><span id="ResourceManagement"></span><span id="resourcemanagement"></span><span id="RESOURCEMANAGEMENT"></span>オーディオドライバーのリソース管理


低コストのモバイルデバイスで優れたオーディオエクスペリエンスを作成する際の1つの問題は、一部のデバイスでさまざまな同時実行制約があることです。 たとえば、デバイスが同時に最大6つのオーディオストリームを再生でき、2つのオフロードストリームのみをサポートする可能性があります。 モバイルデバイスにアクティブな通話がある場合、デバイスがサポートするオーディオストリームは2つだけである可能性があります。 デバイスがオーディオをキャプチャしている場合、デバイスは最大4つのオーディオストリームのみを再生できます。

Windows 10 には、高優先度のオーディオストリームや携帯電話通話を再生できるように、同時実行の制約を表現するメカニズムが含まれています。 システムに十分なリソースがない場合は、低優先度のストリームが終了します。 このメカニズムは、デスクトップやノート pc にない携帯電話やタブレットでのみ使用できます。

詳細については、「 [Audio Hardware Resource Management](audio-hardware-resource-management.md)」を参照してください。

## <a name="span-idpnprebalancespanspan-idpnprebalancespanspan-idpnprebalancespanpnp-rebalance-for-audio-drivers"></a><span id="PNPRebalance"></span><span id="pnprebalance"></span><span id="PNPREBALANCE"></span>オーディオドライバーの PNP 再調整


PNP の再調整は、メモリリソースを再割り当てする必要がある特定の PCI シナリオで使用されます。 この場合、一部のドライバーはアンロードされ、別のメモリ位置に再読み込みされるため、連続した空きメモリ領域が作成されます。 再調整は、主に次の2つのシナリオで発生します。

1. PCI hotplug: ユーザーがデバイスに接続し、PCI バスに新しいデバイス用のドライバーを読み込むための十分なリソースがありません。 このカテゴリに分類されるデバイスの例として、Thunderbolt icon、USB-C、および NVME ストレージがあります。 このシナリオでは、追加する追加のデバイスをサポートするために、メモリリソースを再編成して統合する必要があります (再分配)。
2. PCI 再測定可能なバー: デバイスのドライバーがメモリに正常に読み込まれた後、追加のリソースを要求します。 デバイスの例としては、ハイエンドグラフィックスカードや記憶装置などがあります。
詳細については、「 [PortCls Audio Drivers の PnP 再調整の実装](implement-pnp-rebalance-for-portcls-audio-drivers.md)」を参照してください。

 

 




