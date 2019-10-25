---
title: WavePci ミニポート ドライバーにおけるパフォーマンスの問題
description: WavePci ミニポート ドライバーにおけるパフォーマンスの問題
ms.assetid: 785fd743-0c78-44cd-95bf-1f961aa414b5
keywords:
- WavePci パフォーマンスの問題の WDK オーディオ
- ストリームサービスメカニズムの WDK オーディオ
- ハードウェア割り込みの WDK オーディオ
- 割り込みサービスルーチン WDK オーディオ
- Isr WDK オーディオ
- タイマー Dpc WDK オーディオ
- 一時停止/取得の最適化 WDK オーディオ
- IPreFetchOffset
- 同期プリミティブ WDK オーディオ
- IPinCount
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0861936e5e1b079d8b665338ec9907d63a7982f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832511"
---
# <a name="performance-issues-for-a-wavepci-miniport-driver"></a>WavePci ミニポート ドライバーにおけるパフォーマンスの問題


## <span id="performance_issues_for_a_wavepci_miniport_driver"></span><span id="PERFORMANCE_ISSUES_FOR_A_WAVEPCI_MINIPORT_DRIVER"></span>


次の一般的な原則に従うことで、システムに対するオーディオドライバーのパフォーマンスへの影響を大幅に軽減できます。

-   通常の操作中に実行されるコードを最小化します。

-   必要な場合にのみコードを実行します。

-   CPU の負荷だけでなく、システムリソースの消費量の合計を考慮してください。

-   速度とサイズに合わせてコードを最適化します。

また、WavePci ミニポートドライバーでは、オーディオデバイス固有のパフォーマンスの問題に対処する必要があります。 次の説明では、主にオーディオレンダリングの問題について説明します。ただし、いくつかの推奨される手法はオーディオキャプチャにも当てはまります。

### <a name="span-idstream_servicing_mechanismsspanspan-idstream_servicing_mechanismsspanspan-idstream_servicing_mechanismsspanstream-servicing-mechanisms"></a><span id="Stream_Servicing_Mechanisms"></span><span id="stream_servicing_mechanisms"></span><span id="STREAM_SERVICING_MECHANISMS"></span>ストリームのサービスメカニズム

パフォーマンスの最適化について説明する前に、ストリームを処理するための WavePci メカニズムを理解するために、いくつかの背景が必要です。

Wave レンダーストリームまたはキャプチャストリームを処理する場合、オーディオデバイスはミニポートドライバーによって定期的にサービスを実行する必要があります。 ストリームに対して新しいマッピングを使用できる場合、ドライバーはこれらのマッピングをストリームの DMA キューに追加します。 また、このドライバーは、既に処理されているすべてのマッピングをキューから削除します。 マッピングの詳細については、「 [WavePci Latency](wavepci-latency.md)」を参照してください。

サービスを実行するために、ミニポートドライバーは、間隔がシステムタイマーによって設定されるか、DMA による割り込みによって設定されるかに応じて、*遅延プロシージャ呼び出し (DPC)* または割り込みサービスルーチン (ISR) を提供します。 後者の場合、DMA ハードウェアは通常、が一定量のストリームデータの転送を完了するたびに割り込みをトリガーします。

DPC または ISR が実行されるたびに、サービスを必要とするストリームが決定されます。 DPC または ISR は、 [**IPortWavePci:: Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)メソッドを呼び出すことによってストリームをサービスします。 このメソッドは、stream のサービスグループ ( [Iservicegroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)型のオブジェクト) の呼び出しパラメーターとしてを受け取ります。 **Notify**メソッドは、サービスグループの[**requestservice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice)メソッドを呼び出します (「 **iservices**」を参照してください)。

サービスグループオブジェクトには、 [Iservices ink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)型のオブジェクトであるサービスシンクのグループが含まれています。 [Iservicegroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)は Iservices ink から派生し、両方のインターフェイスに[**requestservice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice)メソッドがあります。 [**Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)メソッドがサービスグループの**requestservice**メソッドを呼び出すと、サービスグループは、グループ内の各サービスシンクで**requestservice**メソッドを呼び出すことによって応答します。

ストリームのサービスグループには、少なくとも1つのサービスシンクが含まれています。これは、ストリームの作成直後にポートドライバーがサービスグループに追加します。 ポートドライバーは、ミニポートドライバーの[**IMiniportWavePci:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)メソッドを呼び出して、サービスグループへのポインターを取得します。 サービスシンクの[**requestservice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice)メソッドは、ポートドライバーのストリーム固有のサービスルーチンです。 このルーチンは、次のことを行います。

-   ミニポートドライバーの[**IMiniportWavePciStream:: Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service)メソッドを呼び出します。

-   サービスルーチンが最後に実行されてからストリームで、新しく保留された位置またはクロックイベントをトリガーします。

「 [KS イベント](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)」で説明されているように、クライアントは、ストリームが特定の位置に到達したとき、またはクロックが特定のタイムスタンプに達したときに通知を受け取るように登録できます。 [**Newstream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)メソッドには、サービスグループを提供しないオプションがあります。この場合、ポートドライバーは独自のタイマーを設定して、サービスルーチンへの呼び出しの間隔をマークします。

[**Newstream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)メソッドと同様に、ミニポートドライバーの[**IMiniportWavePci:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)メソッドは、サービスグループへのポインターも出力します。 **Init**呼び出しの後、ポートドライバーはサービスシンクをサービスグループに追加します。 この特定のサービスシンクには、フィルター全体のサービスルーチンが含まれています。 (前の段落では、フィルターのピンに関連付けられているストリームのサービスシンクについて説明しています)。このサービスルーチンは、ミニポートドライバーの[**IMiniportWavePci:: service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-service)メソッドを呼び出します。 サービスルーチンは、DPC または ISR 呼び出しによって、フィルターのサービスグループが[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)されるたびに実行されます。 **Init**メソッドには、サービスグループを指定しないオプションがあります。この場合、ポートドライバーはフィルターサービスルーチンを呼び出しません。

### <a name="span-idhardware_interruptsspanspan-idhardware_interruptsspanspan-idhardware_interruptsspanhardware-interrupts"></a><span id="Hardware_Interrupts"></span><span id="hardware_interrupts"></span><span id="HARDWARE_INTERRUPTS"></span>ハードウェア割り込み

一部のミニポートドライバーによって生成されるハードウェア割り込みが多すぎるか、十分ではありません。 DirectSound ハードウェアアクセラレーションを使用する一部の WavePci レンダリングデバイスでは、マッピングの提供がほぼ使い果たされ、レンダリングエンジンが枯渇する危険性がある場合にのみ、ハードウェアの割り込みが発生します。 その他のハードウェアアクセラレータ WavePci デバイスでは、1つのマッピングが完了するたびに、またはその他の比較的小さな間隔でハードウェアの割り込みが発生します。 この場合、ISR によって実行されることはほとんどありませんが、各割り込みは、レジスタスワップとキャッシュ再読み込みによってシステムリソースを消費します。 ドライバーのパフォーマンスを向上させるための最初の手順は、割り込みの数を可能な限り減らすことです。 不要な割り込みをなくした後、より効率的に実行されるように ISR を設計することで、パフォーマンスをさらに向上させることができます。

一部のドライバーでは、Isr は、ストリームが実際に実行されているかどうかに関係なく、ハードウェアの割り込みが発生するたびにストリームの[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)メソッドを呼び出すことによって時間を無駄にします。 実行状態のストリームがない場合、DMA は非アクティブになります。また、ストリーム内の新しいイベントを取得しようとするために費やされた時間は無駄になります。 効率的なドライバーでは、ISR はストリームが実行中であることを確認してからストリームの**通知**メソッドを呼び出します。

ただし、この種類の ISR を持つドライバーは、ストリームが実行状態を終了したときに、ストリームの保留中のイベントがトリガーされるようにする必要があります。 そうしないと、イベントが遅延したり失われたりする可能性があります。 この問題が発生するのは、Microsoft Windows XP より前のオペレーティングシステムの実行から一時停止への移行中のみです。 Windows XP 以降では、ストリームの状態が [実行中] から [一時停止] に変更された場合、ポートドライバーによって未処理の位置イベントがすぐに自動的に通知されます。 ただし、以前のオペレーティングシステムでは、ミニポートドライバーは、ストリームが一時停止した直後に[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)するための最後の呼び出しを行うことによって、未処理のイベントをトリガーします。 詳細については、以下の「一時停止/取得の最適化」を参照してください。

一般的な WavePci ミニポートドライバーは、 [KMixer システムドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)からの単一の再生ストリームを管理します。 KMixer の現在の実装では、3つ以上のマッピング Irp を使用して、再生ストリームをバッファーします。 各 IRP には、約10ミリ秒のオーディオを格納するための十分なバッファーストレージが含まれています。 IRP 内の最終的なマッピングで DMA コントローラーが終了するたびに、ミニポートドライバーによってハードウェア割り込みが発生した場合、通常の10ミリ秒間隔で割り込みが発生します。これは、DMA キューがいっぱいになるのを防ぐのに十分な頻度です。 

### <a name="span-idtimer_dpcsspanspan-idtimer_dpcsspanspan-idtimer_dpcsspantimer-dpcs"></a><span id="Timer_DPCs"></span><span id="timer_dpcs"></span><span id="TIMER_DPCS"></span>タイマー Dpc

ドライバーがハードウェアアクセラレータによる DirectSound ストリームを管理する場合、DMA 駆動型ハードウェア割り込みではなく、タイマー DPC ([タイマーオブジェクトと dpc](https://docs.microsoft.com/windows-hardware/drivers/kernel/timer-objects-and-dpcs)を参照) を使用する必要があります。 同様に、オンボードタイマーを使用する PCI カード上の WavePci デバイスは、DPC ではなくタイマー駆動型のハードウェア割り込みを使用できます。

DirectSound バッファーの場合、バッファー全体を1つの IRP にアタッチできます。 バッファーが大きい場合、ミニポートドライバーは、バッファーの最後に到達したときにのみハードウェア割り込みをスケジュールします。これまでに、DMA キューがいっぱいになるまで、連続した割り込みが発生する可能性があります。 また、ドライバーが多数のハードウェアアクセラレータの DirectSound ストリームを管理しており、各ストリームが独自の割り込みを生成した場合、すべての割り込みの累積的な影響によってシステムパフォーマンスが低下する可能性があります。 このような状況では、ミニポートドライバーは、個々のストリームのサービスをスケジュールするためにハードウェア割り込みを使用しないようにする必要があります。 代わりに、通常のタイマーによって生成される間隔で実行されるようにスケジュールされた1つの DPC 内のすべてのストリームを処理する必要があります。

タイマー間隔を10ミリ秒に設定することにより、連続する DPC 実行の間隔は、前に説明したように、1つの KMixer 再生ストリームの場合のハードウェア割り込みに似ています。 そのため、DPC は、ハードウェアアクセラレータによる DirectSound ストリームに加えて、KMixer 再生ストリームを処理できます。

最後のストリームが実行状態を終了すると、ミニポートドライバーは、システムの CPU サイクルを浪費しないように、タイマー DPC を無効にする必要があります。 DPC を無効にした直後に、ドライバーは、以前に実行されたストリームで保留中のクロックイベントまたは位置イベントがフラッシュされるようにする必要があります。 Windows 98/Me および Windows 2000 では、ドライバーは、一時停止中のストリームで保留中のイベントをトリガーするために[**Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)を呼び出す必要があります。 Windows XP 以降では、ストリームが実行状態を終了すると、オペレーティングシステムによって保留中のイベントが自動的にトリガーされます。ミニポートドライバーによる操作は必要ありません。

### <a name="span-idpause_acquire_optimizationsspanspan-idpause_acquire_optimizationsspanspan-idpause_acquire_optimizationsspanpauseacquire-optimizations"></a><span id="PAUSE_ACQUIRE_Optimizations"></span><span id="pause_acquire_optimizations"></span><span id="PAUSE_ACQUIRE_OPTIMIZATIONS"></span>一時停止/取得の最適化

Windows 98/Me と Windows 2000 では、WavePci port ドライバーのストリームサービスルーチン ( [**Requestservice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice)メソッド) は、ストリームがにあるかどうかに関係なく、常にミニポートドライバーの[**IMiniportWavePciStream:: service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service)メソッドの呼び出しを生成します。実行状態。 これらのオペレーティングシステムでは、実際の作業に時間を費やす前に、**サービス**メソッドでストリームが実行されているかどうかを確認する必要があります。 (ただし、ミニポートドライバーの DPC または ISR が、を実行しているストリームに対してのみ[**通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)を呼び出すように既に最適化されている場合は、このチェックを**サービス**メソッドに追加することが冗長になる可能性があります)。

Windows XP 以降では、 [**Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)メソッドは実行中のストリームに対してのみ[**サービス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service)メソッドを呼び出すため、この最適化は不要です。

### <a name="span-idusing_the_iprefetchoffset_interfacespanspan-idusing_the_iprefetchoffset_interfacespanspan-idusing_the_iprefetchoffset_interfacespanusing-the-iprefetchoffset-interface"></a><span id="Using_the_IPreFetchOffset_Interface"></span><span id="using_the_iprefetchoffset_interface"></span><span id="USING_THE_IPREFETCHOFFSET_INTERFACE"></span>IPreFetchOffset インターフェイスの使用

DirectSound ユーザーは、play カーソルと書き込みカーソルの2つの概念に精通しています。 Play カーソルは、デバイスから出力されているデータのストリーム内の位置を示します (現在 DAC にあるサンプルのドライバーの最適な推定値)。 書き込み位置は、クライアントが追加データを書き込むための次の安全な場所のストリーム内の位置です。 WavePci の場合、既定では、書き込みカーソルは最後に要求されたマッピングの最後に配置されます。 ミニポートドライバーが大量の未処理のマッピングを取得した場合、play カーソルと書き込みカーソルの間のオフセットが非常に大きくなる可能性があります。これは、特定の WHQL オーディオ位置テストを失敗させるのに十分な大きさです。 Windows XP 以降では、 [Iprefetchoffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iprefetchoffset)インターフェイスによってこれらの問題が解決されます。

ミニポートドライバーは、 [Iprefetchoffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iprefetchoffset)を使用して、バスマスタハードウェアのプリフェッチ特性を指定します。これは主にハードウェア FIFO サイズによって決まります。 オーディオサブシステムでは、このデータを使用して、再生カーソルと書き込みカーソルの間に一定のオフセットを設定します。 この定数オフセットは、既定のオフセットよりも大幅に小さくなる可能性があります。そのため、play カーソルが場所から離れた場所にある限り、マッピングがハードウェアに渡された後でもデータをマッピングに書き込むことができるという事実を活用します。データが書き込まれます。 (このステートメントは、ドライバーがマッピング内のデータをコピーしたり、それ以外の方法で操作したりしないことを前提としています)。一般的なオフセットは、エンジンの設計によっては、64サンプルの順序である場合があります。 この小さなオフセットを使用すると、WavePci ドライバーは完全に応答し、大量のマッピングを要求しながら機能します。

DirectSound では、現在、ハードウェアアクセラレータのピンの書き込みカーソルが10ミリ秒で埋め込まれていることに注意してください。

詳細については、「[プリフェッチオフセット](prefetch-offsets.md)」を参照してください。

### <a name="span-idprocessing_data_in_mappingsspanspan-idprocessing_data_in_mappingsspanspan-idprocessing_data_in_mappingsspanprocessing-data-in-mappings"></a><span id="Processing_Data_in_Mappings"></span><span id="processing_data_in_mappings"></span><span id="PROCESSING_DATA_IN_MAPPINGS"></span>マッピング内のデータの処理

可能な場合は、ハードウェアドライバーがマッピング内のデータをタッチしないようにします。 マッピングに含まれるデータのすべてのソフトウェア処理は、ハードウェアドライバーとは別のソフトウェアフィルターに分割する必要があります。 ハードウェアドライバーがこのような処理を実行すると、効率性が低下し、待機時間の問題が発生します。

ハードウェアドライバーは、実際のハードウェア機能について透過的に行う必要があります。 ドライバーは、実際にはソフトウェアで実行されるデータ変換のハードウェアサポートを提供するように要求することはできません。

### <a name="span-idsynchronization_primitivesspanspan-idsynchronization_primitivesspanspan-idsynchronization_primitivesspansynchronization-primitives"></a><span id="Synchronization_Primitives"></span><span id="synchronization_primitives"></span><span id="SYNCHRONIZATION_PRIMITIVES"></span>同期プリミティブ

ドライバーが、可能な限りブロックされないように設計されている場合、デッドロックやパフォーマンスの問題が発生する可能性は低くなります。 具体的には、ドライバーの実行スレッドは、別のスレッドまたはリソースを待機している間に停止するリスクを生じることなく、完了まで実行するように努める必要があります。 たとえば、ドライバースレッドでは、インタロックされた*Xxx*関数 (たとえば、 [**InterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)を参照) を使用して、特定の共有リソースへのアクセスを調整できます。ブロックされるリスクはありません。

これらは強力な手法ですが、実行パスからすべてのスピンロック、ミューテックス、およびその他のブロックしている同期プリミティブを安全に削除できない可能性があります。 無限の待機によってデータが枯渇する可能性があるという知識があれば、インタロックされた*Xxx*関数を慎重に使用してください。

それ以外の場合は、カスタム同期プリミティブを作成しないでください。 組み込みの Windows プリミティブ (mutex、スピンロックなど) は、将来的に新しいスケジューラ機能をサポートするために必要に応じて変更される可能性があります。また、カスタム構成体を使用するドライバーは、今後は動作しないことが事実上保証されます。

### <a name="span-idipincount_interfacespanspan-idipincount_interfacespanspan-idipincount_interfacespanipincount-interface"></a><span id="IPinCount_Interface"></span><span id="ipincount_interface"></span><span id="IPINCOUNT_INTERFACE"></span>IPinCount インターフェイス

Windows XP 以降では、 [Ipincount](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-ipincount)インターフェイスにより、ミニポートドライバーは、pin の割り当てによって使用されるハードウェアリソースをより正確に考慮することができます。 ミニポートドライバーの[**Ipincount::P incount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-ipincount-pincount)メソッドを呼び出すことにより、ポートドライバーは次のことを実行します。

-   ポートドライバーによって保持されているフィルターの現在の pin 数をミニポートドライバーに公開します。

-   は、ハードウェアリソースの現在の可用性を動的に反映するように、pin の数を変更する機会をミニポートドライバーに与えます。

一部のオーディオデバイスでは、さまざまな属性 (3-d、ステレオ、mono など) を持つ wave ストリームの "重み" は、使用するハードウェアリソースの数によって異なる場合があります。 "ライトウェイト" ストリームを開いたり閉じたりすると、ドライバーは使用可能な pin の数を1つずつ増減させることができます。 ただし、"重い" ストリームを開くときに、ミニポートドライバーでは、残りのリソースで作成できる pin の数を正確に示すために、使用可能な pin の数を1つずつではなく2つ減らす必要がある場合があります。

このプロセスは、重いストリームが閉じられると元に戻されます。 新たに解放されたリソースから2つ以上の軽量ストリームを作成できるという事実を反映するために、使用可能な pin の数が1つ以上増加することがあります。

 

 




