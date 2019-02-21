---
title: Windows 10 のオーディオ ドライバーには新機能
description: このトピックでは、高レベルの Windows 10 用のオーディオの新機能新機能の概要を説明します。
ms.assetid: 9005966A-CCC2-478C-9221-56007B7FADFB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 502b99e61f97df9585478d4a02fda524acdb72fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531840"
---
# <a name="windows-10-whats-new-for-audio-drivers"></a>Windows 10:オーディオ ドライバーには新機能


このトピックでは、高レベルの Windows 10 用のオーディオの新機能新機能の概要を説明します。

## <a name="span-idfeaturesummaryspanspan-idfeaturesummaryspanspan-idfeaturesummaryspanfeature-summary"></a><span id="Feature_Summary"></span><span id="feature_summary"></span><span id="FEATURE_SUMMARY"></span>機能の概要


Windows 10 の新しいオーディオ機能を示します。

-   [オーディオのモジュールの通信を実装します。](implementing-audio-module-communication.md)

-   [低待機時間のオーディオ機能強化](#lowlatency)

-   [信号処理モードとオーディオのカテゴリ](#signalprocessing)

-   [ハードウェア オフロード APO 効果](#hardwareoffloaded)

-   [Cortana 音声をアクティブ化](#cortanavoice)

-   [オーディオの Windows ユニバーサル ドライバー](#windowsuniversal)

-   [オーディオ ドライバーのリソースの管理](#resourcemanagement)

-   [オーディオ ドライバーの PNP のバランス調整](#pnprebalance)

## <a name="span-idlowlatencyspanspan-idlowlatencyspanspan-idlowlatencyspanlow-latency-audio-improvements"></a><span id="LowLatency"></span><span id="lowlatency"></span><span id="LOWLATENCY"></span>低待機時間のオーディオ機能強化


オーディオの待機時間は、その時点のサウンドの間の遅延が作成され、聞いたときに。 オーディオの待ち時間を持つことは、次のようないくつかの主要なシナリオ、非常に重要です。

-   Pro オーディオ
-   音楽の作成との混合
-   Skype などの通信
-   仮想および Augmented Reality
-   ゲーム

デバイスの合計待機時間は、次のコンポーネントの待機時間の合計を示します。

-   オペレーティング システム
-   オーディオ処理オブジェクト
-   オーディオ ドライバー
-   オーディオ ハードウェア

Windows 10 では、作業は OS で待機時間を減らす行われました。 ドライバー変更なしで Windows 10 のアプリケーションに 4.5 16 ミリ秒の待ち時間が発生します。 さらに、新しい低待機時間の小さなバッファーを使用して、オーディオ データを処理する Ddi 活用するために、ドライバーが更新された場合、待機時間が引き下げられますより。 場合ドライバー サポート ミリ秒オーディオ バッファー ラウンドト リップの待機時間は約 10 ミリ秒とします。

![アプリ、オーディオ エンジン ドライバーおよびハードウェアを示す短い待機時間オーディオ スタックの図](images/low-latency-audio-stack-diagram-1.png)

オーディオ スタックは、複数のパケット サイズと待機時間と、ユーザーのシナリオに基づく power 間のトレードオフを最適化するために、動的なパケットのサイズ変更をサポートします。 さらに、ストリームは優先順位を設定、優先度の高いストリーム (電話など) が専用のリソースをことを保証するためにします。

低待機時間をサポートするために、オーディオ ドライバーの順番は、Windows 10 は、次の 3 つの新機能を提供します。

1. \[必須\]各モードでサポートされている最小バッファー サイズを宣言します。
2. \[省略可、ただし推奨\]ドライバーと OS の間のデータ フローの連携を強化します。
3. \[省略可、ただし推奨\]ドライバー リソース (割り込み、スレッド) を登録し、低待機時間シナリオでの OS で保護するようにします。
詳細については、次を参照してください。[低待機時間のオーディオ](low-latency-audio.md)します。

## <a name="span-idsignalprocessingspanspan-idsignalprocessingspanspan-idsignalprocessingspansignal-processing-modes-and-audio-categories"></a><span id="SignalProcessing"></span><span id="signalprocessing"></span><span id="SIGNALPROCESSING"></span>信号処理モードとオーディオのカテゴリ


**信号処理モード**

ドライバーは、サポートされているオーディオ信号の各デバイスの処理モードを宣言します。

オーディオのカテゴリ (アプリケーションで選択) は、オーディオのモード (ドライバーによって定義される) にマップされます。 Windows では、7 つのオーディオ信号処理モードを定義します。 Oem および ihv 側では、どのモードを実装するかを判断できます。 モードは、次の表にまとめます。

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
<td align="left"><strong>説明</strong></td>
</tr>
<tr class="even">
<td align="left">直接</td>
<td align="left">どちらもオン</td>
<td align="left"><p>Raw モードでは、存在しないことをストリームに適用される、信号処理を指定します。</p>
<p>アプリケーションは完全に変更されず、生のストリームを要求し、独自の信号処理を実行できます。</p></td>
</tr>
<tr class="odd">
<td align="left">Default</td>
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

 

オーディオ デバイス ドライバーは、少なくとも Raw または既定のモードをサポートする必要があります。 追加モードをサポートするは省略可能です。

音声、ビデオ、音楽、および通信専用モードです。 オーディオ ドライバーでは、オーディオ形式のさまざまな種類を定義できなくなり、ストリームの種類に基づいて、処理します。

**オーディオのカテゴリ**

次の表には、Windows 10 でのオーディオのカテゴリが表示されます。

アプリケーションでは、オーディオ ストリームの使用方法について、システムを通知するために、ストリームを特定のオーディオ ストリームのカテゴリとタグ付けするオプションがあります。 Windows 10 では、9 つのオーディオ ストリームのカテゴリがあります。

|                |                                                                                                       |
|----------------|-------------------------------------------------------------------------------------------------------|
| **カテゴリ**   | **説明**                                                                                       |
| ビデオ\*        | ムービー、ビデオのダイアログ ボックス (ForegroundOnlyMedia が置き換えられます)                                              |
| メディア\*        | メディアの再生 (BackgroundCapableMedia が置き換えられます) の既定のカテゴリ                                 |
| ゲームのチャット\*    | ユーザー (Windows 10 の新しいカテゴリ) 間のゲーム内の通信                                      |
| 音声認識\*       | 音声入力 (例: パーソナル アシスタント) と出力 (例: アプリのナビゲーション) (Windows 10 の新しいカテゴリ) |
| Communications | VOIP、リアルタイムのチャット                                                                                  |
| アラート         | アラーム、着信音、通知                                                                       |
| サウンド効果  | ビープ音など                                                                                     |
| ゲームのメディア     | ゲームの音楽                                                                                         |
| ゲーム効果   | 車のエンジン音、箇条書きなどをはずむボールです。                                                      |
| その他          | カテゴリ化されていないストリーム                                                                                 |

 

\* Windows 10 の新機能です。

詳細については、次を参照してください。[オーディオ信号の処理モード](audio-signal-processing-modes.md)と[オーディオ処理オブジェクト アーキテクチャ](audio-processing-object-architecture.md)します。

## <a name="span-idhardwareoffloadedspanspan-idhardwareoffloadedspanspan-idhardwareoffloadedspanhardware-offloaded-apo-effects"></a><span id="HardwareOffloaded"></span><span id="hardwareoffloaded"></span><span id="HARDWAREOFFLOADED"></span>ハードウェア オフロード APO 効果


Windows 10 には、ハードウェアのオフロード APO 効果がサポートされています。 APOs は、オフロードの暗証番号 (pin) の上に読み込むことができます。 これにより、ソフトウェアとハードウェアの両方で行われるオーディオの処理。 さらに、処理を動的に変更できます。 一部またはすべての処理を十分なハードウェア リソースがある場合に、ソフトウェア APO から DSP に移動してに戻すソフトウェア APO DSP に負荷が増えたときにすることができます。

詳細については、次を参照してください。[ハードウェア オフロード APO 効果の実装](implementing-hardware-offloaded-apo-effects.md)します。

## <a name="span-idcortanavoicespanspan-idcortanavoicespanspan-idcortanavoicespancortana-voice-activation---wake-on-voice"></a><span id="CortanaVoice"></span><span id="cortanavoice"></span><span id="CORTANAVOICE"></span>Cortana 音声のアクティブ化 - 音声でウェイク アップ

Cortana、パーソナル アシスタントのテクノロジは、2013 Microsoft BUILD Developer Conference での最初の demonstarted をしました。 音声をアクティブ化は、コルタナさん」- 特定の語句を言うことにより、さまざまなデバイスの電源の状態からの音声認識エンジンを起動できる機能です。 コルタナさん」音声アクティベーション (VA) 機能では、自分の音声を使用して、自分のアクティブなコンテキストを使用して、(つまり、現在にあるものの画面) の外部でエクスペリエンス (Cortana など) を迅速に情報交換することができます。 機能はシナリオの対象となる画面がオフ、アイドル状態、または完全に有効になります。 ハードウェアでは、バッファリングをサポートする場合のユーザー、連結できます、キー フレーズとコマンドの語句。 これにより、ユーザーのボイス エクスペリエンスでエンド ツー エンドのスリープ解除が向上します。 詳細については、次を参照してください。[音声をアクティブ化](voice-activation.md)します。

## <a name="span-idwindowsuniversalspanspan-idwindowsuniversalspanspan-idwindowsuniversalspanwindows-universal-drivers-for-audio"></a><span id="WindowsUniversal"></span><span id="windowsuniversal"></span><span id="WINDOWSUNIVERSAL"></span>オーディオの Windows ユニバーサル ドライバー


Windows 10 では、スマート フォンやタブレットの小さな画面の PC の 2:1 の動作の 1 つのドライバー モデル、および Windows 10 をサポートします。 つまり、Ihv が 1 つのプラットフォームでは、そのドライバーを開発および、そのドライバーがすべてのデバイス (デスクトップ、ラップトップ、タブレット、携帯電話) で動作します。 開発時間の短縮とコストになります。

ユニバーサルのオーディオ ドライバーを開発するには、次のツールを使用します。

1. Visual Studio 2015:新しいドライバーの設定は、マルチプラット フォームのドライバーを作成する"Universal"に設定する「ターゲット プラットフォーム」を許可します。
2. APIValidator:これは、ドライバーがユニバーサルおよび更新する必要がある呼び出しを強調表示かどうかをチェックする WDK ツールです。
3. GitHub でのオーディオ サンプル:Sysvad と SwapAPO ユニバーサル ドライバーに変換されました。
詳細と GitHub のサンプル コードへのポインターは、次を参照してください。[オーディオのユニバーサル Windows ドライバー](audio-universal-drivers.md)します。

## <a name="span-idresourcemanagementspanspan-idresourcemanagementspanspan-idresourcemanagementspanresource-management-for-audio-drivers"></a><span id="ResourceManagement"></span><span id="resourcemanagement"></span><span id="RESOURCEMANAGEMENT"></span>オーディオ ドライバーのリソースの管理


低コストのモバイル デバイスでオーディオの良好なエクスペリエンスを作成する 1 つの課題は、一部のデバイスにさまざまな同時実行の制約があることです。 たとえば、2 のみをサポートするストリームをオフロードすると、デバイスが同時に最大 6 のオーディオ ストリームを再生のみできますです。 モバイル デバイスでアクティブな電話呼び出しがあるときに、デバイスが 2 つだけのオーディオ ストリームをサポートしていること。 デバイスでは、オーディオのキャプチャ時に、デバイスはのみに最大 4 つのオーディオ ストリームを再生できます。

Windows 10 には、優先度の高いオーディオ ストリームと携帯電話の呼び出しができるを再生することを保証する同時実行の制約を表現するためのメカニズムが含まれています。 システムが十分なリソースを持たない場合は、低優先度のストリームが終了します。 このメカニズムでは、携帯電話とタブレットではなくデスクトップやラップトップで使用できるのみです。

詳細については、次を参照してください。[オーディオ ハードウェア リソースの管理](audio-hardware-resource-management.md)します。

## <a name="span-idpnprebalancespanspan-idpnprebalancespanspan-idpnprebalancespanpnp-rebalance-for-audio-drivers"></a><span id="PNPRebalance"></span><span id="pnprebalance"></span><span id="PNPREBALANCE"></span>オーディオ ドライバーの PNP のバランス調整


PNP 再調整はシナリオで使用特定 PCI を再割り当てするメモリ リソースが必要があります。 その場合は、一部のドライバーが、アンロードし、連続したメモリの空き領域を作成するには、さまざまなメモリの場所に再度読み込まれます。 2 つの主なシナリオでは、再調整が引き起こされます。

1. PCI ホットプラグ:ユーザーはデバイスをプラグインし、PCI バスには、新しいデバイスのドライバーの読み込みには、十分なリソースはありません。 このカテゴリに分類されるデバイスのいくつかの例には、Thunderbolt、USB C および NVME ストレージが含まれます。 このシナリオでメモリ リソースを再配置し、統合 (rebalanced) サポートする必要があるされる追加のデバイス。
2. PCI サイズ バー:デバイスのドライバーのメモリに読み込みが成功した後、その他のリソースを要求します。 デバイスのいくつかの例には、ハイエンドなグラフィックス カードと記憶装置が含まれます。
詳細については、次を参照してください。[実装 PortCls オーディオ ドライバーの PnP 再調整](implement-pnp-rebalance-for-portcls-audio-drivers.md)します。

 

 




