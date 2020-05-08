---
title: ウェーブ フィルター
description: ウェーブ フィルター
ms.assetid: 9e364c8f-55c3-4ec9-a9ce-9ee0f6a0746b
keywords:
- オーディオフィルター WDK audio、wave
- wave フィルター WDK オーディオ
- WDK オーディオ、wave をフィルター処理します
- wave レンダリングフィルター WDK オーディオ
- wave キャプチャフィルター WDK オーディオ
- wave audio WDK オーディオのレンダリング
- wave audio WDK オーディオをキャプチャする
- WaveRT フィルター WDK オーディオ
- WavePci フィルター WDK オーディオ
- WaveCyclic フィルター WDK オーディオ
- WaveRT、フィルター
- WavePci、フィルター
- オーディオデバイス、WaveCyclic
- WaveCyclic、フィルター
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: f8264ef7e4d007d006d05c5924890e4d74876ad8
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925629"
---
# <a name="wave-filters"></a>ウェーブ フィルター


## <span id="wave_filters"></span><span id="WAVE_FILTERS"></span>


Wave フィルターは、wave 形式のデジタルオーディオデータを表示またはキャプチャするデバイスを表します。 通常、アプリケーションは DirectSound API または Microsoft Windows マルチメディア waveOut*xxx*および waveIn*xxx*関数を使用して、これらのデバイスの機能にアクセスします。 WDM オーディオドライバーがサポートできる wave 形式の詳細については、「 [**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex) and [**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)」を参照してください。

*Wave レンダリング*フィルターは、入力として wave デジタルオーディオストリームを受信し、アナログオーディオ信号 (スピーカーまたは外部ミキサーのセット) またはデジタルオーディオストリーム (S/PDIF コネクタなど) のいずれかを出力します。

*Wave キャプチャ*フィルターは、アナログオーディオ信号 (マイクまたは入力ジャックからの) またはデジタルストリーム (たとえば、S/PDIF コネクタからの) を入力として受け取ります。 同じフィルターは、デジタルオーディオデータを含む wave ストリームを出力します。

1つの wave フィルターは、レンダリングとキャプチャの両方を同時に実行できます。 たとえば、この種類のフィルターは、スピーカーのセットを介してオーディオを再生し、同時にマイクを介してオーディオを録音できるオーディオデバイスを表します。 または、「[動的オーディオサブデバイス](dynamic-audio-subdevices.md)」で説明されているように、wave レンダリングハードウェアと wave キャプチャハードウェアが個別の wave フィルターとして表される場合があります。

オーディオアダプタードライバーは、ハードウェアベンダーがアダプタードライバーの一部として実装する wave ミニポートドライバーを、システムによって実装される wave ポートドライバーでバインドすることによって、wave フィルターを形成します。 ミニポートドライバーは、wave フィルターに対するハードウェア固有のすべての操作を処理し、ポートドライバーはすべての汎用 wave フィルター関数を管理します。

PortCls システムドライバー (Portcls) は、WaveRT、WavePci、WaveCyclic の3つの wave ポートドライバーを実装しています。

次の3種類の wave フィルターが動作します。

-   *Wavert*フィルターは、wave データ用のバッファーを割り当て、そのバッファーにユーザーモードクライアントから直接アクセスできるようにします。 バッファーは、wave デバイスのハードウェア機能に応じて、連続した、または連続しないメモリブロックで構成できます。 クライアントは、仮想メモリの連続するブロックとしてバッファーにアクセスします。 バッファーは循環しています。つまり、デバイスの読み取り (レンダリング用) または書き込み (キャプチャ用) ポインターがバッファーの末尾に達すると、バッファーの先頭に自動的にラップされます。

-   *WavePci*フィルターは、クライアントのバッファーに直接アクセスします。 クライアントは、1つの連続した仮想メモリブロックとしてバッファーにアクセスしますが、WavePci フィルターは、連続していない可能性のあるメモリブロックとしてバッファーにアクセスする必要があります。 レンダリングストリームまたはキャプチャストリームの連続部分を含むブロックは、デバイスでキューに登録されます。 デバイスの読み取りまたは書き込みポインターが1つのブロックの最後に達すると、キュー内の次のブロックの先頭に移動します。

-   *WaveCyclic*フィルターは、1つの連続したメモリブロックで構成されるバッファーを割り当てて、その出力 (レンダリング用) または入力 (キャプチャ用) バッファーとして使用します。 このバッファーは循環しています。 バッファーにはクライアントから直接アクセスできないため、ドライバーは、ドライバーの循環バッファーとクライアントのユーザーモードバッファーとの間でデータをコピーする必要があります。

WaveRT は、WaveCyclic とよりも優先されます。 WavePci と WaveCyclic は、以前のバージョンの Windows で使用されていました。

WaveRT フィルターは、PCI や PCI Express などのシステムバス上に存在するオーディオデバイスを表すことができます。 WaveCyclic フィルターまたは WavePci フィルターに対する WaveRT フィルターの主な利点は、WaveRT フィルターを使用すると、ユーザーモードのクライアントがオーディオハードウェアとオーディオデータを直接交換できることです。 一方、WaveCyclic フィルターと WavePci フィルターでは、ドライバーによる定期的なソフトウェアの介入が必要です。これにより、オーディオストリームの待機時間が長くなります。 さらに、スキャッター/ギャザー DMA 機能の有無にかかわらず、オーディオデバイスは WaveRT フィルターとして表すことができます。 詳細については、「[リアルタイムオーディオストリーミング用の Wave ポートドライバー](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WaveRTport.doc) 」ホワイトペーパーを参照してください。


### <a name="span-idwavert_filterspanspan-idwavert_filterspanwavert-filters"></a><span id="wavert_filter"></span><span id="WAVERT_FILTER"></span>WaveRT フィルター

WaveRT フィルターは、ポート/ミニポートドライバーのペアとして実装されます。 Windows Vista 以降では、WaveRT フィルターファクトリによって WaveRT フィルターが次のように作成されます。

-   WaveRT ミニポートドライバーオブジェクトをインスタンス化します。

-   このメソッドは、GUID 値**CLSID\_PortWaveRT**を持つ[**pcnewport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)を呼び出すことによって、wastport ドライバーオブジェクトをインスタンス化します。

-   ポートドライバーの[**IPort:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)メソッドを呼び出して、ミニポートドライバーをポートドライバーにバインドします。

[サブデバイス作成](subdevice-creation.md)のコード例では、このプロセスを示しています。 ポートとミニポートドライバーは、 [IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)インターフェイスと[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)インターフェイスを使用して相互に通信します。

詳細については、「[リアルタイムオーディオストリーミング用の Wave ポートドライバー](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WaveRTport.doc) 」ホワイトペーパーを参照してください。

### <a name="span-idinformation_for_previous_versions_of_windowsspanspan-idinformation_for_previous_versions_of_windowsspanspan-idinformation_for_previous_versions_of_windowsspaninformation-for-previous-versions-of-windows"></a><span id="Information_for_previous_versions_of_Windows"></span><span id="information_for_previous_versions_of_windows"></span><span id="INFORMATION_FOR_PREVIOUS_VERSIONS_OF_WINDOWS"></span>以前のバージョンの Windows に関する情報

**Windows の以前のバージョンの WaveCyclic 情報**

WaveCyclic フィルターは、ISA、PCI、PCI Express、PCMCIA などのシステムバスに接続するオーディオデバイスを表すことができます。 "WavePci" という名前が示すように、WavePci フィルターは通常、PCI バスに接続するデバイスを表します。ただし、原則として、WavePci デバイスは代わりに ISA バスに接続することがあります (たとえば、)。 WaveCyclic でサポートされているより単純なデバイスとは異なり、WavePci でサポートされているデバイスには、スキャッター/ギャザー DMA 機能が必要です。 PCI バスに存在するが、スキャッター/ギャザー DMA がないオーディオデバイスは、WaveCyclic フィルターとして表すことができますが、WavePci フィルターとして表示することはできません。

**Windows の以前のバージョンの WavePci 情報**

WavePci デバイスは、任意のメモリアドレスに配置でき、任意のバイト配置で開始および終了するバッファーとの間で、スキャッター/ギャザー DMA 転送を実行できます。 これに対し、WaveCyclic デバイスの DMA ハードウェアでは、デバイスのミニポートドライバーによって割り当てられる1つのバッファーとの間でデータを移動する機能のみが必要です。 WaveCyclic ミニポートドライバーは、DMA チャネルの制限された機能を満たす循環バッファーを自由に割り当てることができます。 たとえば、一般的な WaveCyclic デバイスの DMA チャネルでは、次の制限を満たすバッファーが必要になる場合があります。

-   バッファーは、物理アドレス空間の特定の領域にあります。

-   バッファーは、物理および仮想アドレス空間で連続しています。

-   バッファーは、4バイトまたは8バイトの境界で開始および終了します。

ただし、このように簡単にするために、WaveCyclic デバイスは、周期的なバッファーとの間でデータをコピーするソフトウェアに依存する必要があります。一方、WavePci デバイスは、そのようなコピーを避けるために、DMA ハードウェアのスキャッター/ギャザー機能に依存しています。 Wave オーディオデータをレンダリングデバイスに配信するか、キャプチャデバイスからデータを取得する Irp は、データバッファーを伴います。これらの各バッファーには、レンダリングまたはキャプチャされるオーディオストリームの一部が含まれます。 WavePci デバイスは、スキャッター/ギャザー DMA エンジンを使用してこれらのバッファーに直接アクセスできます。一方、WaveCyclic デバイスでは、データを IRP からの循環バッファーにコピーする必要があります。また、その逆も可能です。

### <a name="span-idwavepci_filterspanspan-idwavepci_filterspanwavepci-filters"></a><span id="wavepci_filter"></span><span id="WAVEPCI_FILTER"></span>WavePci フィルター

**注: 以前のバージョンの Windows の WavePci 情報**

WavePci フィルターは、ポート/ミニポートドライバーのペアとして実装されます。 WavePci フィルターファクトリは、次のように WavePci フィルターを作成します。

-   WavePci ミニポートドライバーオブジェクトをインスタンス化します。

-   このメソッドは、GUID 値**CLSID\_PortWavePci**を指定して[**pcnewport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)を呼び出すことによって、WavePci port driver オブジェクトをインスタンス化します。

-   ポートドライバーの[**IPort:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)メソッドを呼び出して、ミニポートドライバーをポートドライバーにバインドします。

[サブデバイス作成](subdevice-creation.md)のコード例では、このプロセスを示しています。 ポートとミニポートドライバーは、 [IPortWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepci)インターフェイスと[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)インターフェイスを使用して相互に通信します。

詳細については、「 [WavePci Devices の実装に関する問題](implementation-issues-for-wavepci-devices.md)」を参照してください。

### <a name="span-idwavecyclic_filterspanspan-idwavecyclic_filterspanwavecyclic-filters"></a><span id="wavecyclic_filter"></span><span id="WAVECYCLIC_FILTER"></span>WaveCyclic フィルター

**注: 以前のバージョンの Windows の WaveCyclic 情報**

WaveCyclic フィルターは、ポート/ミニポートドライバーのペアとして実装されます。 WaveCyclic フィルターファクトリは、次のように WaveCyclic フィルターを作成します。

-   WaveCyclic ミニポートドライバーオブジェクトをインスタンス化します。

-   このメソッドは、GUID 値**CLSID\_PortWaveCyclic**を指定して[**pcnewport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)を呼び出すことによって、WaveCyclic port driver オブジェクトをインスタンス化します。

-   ポートドライバーの[**IPort:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)メソッドを呼び出して、ミニポートドライバーをポートドライバーにバインドします。

[サブデバイス作成](subdevice-creation.md)のコード例では、このプロセスを示しています。 ポートとミニポートドライバーは、 [IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)インターフェイスと[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)インターフェイスを使用して相互に通信します。

WaveCyclic フィルターの循環バッファーは、常に、連続した仮想メモリのブロックで構成されます。 [**IDmaChannel:: AllocateBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-allocatebuffer)メソッドのポートドライバーの実装では、物理と仮想の両方のメモリアドレス空間で連続したバッファーが常に割り当てられます。 前述のように、WaveCyclic デバイスの DMA エンジンによってバッファーメモリに追加の制約が課される場合、ミニポートドライバーは、これらの制約を満たす独自のバッファー割り当て方法を自由に実装できます。

大きなバッファー (たとえば、物理的に連続する8つのメモリページ) を要求する WaveCyclic ミニポートドライバーは、オペレーティングシステムによって元の要求が拒否された場合に、バッファーサイズを小さくするための準備を行う必要があります。 オーディオデバイスは、システムリソースを再調整するためにアンロードおよび再読み込みされることがあります (「リソースを再調整[するためのデバイスの停止](https://docs.microsoft.com/windows-hardware/drivers/kernel/stopping-a-device-to-rebalance-resources)」を参照してください)。

バスマスタリング DMA ハードウェアが組み込まれた WaveCyclic デバイスは、*マスターデバイス*と呼ばれます。 また、WaveCyclic デバイスは、DMA が組み込まれていない*下位デバイス*でもかまいません。 下位デバイスは、システム DMA コントローラーに依存して、必要なデータ転送を実行する必要があります。 マスターデバイスと下位デバイスの詳細については、「 [IDmaChannel](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannel) and [IDmaChannelSlave](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannelslave)」を参照してください。

WaveCyclic ミニポートドライバーは、既定の DMA チャネルオブジェクトを使用する代わりに、独自の DMA チャネルオブジェクトを実装できます。このオブジェクトは、ポートドライバーの新しい*Xxx*DmaChannel メソッドのいずれかによって作成されます。

[**IPortWaveCyclic::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newmasterdmachannel)

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newslavedmachannel)

アダプタードライバーのカスタム[IDmaChannel](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannel)実装では、特殊なハードウェア制約を満たすためにデータのカスタム処理を実行できます。 たとえば、Windows マルチメディア関数では、16ビットのサンプルが常に符号付きの値である wave 形式が使用されますが、オーディオレンダリングハードウェアは、16ビットの符号なしの値を代わりに使用するように設計されている場合があります。 この場合、ドライバーのカスタム[**IDmaChannel:: CopyTo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyto)メソッドを記述して、署名されたソース値を、ハードウェアが必要とする符号なしのターゲット値に変換することができます。 この手法は、ハードウェア設計の欠陥を回避するのに役立ちますが、ソフトウェアのオーバーヘッドに大きなコストがかかることもあります。

独自の DMA チャネルオブジェクトを実装するドライバーの例については、「Sb16 sample audio adapter in the WDK」を参照してください。 定数\_オーバーライド DMA\_チャネルが**TRUE**に定義されている場合、ソースコード内の条件付きコンパイルステートメントによって、独自の[IDmaChannel](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannel)オブジェクトを実装できるようになります。このオブジェクトは、ドライバーが IPortWaveCyclic:: New*Xxx*DmaChannel 呼び出しの既定の IDmaChannel オブジェクトの代わりに使用します。

 

 




