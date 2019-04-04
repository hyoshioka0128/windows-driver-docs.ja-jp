---
title: WavePci ミニポート ドライバーにおけるパフォーマンスの問題
description: WavePci ミニポート ドライバーにおけるパフォーマンスの問題
ms.assetid: 785fd743-0c78-44cd-95bf-1f961aa414b5
keywords:
- WavePci パフォーマンスの問題の WDK オーディオ
- サービス メカニズム WDK のオーディオのストリーム
- ハードウェアの割り込みの WDK オーディオ
- 割り込みサービス ルーチン WDK オーディオ
- Isr WDK オーディオ
- タイマー Dpc WDK オーディオ
- 最適化 WDK オーディオの一時停止/取得
- IPreFetchOffset
- 同期プリミティブの WDK オーディオ
- IPinCount
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ccbbd144dc9645f35c9a56da6188327eb6b66ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574558"
---
# <a name="performance-issues-for-a-wavepci-miniport-driver"></a>WavePci ミニポート ドライバーにおけるパフォーマンスの問題


## <span id="performance_issues_for_a_wavepci_miniport_driver"></span><span id="PERFORMANCE_ISSUES_FOR_A_WAVEPCI_MINIPORT_DRIVER"></span>


これらの原則に従って、システムのオーディオ ドライバーのパフォーマンスに影響を大幅に削減できます。

-   通常の操作中に実行されるコードを最小限に抑えます。

-   必要な場合にのみコードを実行します。

-   合計システム リソースの消費量 (だけでなく CPU を読み込み中) を検討してください。

-   コードの速度とサイズを最適化します。

さらに、WavePci ミニポート ドライバーはオーディオ デバイスに固有のいくつかのパフォーマンスの問題に対処する必要があります。 次の説明は、オーディオ キャプチャもに、推奨される手法のいくつか適用されますが、オーディオのレンダリングの問題を主に扱います。

### <a name="span-idstreamservicingmechanismsspanspan-idstreamservicingmechanismsspanspan-idstreamservicingmechanismsspanstream-servicing-mechanisms"></a><span id="Stream_Servicing_Mechanisms"></span><span id="stream_servicing_mechanisms"></span><span id="STREAM_SERVICING_MECHANISMS"></span>Stream のメカニズムをサービス

パフォーマンスの最適化を説明する前にいくつかのバック グラウンドでは、ストリームを提供するための WavePci しくみを理解する必要があります。

波を処理するか、レンダリング、ストリームをキャプチャ、オーディオ デバイスでは、ミニポート ドライバーで一定の間隔でサービスが必要です。 新しいマッピングがストリームの使用可能な場合は、ドライバーは、ストリームの DMA キューにそれらのマッピングを追加します。 ドライバーも、キューから削除するが、既に処理されたすべてのマッピング。 マッピングについては、[WavePci 待機時間](wavepci-latency.md)を参照してください。

サービスを実行するミニポート ドライバーを提供するか、*遅延プロシージャ呼び出し (DPC)* または割り込みサービス ルーチン (ISR) システム タイマーまたは DMA ドリブン割り込みに間隔を設定するかどうかによって異なります。 後者の場合、DMA ハードウェアでは、ある程度の転送が完了するとデータをストリーミングする場合、割り込みを毎回が通常トリガーします。

DPC されるたびに、ISR 実行、または修理するストリームが必要なことを決定します。 呼び出してストリームをサービス ISR、DPC、 [ **IPortWavePci::Notify** ](https://msdn.microsoft.com/library/windows/hardware/ff536918)メソッド。 このメソッドは、呼び出しのパラメーターとして型のオブジェクトでは、ストリームのサービス グループ[IServiceGroup](https://msdn.microsoft.com/library/windows/hardware/ff536994)します。 **通知**メソッドは、サービス グループの[ **RequestService** ](https://msdn.microsoft.com/library/windows/hardware/ff537009)メソッド (を参照してください**IServiceSink::RequestService**)。

サービス グループ オブジェクトには、サービスのシンクは、型のオブジェクトのグループが含まれています。 [IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)します。 [IServiceGroup](https://msdn.microsoft.com/library/windows/hardware/ff536994) IServiceSink から派生し、両方のインターフェイスが[ **RequestService** ](https://msdn.microsoft.com/library/windows/hardware/ff537009)メソッド。 ときに、 [**通知**](https://msdn.microsoft.com/library/windows/hardware/ff536918)メソッドは、サービス グループの**RequestService**メソッドを呼び出して、このサービス グループ応答、 **RequestService** 、グループ内の各サービスのメソッドのシンクします。

ストリームのサービス グループには、ポート ドライバーは、ストリームの作成の直後に続く、サービスのグループに追加するには少なくとも 1 つのサービス シンクが含まれています。 ポート ドライバー呼び出し、ミニポート ドライバーの[ **IMiniportWavePci::NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536735)サービス グループへのポインターを取得します。 サービスのシンクの[ **RequestService** ](https://msdn.microsoft.com/library/windows/hardware/ff537009)メソッドは、ポート ドライバーのストリームに固有のサービスのルーチンです。 このルーチンは、次を行います。

-   呼び出す、ミニポート ドライバーの[ **IMiniportWavePciStream::Service** ](https://msdn.microsoft.com/library/windows/hardware/ff536731)メソッド。

-   前回サービス ルーチンの実行後に、位置またはクロック イベント ストリームの保留中の新しくをトリガーします。

説明したよう[KS イベント](https://msdn.microsoft.com/library/windows/hardware/ff567643)ストリームは、特定の位置またはクロックが特定のタイムスタンプに達したときに達したときに通知できるクライアントを登録できます。 [ **NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536735)メソッドをケース ポート ドライバー設定、独自のタイマーをオフにするには、そのサービス ルーチン呼び出しの間の間隔をサービスのグループを指定していないのオプションがあります。

ように、 [ **NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536735)メソッド、ミニポート ドライバーの[ **IMiniportWavePci::Init** ](https://msdn.microsoft.com/library/windows/hardware/ff536734)メソッドはサービスのグループへのポインターも出力. 次の**Init**ポート ドライバーの呼び出しは、サービスのグループにサービスがシンクを追加します。 この特定のサービスのシンクには、全体として、フィルターのサービス ルーチンが含まれています。 (前の段落には、フィルターに暗証番号 (pin) に関連付けられているストリームのサービスのシンクがについて説明します)。このサービス ルーチン呼び出し、ミニポート ドライバーの[ **IMiniportWavePci::Service** ](https://msdn.microsoft.com/library/windows/hardware/ff536736)メソッド。 サービス ルーチンで実行されるたびに DPC または ISR 呼び出し[**通知**](https://msdn.microsoft.com/library/windows/hardware/ff536918)フィルターのサービス グループにします。 **Init**メソッドがないケース ポート ドライバーが決してそのフィルター サービス ルーチンを呼び出すが、サービスのグループを指定できます。

### <a name="span-idhardwareinterruptsspanspan-idhardwareinterruptsspanspan-idhardwareinterruptsspanhardware-interrupts"></a><span id="Hardware_Interrupts"></span><span id="hardware_interrupts"></span><span id="HARDWARE_INTERRUPTS"></span>ハードウェアの割り込み

一部のミニポート ドライバーでは、多すぎるか不十分ハードウェアの割り込みを生成します。 DirectSound ハードウェア アクセラレーションを使った WavePci レンダリング デバイスによっては、ハードウェア割り込みは、マッピングの指定が不足して、レンダリング エンジンに枯渇のリスクが場合にのみ発生します。 その他のハードウェア アクセラレータによる WavePci デバイス ハードウェアの割り込みをすべて 1 つのマッピングの完了または他の比較的小さな間隔でに発生します。 この場合は、ISR を行うにはほとんどありませんが、各割り込みもレジスタのスワップとキャッシュの再読み込みを使用してシステム リソースを消費を頻繁に検索します。 ドライバーのパフォーマンスを向上させるのには、最初の手順では、枯渇のリスクなし割り込み可能な限りの数を減らします。 不要な割り込みを削除した後より効率的に実行する ISR を設計することでパフォーマンスを向上を実現できます。

一部のドライバーでは、Isr がストリームを呼び出すことによって時間を無駄[**通知**](https://msdn.microsoft.com/library/windows/hardware/ff536918)メソッド ストリームが実際に実行されているかどうかに関係なく、ハードウェアの割り込みが発生するたびにします。 ストリームが実行状態がない場合、DMA がアクティブでとしようとしてマッピングを取得、マッピングのリリースに費やされる時間または新しいイベントのストリームでのチェックは無駄になります。 ストリームが、ストリームを呼び出す前に実行されていることを ISR 効率的なドライバーでは、検証**通知**メソッド。

ただし、この種類の ISR ドライバーは、ストリームの実行状態の終了時に、保留中のイベント ストリームでトリガーされるかどうかを確認する必要があります。 それ以外の場合、イベントを遅延または紛失する可能性があります。 この問題は、Microsoft Windows XP よりも古いオペレーティング システムで一時停止への実行に遷移中にのみ発生します。 Windows XP 以降では、ポート ドライバーに自動的に、位置の未処理のイベント ストリーム状態を変更するとすぐにから信号実行を一時停止します。 古いオペレーティング システムでは、一方、ミニポート ドライバーは最終的な呼び出すことによって、未処理のイベントをトリガーする責任を負います[**通知**](https://msdn.microsoft.com/library/windows/hardware/ff536918)ストリームが一時停止した後すぐにします。 詳細については、一時停止/取得の最適化は以下を参照してください。

一般的な WavePci ミニポート ドライバー管理からの 1 つの再生ストリーム、 [KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)します。 KMixer の現在の実装では、再生のストリームをバッファーに 3 つのマッピング Irp の最小値を使用します。 各 IRP には、オーディオの約 10 ミリ秒の場合は、十分なバッファー ストレージが含まれています。 ミニポート ドライバーは IRP の最終的なマッピングでは、DMA コント ローラーが終了するたびに、ハードウェア割り込みをトリガー、割り込みする必要があります、DMA キューが不足するを防止するのに十分な頻度は比較的一定の 10 ミリ秒間隔で発生します。 

### <a name="span-idtimerdpcsspanspan-idtimerdpcsspanspan-idtimerdpcsspantimer-dpcs"></a><span id="Timer_DPCs"></span><span id="timer_dpcs"></span><span id="TIMER_DPCS"></span>タイマー Dpc

ドライバーは、任意のハードウェア アクセラレータによる DirectSound ストリームを管理している場合は、DPC、タイマーを使用してください (を参照してください[タイマー オブジェクトと Dpc](https://msdn.microsoft.com/library/windows/hardware/ff564655)) DMA 駆動のハードウェアの割り込みの代わりにします。 同等に、オンボードのタイマー付き PCI カード上の WavePci デバイスでは、DPC 代わりタイマーに基づくハードウェア割り込みを使用できます。

DirectSound バッファーの場合、1 つの IRP にバッファー全体をアタッチできます。 場合は、バッファーの大きさが、バッファーの末尾に達した場合にのみ、ミニポート ドライバーがハードウェア割り込みをスケジュール、連続する割り込み発生する可能性がこれまでに離れている DMA キューが特定されます。 また、ドライバーが、ハードウェア アクセラレータによる DirectSound ストリームの数が多いを管理する、各ストリームに独自の割り込みが生成される場合は、すべての割り込みの累積的な影響システムのパフォーマンスが低下します。 このような場合は、ハードウェアの割り込みを使用して、個々 のストリームの処理をスケジュールするミニポート ドライバーを避ける必要があります。 代わりに、すべてのストリームでタイマーによって生成された一定の間隔で実行するようにスケジュールを 1 つの DPC にサービスを提供する必要があります。

タイマーの間隔を 10 ミリ秒に設定して DPC 実連続的な間隔は、単一 KMixer 再生ストリームの場合は、ハードウェア割り込みの前に説明したのと同様です。 したがって、DPC は DirectSound ストリームのハードウェア アクセラレータを使用しただけでなく KMixer 再生ストリームを処理できます。

最後のストリームを終了すると、実行の状態、ミニポート ドライバーは、DPC システム CPU サイクルを節約するのには、タイマーを無効にする必要があります。 DPC を無効にすると、直後に、ドライバーをストリームに実行されていたで保留中のクロックまたは位置イベントがフラッシュされることを確認してください。 Windows 98 では、ドライバーを呼び出す必要があります Me、Windows 2000/ [**通知**](https://msdn.microsoft.com/library/windows/hardware/ff536918)保留中の一時停止中はストリームのイベントをトリガーします。 Windows XP 以降では、オペレーティング システムに保留中のイベント ストリーム、ミニポート ドライバーによる介入を必要とせず、実行状態を終了したときに自動的にトリガーされます。

### <a name="span-idpauseacquireoptimizationsspanspan-idpauseacquireoptimizationsspanspan-idpauseacquireoptimizationsspanpauseacquire-optimizations"></a><span id="PAUSE_ACQUIRE_Optimizations"></span><span id="pause_acquire_optimizations"></span><span id="PAUSE_ACQUIRE_OPTIMIZATIONS"></span>一時停止/取得の最適化

Windows 98 と Windows 2000 まで、WavePci ポート ドライバーのストリームのサービス ルーチン/(、 [ **RequestService** ](https://msdn.microsoft.com/library/windows/hardware/ff537009)メソッド)、ミニポート ドライバーの呼び出しが常に生成されます[ **IMiniportWavePciStream::Service** ](https://msdn.microsoft.com/library/windows/hardware/ff536731)ストリームが実行状態がかどうかに関係なくメソッド。 これらのオペレーティング システムで、**サービス**メソッドが時間を費やす前にストリームが実行されているかどうかを確認する必要があります実際の作業を実行します。 (ただし、ミニポート ドライバーの DPC または ISR が呼び出しに最適化されて既に場合[**通知**](https://msdn.microsoft.com/library/windows/hardware/ff536918)を実行している、追加するには、このチェックはストリームに対してのみ、**サービス**メソッドあります冗長です。)

Windows XP 以降では、この最適化は必要ありませんので、 [**通知**](https://msdn.microsoft.com/library/windows/hardware/ff536918)メソッドの呼び出し、 [**サービス**](https://msdn.microsoft.com/library/windows/hardware/ff536731)メソッドでのみ実行しているストリーム。

### <a name="span-idusingtheiprefetchoffsetinterfacespanspan-idusingtheiprefetchoffsetinterfacespanspan-idusingtheiprefetchoffsetinterfacespanusing-the-iprefetchoffset-interface"></a><span id="Using_the_IPreFetchOffset_Interface"></span><span id="using_the_iprefetchoffset_interface"></span><span id="USING_THE_IPREFETCHOFFSET_INTERFACE"></span>IPreFetchOffset インターフェイスを使用します。

DirectSound ユーザーがプレイ カーソルと書き込みカーソルのデュアルの概念を理解します。 再生のカーソルでは、デバイス (現時点で、DAC のサンプルのドライバーの最適な見積もり) から出力されるデータのストリーム内の位置を示します。 書き込み位置は、追加のデータを記述するクライアントの [次へ] の安全な場所のストリームの位置です。 WavePci、既定の想定は書き込みカーソルが要求された最後のマッピングの末尾に配置されていることです。 ミニポート ドライバーでは、未処理のマッピングの数が多い、取得された場合、再生のカーソル書き込みカーソルとオフセットが非常に大きくなることができます: WHQL オーディオ位置の特定のテストが失敗するのに十分な大きさです。 Windows XP 以降では、 [IPreFetchOffset](https://msdn.microsoft.com/library/windows/hardware/ff536951)インターフェイスがこうした問題に対処します。

ミニポート ドライバーを使用して[IPreFetchOffset](https://msdn.microsoft.com/library/windows/hardware/ff536951)を主に、ハードウェアの FIFO のサイズによって決まりますが、バス マスター ハードウェアのプリフェッチの特性を指定します。 オーディオのサブシステムは、再生のカーソル書き込みカーソルと定数のオフセットを設定するのに、このデータを使用します。 マッピングが、ハードウェアに渡される後もデータをマッピングに書き込まれることができます限り再生カーソルの場所から十分なことのできるは、既定のオフセットよりも大幅に小さくする、この定数のオフセットを利用します。これには、データが書き込まれます。 (このステートメントは、ドライバーのコピーまたはそれ以外の場合のマッピングのデータの操作はできませんと仮定)。一般的なオフセット 64 サンプルは、エンジンの設計によって順序があります。 この小さなオフセット、WavePci ドライバーは、多数のマッピングをまだ要求中に、応答性と機能を完全に指定できます。

DirectSound は、10 ミリ秒でハードウェア アクセラレータを使用した暗証番号 (pin) の書き込みカーソルを現在埋めますに注意してください。

詳細については、[プリフェッチ オフセット](prefetch-offsets.md)を参照してください。

### <a name="span-idprocessingdatainmappingsspanspan-idprocessingdatainmappingsspanspan-idprocessingdatainmappingsspanprocessing-data-in-mappings"></a><span id="Processing_Data_in_Mappings"></span><span id="processing_data_in_mappings"></span><span id="PROCESSING_DATA_IN_MAPPINGS"></span>マッピングでのデータ処理

可能であれば、マッピングでデータをタッチ ハードウェア ドライバーを必要があります。 ソフトウェアのマッピングに含まれるデータの処理は、ソフトウェアのフィルター、ハードウェア ドライバーとは別に分けする必要があります。 ハードウェア ドライバーがこのような処理を実行し、削減、効率、待機時間の問題を作成します。

ハードウェア ドライバーは、透明の実際のハードウェア機能に限り必要があります。 ドライバーは、ソフトウェアで実際に実行されるデータ変換のハードウェアのサポートを提供する必要があります要求ことはありません。

### <a name="span-idsynchronizationprimitivesspanspan-idsynchronizationprimitivesspanspan-idsynchronizationprimitivesspansynchronization-primitives"></a><span id="Synchronization_Primitives"></span><span id="synchronization_primitives"></span><span id="SYNCHRONIZATION_PRIMITIVES"></span>同期プリミティブ

ドライバーがそのコードが可能な場合にブロックされるを防ぐために設計されている場合、今後は、デッドロックやパフォーマンスの問題がある可能性は低くします。 具体的には、ドライバーのスレッドの実行は、別のスレッドまたはリソースの待機中に停止のリスクを負うことがなく完了するまで実行するよう努める必要があります。 たとえば、ドライバーのスレッドが、Interlocked を使用できます*Xxx*関数 (たとえばを参照してください[ **InterlockedIncrement**](https://msdn.microsoft.com/library/windows/hardware/ff547910)) 共有にアクセスを調整するにはリソースがブロックされているおそれはありません。

これらは強力な手法が、実行パスからすべてのスピン ロック、ミュー テックス、およびその他のブロックの同期プリミティブを安全に削除することができません。 使用、Interlocked*Xxx*無期限の待機は、データの不足で発生する可能性がありますに関する知識を持つ慎重関数。

何よりも、カスタムの同期プリミティブを作成できません。 組み込み Windows プリミティブ (ミュー テックス、スピン ロック) が、将来、新しいスケジューラ機能をサポートするために必要に応じて変更する可能性がありますし、カスタムの構造を使用したドライバーしないことが事実上保証、将来の処理します。

### <a name="span-idipincountinterfacespanspan-idipincountinterfacespanspan-idipincountinterfacespanipincount-interface"></a><span id="IPinCount_Interface"></span><span id="ipincount_interface"></span><span id="IPINCOUNT_INTERFACE"></span>IPinCount インターフェイス

Windows XP 以降では、 [IPinCount](https://msdn.microsoft.com/library/windows/hardware/ff536832)インターフェイスは、pin を割り当てることによって利用できるハードウェア リソースをより正確にアカウントに、ミニポート ドライバーの方法を提供します。 呼び出して、ミニポート ドライバーの[ **IPinCount::PinCount** ](https://msdn.microsoft.com/library/windows/hardware/ff536834)メソッド、ポート、ドライバーは次の処理します。

-   公開フィルターの現在の pin によって (ようにポート ドライバーによって管理される) が、ミニポート ドライバーをカウントします。

-   ミニポート ドライバー、pin を変更する営業案件の数を動的にでは、ハードウェア リソースの現在の可用性を反映します。

オーディオ デバイスによっては、wave ストリームでは、さまざまな属性 (3-D、ステレオ/mono など) が消費されることにハードウェア リソースの数の観点からさまざまな「重み」をもがあります。 ときに、開く、またはいずれかによって、使用可能な pin の数で「軽量」ストリーム、ドライバーのインクリメントまたはデクリメントが閉じる。 「重い」ストリームを開くときに、ミニポート ドライバーを 1 つに 2 つの代わりより正確に残りのリソースを作成できるピンの数を指定するために pin の使用可能なカウントをデクリメントする必要があります。

重量級のストリームが閉じられたときに、プロセスが取り消されます。 使用可能な暗証番号 (pin) の数が増加する 1 つ以上という事実を反映するためにその 2 つまたは解放されたリソースより軽量のストリームを作成できます。

 

 




