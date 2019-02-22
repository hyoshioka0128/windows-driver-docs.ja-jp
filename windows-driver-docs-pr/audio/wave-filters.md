---
title: Wave フィルター
description: Wave フィルター
ms.assetid: 9e364c8f-55c3-4ec9-a9ce-9ee0f6a0746b
keywords:
- オーディオ フィルター WDK のオーディオ、wave
- wave フィルター WDK オーディオ
- フィルターの WDK オーディオ、wave
- wave 表示フィルターの WDK オーディオ
- wave キャプチャ フィルターの WDK オーディオ
- WDK オーディオのオーディオ レンダリング wave
- wave オーディオを WDK のキャプチャ
- WaveRT フィルター WDK オーディオ
- WavePci フィルター WDK オーディオ
- WaveCyclic フィルター WDK オーディオ
- WaveRT、フィルター処理
- WavePci、フィルター処理
- オーディオ デバイス、WaveCyclic
- WaveCyclic、フィルター処理
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6c32ab24051c34ffe8cf8f265baaabdc5fa44880
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552845"
---
# <a name="wave-filters"></a>Wave フィルター


## <span id="wave_filters"></span><span id="WAVE_FILTERS"></span>


Wave フィルターは、表示や、wave 形式のデジタル オーディオ データをキャプチャするデバイスを表します。 アプリケーションが通常、DirectSound API または Microsoft Windows のマルチ メディア waveOut のいずれかにこれらのデバイスの機能がアクセス*Xxx*と waveIn*Xxx*関数。 WDM オーディオ ドライバーをサポートできる wave 形式については、次を参照してください。 [ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)と[ **WAVEFORMATEXTENSIBLE**](https://msdn.microsoft.com/library/windows/hardware/ff538802)します。

A *wave レンダリング*フィルター wave デジタル オーディオ ストリーム入力として受け取るし、(スピーカーまたは外付けミキサーのセット) をオーディオ信号をアナログまたはデジタル オーディオ ストリームを (たとえばの S/PDIF コネクタ) を出力します。

A *wave キャプチャ*(や入力とマイクのジャック) からオーディオ信号をアナログまたはデジタルのストリーム (たとえばの S/PDIF コネクタ) からフィルターを入力として受け取ります。 同じフィルターは、デジタル オーディオ データを含む wave ストリームを出力します。

1 つのウェーブ フィルター レンダリングとキャプチャの両方を同時に実行することができます。 この種のフィルターは、たとえば、オーディオを再生する一連のスピーカーとオーディオの録音、マイクを同時に、オーディオ デバイスを表す場合があります。 または、wave レンダリングと wave キャプチャ ハードウェアとして表現されます、個別のウェーブ フィルター」の説明に従って[動的オーディオ サブデバイス](dynamic-audio-subdevices.md)します。

オーディオ ドライバーは、システムは、実装 wave ポートのドライバーとドライバーの一部として、ハードウェア ベンダーの実装、wave ミニポート ドライバーをバインドすることによって、wave フィルターを形成します。 ミニポート ドライバーは、wave フィルターは、すべてのハードウェア固有の操作を処理し、ポート ドライバーが汎用 wave-フィルターのすべての機能を管理します。

PortCls システム ドライバー (Portcls.sys) には、次の 3 つのウェーブ ポート ドライバーが実装されています。WaveRT、WavePci、および WaveCyclic です。

Wave フィルターの 3 種類がとおりに動作します。

-   A *WaveRT*フィルター wave データ バッファーを割り当てます、そのバッファーをユーザー モードのクライアントに直接アクセスすることになります。 バッファーは、wave デバイスのハードウェア機能に応じて、メモリの連続または不連続なブロックで構成できます。 クライアントでは、仮想メモリの連続したブロックとしてバッファーにアクセスします。 バッファーは、こと (レンダリング用)、デバイスの読み取りまたは書き込み (キャプチャ) のポインターが、バッファーの末尾に達すると、自動的にラップ バッファーの先頭には、周期。

-   A *WavePci*フィルターに直接アクセスするクライアントのバッファー。 クライアントでは、仮想メモリの 1 つ、連続したブロックとして、バッファーにアクセスする、フィルター、一連の連続していない可能性があるメモリのブロックとして、バッファーにアクセスする必要があります。 レンダリングまたはキャプチャ ストリームの連続部分を含むブロックで、デバイス キューします。 デバイスの読み取りまたは書き込みのポインターが 1 つのブロックの末尾に達すると、ときに、キューの次のブロックの先頭に移動します。

-   A *WaveCyclic*フィルターは、メモリ、出力 (レンダリング用) または (キャプチャ) の入力バッファーとして使用するための 1 つの連続したブロックで構成されるバッファーを割り当てます。 このバッファーは循環です。 バッファーが、クライアントに直接アクセス可能でないため、ドライバーはドライバーの循環バッファーと、クライアントのユーザー モード バッファー間でデータをコピーする必要があります。

WaveRT は、WavePci と WaveCyclic を勧めします。 WavePci と WaveCyclic は、Windows の以前のバージョンで使用されました。

WaveRT フィルターは、PCI や PCI Express などのシステム バス上に存在するオーディオ デバイスを表すことができます。 上、WaveCyclic WaveRT フィルターまたはフィルターの主な利点は、WaveRT フィルターできるオーディオ ハードウェアと直接オーディオ データを交換する、ユーザー モードのクライアントです。 これに対し、WaveCyclic および WavePci フィルターは両方では、オーディオ ストリームの待機時間が増加すると、ドライバーによって定期的なソフトウェアの介入が必要です。 さらに、スキャッター/ギャザー DMA 機能の有無にかかわらず、オーディオ デバイスは、WaveRT フィルターとして表されることができます。 詳細については、次を参照してください。、[リアルタイム オーディオ ストリーミング用のウェーブ ポート ドライバー](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WaveRTport.doc)ホワイト ペーパー。


### <a name="span-idwavertfilterspanspan-idwavertfilterspanwavert-filters"></a><span id="wavert_filter"></span><span id="WAVERT_FILTER"></span>WaveRT フィルター

WaveRT フィルターは、ポート/ミニポート ドライバーのペアとして実装されます。 Windows Vista 以降では、WaveRT フィルター ファクトリは WaveRT フィルターを次のように作成されます。

-   WaveRT のミニポート ドライバー オブジェクトがインスタンス化します。

-   呼び出すことによって、WaveRT ポート ドライバー オブジェクトをインスタンス化[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)の GUID 値**CLSID\_PortWaveRT**します。

-   ポート ドライバーの呼び出す[ **iport::init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)ポート ドライバーに、ミニポート ドライバーをバインドするメソッド。

コード例で[サブデバイス作成](subdevice-creation.md)このプロセスを示しています。 ポートおよびミニポートのドライバーがを介して相互に通信、 [IPortWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536920)と[IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)インターフェイス。

詳細については、次を参照してください。、[リアルタイム オーディオ ストリーミング用のウェーブ ポート ドライバー](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WaveRTport.doc)ホワイト ペーパー。

### <a name="span-idinformationforpreviousversionsofwindowsspanspan-idinformationforpreviousversionsofwindowsspanspan-idinformationforpreviousversionsofwindowsspaninformation-for-previous-versions-of-windows"></a><span id="Information_for_previous_versions_of_Windows"></span><span id="information_for_previous_versions_of_windows"></span><span id="INFORMATION_FOR_PREVIOUS_VERSIONS_OF_WINDOWS"></span>Windows の以前のバージョン情報

**Windows の以前のバージョンの WaveCyclic 情報**

WaveCyclic フィルターは、ISA、PCI、PCI Express、または PCMCIA などのシステム バスに接続するオーディオ デバイスを表すことができます。 このオプションを"WavePci"という名前のとおり、原則として、WavePci デバイスが代わりに接続が、ISA バスでは、たとえばに通常は、フィルターは、PCI バスに接続するデバイスを表します。 WaveCyclic でサポートされている単純なデバイスとは異なり WavePci でサポートされているデバイスは、スキャッター/ギャザー DMA の機能をいる必要があります。 オーディオ デバイスは、PCI バス上に存在するが、スキャッター/ギャザーがありません WaveCyclic フィルターがフィルターとしてではなく、DMA を表すことができます。

**Windows の以前のバージョンの WavePci 情報**

WavePci デバイスは、任意のメモリ アドレスに配置されていることと、任意のバイト アラインメントの終了を開始およびバッファーとの間のスキャッター/ギャザー DMA の転送を実行できます。 これに対し、WaveCyclic デバイス DMA ハードウェアまたはデバイスのミニポート ドライバーによって割り当てられる 1 つのバッファーからデータを移動する機能のみが必要です。 WaveCyclic ミニポート ドライバーは、DMA チャネルの機能が制限を満たしている循環バッファーを割り当てることは無料です。 たとえば、一般的な WaveCyclic デバイス DMA チャネルを次の制限を満たすバッファーが必要です。

-   バッファーは、物理アドレス空間の特定の領域にあります。

-   バッファーが連続するは、物理および仮想アドレス空間です。

-   バッファーが始まりも 4 または 8 バイト境界で終了します。

ある代わりにこのわかりやすいように、ただし、WaveCyclic デバイスする必要がありますに依存、循環バッファーとの間のデータのコピーをソフトウェア WavePci デバイスはこのようなコピーを回避するために、DMA ハードウェアのスキャッター/ギャザー機能を利用する一方です。 レンダリング デバイスを wave オーディオ データの提供またはキャプチャ デバイスからデータを取得を伴うデータのバッファーをオーディオ ストリームの一部を含むこれらのバッファーの各 Irp 表示されたり、キャプチャします。 WaveCyclic デバイスは、IRP から循環バッファーにデータをコピーすることが必要ですが、WavePci デバイスは、スキャッター/ギャザーの DMA エンジンから直接これらのバッファーにアクセスすることまたはその逆です。

### <a name="span-idwavepcifilterspanspan-idwavepcifilterspanwavepci-filters"></a><span id="wavepci_filter"></span><span id="WAVEPCI_FILTER"></span>WavePci フィルター

**注:Windows の以前のバージョンの WavePci 情報**

フィルターは、ポート/ミニポート ドライバーのペアとして実装されます。 WavePci フィルター ファクトリは、次のようにフィルターを作成します。

-   WavePci のミニポート ドライバー オブジェクトがインスタンス化します。

-   呼び出すことによって、WavePci ポート ドライバー オブジェクトをインスタンス化[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)の GUID 値**CLSID\_PortWavePci**します。

-   ポート ドライバーの呼び出す[ **iport::init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)ポート ドライバーに、ミニポート ドライバーをバインドするメソッド。

コード例で[サブデバイス作成](subdevice-creation.md)このプロセスを示しています。 ポートおよびミニポートのドライバーがを介して相互に通信、 [IPortWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536905)と[IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)インターフェイス。

詳細については、次を参照してください。 [WavePci デバイスの実装の問題](implementation-issues-for-wavepci-devices.md)します。

### <a name="span-idwavecyclicfilterspanspan-idwavecyclicfilterspanwavecyclic-filters"></a><span id="wavecyclic_filter"></span><span id="WAVECYCLIC_FILTER"></span>WaveCyclic フィルター

**注:Windows の以前のバージョンの WaveCyclic 情報**

WaveCyclic フィルターは、ポート/ミニポート ドライバーのペアとして実装されます。 WaveCyclic フィルター ファクトリは、次のように WaveCyclic フィルターを作成します。

-   WaveCyclic のミニポート ドライバー オブジェクトがインスタンス化します。

-   呼び出すことによって、WaveCyclic ポート ドライバー オブジェクトをインスタンス化[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)の GUID 値**CLSID\_PortWaveCyclic**します。

-   ポート ドライバーの呼び出す[ **iport::init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)ポート ドライバーに、ミニポート ドライバーをバインドするメソッド。

コード例で[サブデバイス作成](subdevice-creation.md)このプロセスを示しています。 ポートおよびミニポートのドライバーがを介して相互に通信、 [IPortWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536899)と[IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)インターフェイス。

WaveCyclic フィルターの循環バッファーは常に、仮想メモリの連続したブロックで構成されます。 ポート ドライバーの実装、 [ **IDmaChannel::AllocateBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff536553)メソッドは常に物理マシンと仮想メモリ アドレス空間内の連続したバッファーを割り当てます。 前述のように、WaveCyclic デバイスの DMA エンジンでバッファー メモリに追加の制約が課せられます場合、ミニポート ドライバーは自由にこれらの制約を満たすために、独自のバッファー割り当てメソッドを実装できます。

大きなバッファー (たとえば、8 の物理的に連続したメモリ ページ) の入力を求める WaveCyclic ミニポート ドライバーは、オペレーティング システムが元の要求を拒否した場合、バッファー サイズを小さくの決済を準備する必要があります。 オーディオ デバイスが場合によってはアンロードされ、システム リソースを再調整を再読み込みして (を参照してください[再調整するリソースへのデバイスを停止する](https://msdn.microsoft.com/library/windows/hardware/ff563877))。

WaveCyclic デバイス組み込み、バス マスターの DMA ハードウェアと呼ばれる、*マスター デバイス*します。 また、WaveCyclic デバイスもあります、*下位デバイス*組み込み DMA ハードウェア機能を持たない。 下位のデバイスは、必要なすべてのデータ転送を実行するシステムの DMA コント ローラーに依存するがします。 マスターおよび下位のデバイスの詳細については、次を参照してください。 [IDmaChannel](https://msdn.microsoft.com/library/windows/hardware/ff536547)と[IDmaChannelSlave](https://msdn.microsoft.com/library/windows/hardware/ff536548)します。

ミニポート ドライバーは、ポート ドライバーのいずれかによって作成される既定の DMA チャネル オブジェクトを使用する代わりに独自の DMA チャネル オブジェクトを実装できます WaveCyclic の新規*Xxx*もできます。

[**IPortWaveCyclic::NewMasterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536900)

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536902)

アダプタのドライバのカスタム[IDmaChannel](https://msdn.microsoft.com/library/windows/hardware/ff536547)実装は、特殊なハードウェアの制約を満たすようにデータのカスタム処理を実行できます。 たとえば、値を符号付きの関数を使用して、wave 形式の 16 ビットのサンプルを常には、Windows のマルチ メディアが符号なし 16 ビットの値を代わりに使用するオーディオ レンダリング ハードウェアを設計する場合があります。 この場合、ドライバーのカスタム[ **IDmaChannel::CopyTo** ](https://msdn.microsoft.com/library/windows/hardware/ff536558)符号付きのソースの値をハードウェアを必要とする符号なしの変換先の値に変換するメソッドを記述することができます。 この手法は、ハードウェア設計の欠陥を回避するための便利なことは、こと、ソフトウェアのオーバーヘッドの大幅なコストも発生です。

独自の DMA チャネル オブジェクトを実装するドライバーの例は、WDK の Sb16 サンプル オーディオ アダプターを参照してください。 定数をオーバーライドする場合\_DMA\_チャネルとして定義されている**TRUE**、ソース コードで条件付きコンパイル ステートメントは、独自の実装を有効にする[IDmaChannel](https://msdn.microsoft.com/library/windows/hardware/ff536547) 、IPortWaveCyclic::New から既定 IDmaChannel オブジェクトの代わりに、ドライバーを使用して、オブジェクト*Xxx*の呼び出しもできます。

 

 




