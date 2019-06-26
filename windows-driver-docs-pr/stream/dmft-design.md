---
title: デバイス MFT 設計ガイド
description: このトピックでは、すべてのストリームに共通の後処理を実行するために使用されるユーザー モードで実行されているデバイス全体にわたる拡張機能の設計について説明します。
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6f1ed6d0adf5043cd87c3be4902510c66ff0401a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358455"
---
# <a name="device-mft-design-guide"></a>デバイス MFT 設計ガイド

Windows でのビデオ キャプチャのスタックでは、MFT0 の形式でユーザー モードの拡張機能をサポートしています。 これは Ihv が指定し、キャプチャ パイプラインは、最初の変換では、取り込み後として挿入するストリームごとの拡張機能コンポーネントです。 MFT0 では、デバイスから、後処理のフレームを取り込まれます。 MFT0 内では、さらに後処理フレームに対する操作を実行できます。 

このトピックでは、すべてのストリームに共通の後処理を実行するために使用されるユーザー モードで実行されているデバイス全体にわたる拡張機能の設計について説明します。

## <a name="terminology"></a>用語

| 項目       | 説明                                                                                         |
|------------|-----------------------------------------------------------------------------------------------------|
| KS         | カーネル ストリーミング ドライバー                                                                             |
| AvStream   | オーディオ ドライバー モデルのビデオのストリーミング                                                                  |
| フィルター     | デバイス インスタンスを表すオブジェクト                                                            |
| デバイス MFT | Ihv によって提供されるユーザー モード キャプチャ ドライバーの拡張機能                                                 |
| Devproxy   | MF <> - AvStream マーシャラー                                                                           |
| DTM        | デバイス Transform Manager devproxy と MFT のデバイスを管理します。 MF パイプラインでデバイスを表します。|

## <a name="design-goals"></a>設計目標

- デバイス フィルターと同じ有効期間を持つデバイス フィルター全体のユーザー モードの拡張機能
- 任意の数のデバイスからの入力をサポートしています
- 任意の数の出力をサポートしています (現在の要件は次の 3 つのストリーム: プレビュー、レコード、および写真)
- デバイスのすべてのコントロールをデバイス MFT (を必要に応じて処理するか、デバイスに渡されます) にルーティングします。
- キャプチャされたストリームの処理を並列に投稿します。
- 3 a の処理を許可するフレーム レートに依存しません。
- 他のストリーム間で共有される 1 つのストリームからのメタデータを許可します。
- GPU リソースへのアクセス
- MF MMCSS 作業キューへのアクセス
- MF アロケーターへのアクセス
- シンプルなインターフェイス (MFT に似ています)
- IHV と OEM の拡張機能の柔軟性の高い内部アーキテクチャ

## <a name="design-constraints"></a>設計上の制約

- キャプチャの API サーフェスの変更はありません。
- 旧バージョンとの互換性を完了します。 たとえば、ない回帰レガシ アプリケーションとシナリオの操作中にします。

## <a name="capture-stack-architecture"></a>スタックのアーキテクチャをキャプチャします。

このトピックでは、キャプチャのドライバーをフィルター全体のユーザー モード拡張機能のサポートについて説明します。 このコンポーネントには、MF Api、スレッド プール、GPU と ISP のリソースへのアクセスがあります。 フィルターのワイド拡張機能は、任意の数のストリームをそれ自体と Ks デバイス間で、柔軟性を提供します。 フィルター。 この柔軟性により、今のところ、ユーザー モードの拡張機能と専用のメタデータと 3A 処理ストリームのために使用できるドライバーの間での帯域外通信ができます。

![スタックのアーキテクチャをキャプチャします。](images/capture-stack-architecture.png)

<br>
<br>

![デバイス mft アーキテクチャ](images/device-mft-architecture.png)

### <a name="device-transform-manager-dtm"></a>デバイス変換 Manager (DTM)

キャプチャのスタックには、新しいシステムで指定されたコンポーネントをデバイス変換 Manager (DTM) が導入されています。 これにより、DeviceSource の中に存在し、Devproxy MFT および MFT のデバイスを管理します。 DTM とは、メディアの種類のネゴシエーション、サンプルの反映、および MFT イベントのすべての処理です。 また、DeviceSource IMFTransform インターフェイスと DeviceSource がストリームのデバイスを管理する必要があるために必要なその他のプライベート インターフェイスも公開します。 このコンポーネントは、パイプラインから Devproxy とデバイス MFT を抽象化します。 パイプラインは、DTM をデバイスおよび DTM からストリームとして、デバイスにストリームとしてだけ表示されます。

### <a name="devproxy"></a>Devproxy

Devproxy では、非同期コマンドと AvStream カメラ ドライバーおよび Media Foundation 間のビデオのフレームをマーシャ リングする MFT です。 これをサポートしている Windows によって提供されます*n*カメラ ドライバーからの出力の数。 また、デバイスによって公開されているすべてのピンのアロケーターを所有しています。

### <a name="device-mft"></a>デバイス MFT

デバイス MFT は、キャプチャ ドライバーへの拡張機能をユーザー モードです。 *M n x*非同期 MFT します。 キャプチャのドライバーを使用したシステムにインストールし、キャプチャのドライバーのベンダーによって提供されます。

デバイス MFT の入力ストリームの数は、デバイスによって公開される Ks ピンの数と同じである必要があります。 デバイス MFT の入力ストリームでサポートされている mediatypes は KS ピンによって公開される mediatypes と同じである必要があります。

デバイス MFT によって公開されている出力ストリームの数は、DeviceSource とキャプチャのスタックに表示される、ストリームは、API とアプリケーションをキャプチャおよび 1 つ、2 つ、または 3 つのストリームにすることができます。 デバイス MFT の入力と出力ストリームの数は同じである必要はありません。 また、入力し、出力ストリームは、同じの mediatypes させる必要はありません異なる mediatypes、通常になります。 Mediatypes 数は、いずれかとも一致しない必要があります。

Devproxy でユーザー モードで表される最初の Ks Pin には、デバイス、MFT MFT、デバイスの 2 つ目の入力ストリームで Devproxy の出力ストリームによってユーザー モードで表される 2 つ目の Ks Pin の最初の入力ストリームに関連付けられたストリームを取得の出力です。

デバイス MFT が Devproxy、DX のデバイスへのポインターを指定し、MF ワーク キューの id。 デバイスから送信されたフレームは、MF サンプルとして、対応するデバイス MFT の入力に直接読み込まれます。 これらのデバイス MFT 投稿できるすべてキャプチャされたサンプルを処理し、プレビュー、レコード、および写真ピンにサンプルを提供します。

すべてのコマンドとコントロールが、デバイスには、デバイス MFT に再ルーティングされます。 デバイス MFT は、コントロールを処理または Devproxy を使ってドライバーに渡します。 これには、キャプチャのドライバー スタックは、コマンド処理が効率化します。

## <a name="functional-overview"></a>機能の概要

デバイスのデバイス MFT がある場合、キャプチャ パイプラインの初期設定で DeviceSource には、DTM がインスタンス化します。 DTM の初期化ルーチンへのデバイスを表す Devproxy のインスタンスを渡します。 DTM 併置デバイス MFT を作成し、基本的な検証、verifes Devproxy の出力ピンの数は同じデバイスの MFT の入力ピンの数が必須のインターフェイスのサポートし、など。

DeviceSource クエリ DTM をサポートされている出力 mediatypes を取得します。 DTM を使用して、これらのデバイス MFT の出力ピンから取得します。 DeviceSource がプレゼンテーションの記述子を公開し、キャプチャ パイプラインには、この情報に基づいて Stream 記述子。

SourceReader では、DeviceSource の公開されている mediatypes を使用し、各ストリームで既定 mediatypes を設定します。 さらに、DeviceSource 既定 mediatypes の DTM の出力ストリームを設定します。 DTM を使用して、デバイス MFT の出力ストリームに、メディアの種類の設定、 [SetOutputStreamState](https://docs.microsoft.com/windows/desktop/api/mftransform/nf-mftransform-imfdevicetransform-setoutputstreamstate)メソッド。

ときに**SetOutputStreamState**を呼び出すと、その入力ストリームのメディアの種類を変更するには、DTM にメッセージが選択されている出力メディアの種類に基づくデバイス MFT 投稿し、待機します。 このメッセージでは、DTM クエリを使用して、デバイス MFT の入力ストリームの優先入力メディアの種類への応答で[GetPreferredInputStreamState](https://docs.microsoft.com/windows/desktop/api/mftransform/nf-mftransform-imfdevicetransform-getinputstreampreferredstate)します。 これにより、Devproxy の対応する出力ストリームに、メディアの種類が設定されます。 成功する場合、DTM は SetInputStreamState を使用して、デバイス MFT の入力ストリームにその同じメディアの種類を設定します。 デバイス MFT の完了後、この呼び出しを受信するには、 **SetOutputStreamState**します。

CaptureEngine は、DeviceSource で特定のストリームを有効にすると個別のストリームを選択します。 これを通じて DTM によってデバイス MFT に伝達は、 **SetOutputStreamState**呼び出します。 デバイス MFT は、要求された状態で、特定の出力ストリームを配置します。 前述のように、デバイス MFT はまた、DTM を有効にする必要があるために必要な入力ストリームの詳細通知します。 これは、結果、DTM Devproxy にストリーム選択を反映します。 このプロセスの最後に、Devproxy とデバイスの MFT 内のすべての必要なストリームは、ストリームができています。

SourceReader は CaptureEngine ReadSample を呼び出すときに、DeviceSource を開始します。 さらに、DeviceSource は、パイプラインの開始を示す MFT_MESSAGE_NOTIFY_BEGIN_STREAMING および MFT_MESSAGE_NOTIFY_START_OF_STREAM のメッセージを送信することによって、DTM を開始します。 DTM は MFT_MESSAGE_NOTIFY_BEGIN_STREAMING および MFT_MESSAAGE_NOTIFY_START_OF_STREAM メッセージ伝達することで Devproxy とデバイス MFT を開始します。 

**注**デバイス MFT 初期化ではなくストリーミングの開始時に必要なリソースを割り当てます。

DTM 呼び出し**SetOutputStreamState**ストリーミング状態パラメーターを使用してデバイス MFT の出力にします。 デバイス MFT は、これらの出力ストリームでは、ストリーミングを開始します。 DTM が有効なメディアの種類を設定する Devproxy 出力ストリームにストリーミングを開始します。 Devproxy サンプルは、割り当て、デバイスからそれらをフェッチします。 これらのサンプルは、関連する入力ピンにデバイス MFT に渡します。 デバイス MFT は、これらのサンプルを処理し、DeviceSource への出力を提供します。 DeviceSource からサンプルを CaptureEngine SourceReader を通過します。

CaptureEngine は、DeviceSource 上の内部のインターフェイスを通じて個別のストリームを無効にして個別のストリームを停止します。 これは、特定の出力デバイス MFT 経由でストリームが無効にするのに変換**SetOutputStreamState**します。 さらに、デバイス MFT がを通じて特定の入力ストリームを無効化を要求する場合があります**METransformInputStreamStateChanged**イベント。 DTM には、対応する Devproxy ストリームにこれが反映されます。

デバイス MFT ストリーミング状態で、要求できる限り、任意の入力ストリームが有効な DeviceStreamState のいずれかに移行します。 たとえば、他のストリームに影響を与えずに DeviceStreamState_Stop または DeviceStreamState_Run または DeviceStreamState_Pause を送信、でした。

ただし、出力ストリームの切り替えは、キャプチャ パイプラインによって制御されます。 たとえば、プレビュー、レコード、およびフォト ストリームを有効または無効にキャプチャ パイプラインによって。 出力は無効になっている場合でも、入力ストリームはでした自体デバイス MFT ストリーミングの状態にある限りはストリーミングもします。

![デバイス mft パイプライン プレビュー シーケンス](images/device-mft-pipeline-preview-sequence.png)

<br>
<br>

![デバイス mft 写真のシーケンスを実行します。](images/device-mft-take-photo-sequence.png)


### <a name="lifetime-of-device-mft"></a>デバイス MFT の有効期間

KS フィルターが作成されたら、デバイス MFT が読み込まれます。 これがアンロードされる KS フィルターが閉じられる前にします。

パイプラインの観点から、DeviceSource が作成されると、デバイス MFT が作成され、デバイス MFT がシャット ダウンを同期的には、DeviceSource がシャット ダウンのとき。

シャット ダウンをサポートするデバイス MFT をサポートする必要があります、 **IMFShutdown**インターフェイス。 後**デバイス MFT シャット ダウン]-> [** を呼び出すと、その他のインターフェイス、デバイス MFT への呼び出しは MF_E_SHUTDOWN エラーを返す必要があります。

### <a name="memory-type"></a>メモリの種類

システム メモリのバッファー、またはカメラ ドライバーの基本設定ごとの DX メモリ バッファーには、フレームをキャプチャできます。 さらに処理するためのデバイス MFT にカメラのドライバーはどのようなバッファーが取り込まれる直接します。

Devproxy では、ドライバーの設定に基づいたバッファーを割り当てます。 メインフレームを使用するようデバイス MFT ですがアロケーター-force-inplace 以外の変換、出力ピンの必要なサンプルを割り当てることの Api。

### <a name="mediatype-change-while-streaming"></a>ストリーミング中のメディアの種類の変更

SourceReader のクライアントは、そのネイティブ デバイス MFT の出力ストリームによって公開される mediatypes mediatypes がサポートされていること。 ネイティブのメディアの種類が変更されたときに、SourceReader は DeviceSource を介してデバイス MFT にメディアの種類の通知呼び出しを送信します。 そのストリームのキューからの保留中のすべてのサンプルをフラッシュし、適切なタイミングで、そのストリームに対する新しいメディアの種類を切り替えるデバイス MFT の役目です。 入力メディアの種類を変更する必要がある場合は、1 つを現在の入力メディアの種類を変更があります。 DTM はデバイス MFT の入力ストリームから現在のメディアの種類を取得し、ネイティブ mediatype 変更のたびに Devproxy の出力ストリームや、デバイス MFT の入力を設定します。

### <a name="input-mediatype-change-in-device-mft"></a>デバイス MFT の入力メディアの種類の変更

これはあるため、 *m n x* MFT、可能性がある影響入力ピンの mediatypes をストリーミングにストリーミングの pin の mediatypes の出力時に状態の変更や状態の変化と。 具体的には、次の変更が発生した場合。

- 出力メディアの種類の変更

    - アプリケーションでネイティブ メディアの種類が変更されたときに重ねて表示キャプチャ スタックを通じてデバイス MFT に出力ピン留めするメディアの種類の変更としてします。

    - ときに、メディアの種類の変更を出力、入力メディアの種類の変更をトリガーする可能性が。 たとえば、すべての出力ピンが 720 p でストリーミングされます。 これは、結果、720 p でカメラからストリーミングします。 次に、レコードのストリームの変更を 1080p にネイティブ、mediatype と仮定します。 その場合は、そのメディアの種類を変更するレコードのストリームにデータをフェッチしていますが、デバイス MFT 入力ストリームのいずれかになります。

- 出力ピンが無効になっています

    - 最適化では、1 つ以上の出力で、同じ入力が共有すると、アプリケーション プログラムがデバイス MFT の出力のいずれか無効にされた場合、入力は、メディアの種類を変更する必要があります。 たとえば、1080 p の出力ストリームが停止し、その他のすべてのストリームが場合、は、720 p でストリーミングは、1 つの入力を共有し、入力ストリームは、720 p 電力の節約し、パフォーマンスを向上するにそのメディアの種類を変更する必要があります。

DTM ハンドル[METransformInputStreamStateChanged](https://docs.microsoft.com/windows-hardware/drivers/stream/metransforminputstreamstatechanged)メディアの種類とデバイス MFT 入力とこれらの条件下で Devproxy 出力の状態を変更するデバイス MFT からの通知。

### <a name="flush-device-mft"></a>フラッシュ デバイス MFT

2 種類のフラッシュが必要なデバイス MFT を管理するときに。

- グローバルのフラッシュ

    - デバイス全体にわたる MFT フラッシュします。 通常、これは、DTM がデバイス MFT にメッセージをストリーミングの停止を送信するときに発生します。

    - デバイス MFT は、その入力と出力キューからすべてのサンプルをドロップし、同期的に返すと想定されます。

    - デバイス MFT の新しい入力を要求または新しい使用可能な出力に関する通知を送信する必要がありますされません。

- ローカル フラッシュ

    - 出力ピンに固有のフラッシュします。 これは通常、ストリームが停止したときに発生します。

フラッシュする前にポストされたすべてのイベントは、デバイス MFT マネージャーによって削除されます。 その内部のフラッシュ後にデバイス MFT リセット[METransformHaveOutput](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformhaveoutput)数を追跡します。

### <a name="drain-of-device-mft"></a>デバイス MFT のドレイン

ドレイン ライブ キャプチャ ソース内の必要性がないために、デバイス MFT は s ドレインが個別のメッセージを受信しません。

### <a name="photo-trigger"></a>写真のトリガー

このモデルで、写真のトリガー フォト シーケンス開始、停止トリガーに直接送信する代わりに、ドライバー、されるデバイス MFT に再ルーティングします。 デバイス MFT はトリガーを処理または、必要に応じて、カメラのドライバーに転送します。

### <a name="warm-start"></a>ウォーム スタート

DeviceSource ウォーム スタート遷移すると、ストリームの状態を一時停止する特定の出力ストリームしようとします。 さらに、DTM を呼び出す、 [IMFDeviceTransform::SetOutputStreamState](https://docs.microsoft.com/windows/desktop/api/mftransform/nf-mftransform-imfdevicetransform-setoutputstreamstate)デバイス MFT 状態を一時停止する特定の出力ストリームに移行するメソッド。 これは、結果を一時停止にする場合は、対応する入力ストリーム。 これは、要求することによってデバイス MFT で実現されます**METransformInputStreamStateChanged** DTM を処理、 [IMFDeviceTransform::SetInputStreamState](https://docs.microsoft.com/windows/desktop/api/mftransform/nf-mftransform-imfdevicetransform-setinputstreamstate)メソッド。

### <a name="variable-photo-sequence"></a>可変の写真シーケンス

このアーキテクチャでは、写真のシーケンスはデバイス MFT、カメラのデバイス ドライバーの複雑さを大幅に減少とカメラのデバイス ドライバーで実装されます。 開始、停止の写真シーケンス トリガーでは、デバイス MFT に送信され、写真のシーケンスをより簡単に処理します。

### <a name="photo-confirmation"></a>写真の確認

写真を使用して確認をサポートするデバイス MFT、 **IMFCapturePhotoConfirmation**インターフェイス。 パイプラインを使用して、このインターフェイスを取得します[IMFGetService::GetService](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfgetservice-getservice)メソッド。

### <a name="metadata"></a>メタデータ

Devproxy はメタデータのバッファー サイズのドライバーを照会し、メタデータのメモリを割り当てます。 ドライバーからのメタデータは、サンプルをまだ Devproxy によって設定されます。 デバイス MFT は、サンプルのメタデータを消費します。 メタデータする、出力ストリームにサンプル渡されるか、その投稿の処理に使用されるだけです。

任意の数の入力をサポートしているデバイス MFT、専用の入力ピンには、メタデータや帯域外のメタデータだけ使用できます。 このピンのメディアの種類がカスタムし、ドライバーがバッファーの数とサイズを決定します。

このメタデータのストリームは、DTM を超える公開されます。 デバイス MFT ストリーミングの開始時に状態をストリーミングには、ストリームを配置することができます。 たとえば、出力ストリームは、ストリーミング用に選択したら、デバイス MFT を要求できます DTM を 1 つまたは複数のビデオ ストリームと同様に、メタデータ ストリームの開始を使用して、 **METransformInputStreamStateChanged**イベント。 

注:このモデルでは、出力ピンの数と一致する入力ピンの数の要件はありません。 別の pin をメタデータまたは 3A だけ専用できます。

## <a name="device-transform-manager-dtm-event-handling"></a>デバイス マネージャーの変換 (DTM) イベントの処理

[デバイス マネージャーの変換イベント](https://docs.microsoft.com/windows-hardware/drivers/stream/device-mft-events)以下の参照トピックで定義されます。

- [METransformFlushInputStream](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformflushinputstream)
- [METransformHaveOutput](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformhaveoutput)
- [METransformInputStreamStateChanged](https://docs.microsoft.com/windows-hardware/drivers/stream/metransforminputstreamstatechanged)
- [METransformNeedInput](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformneedinput)


## <a name="imfdevicetransform-interface"></a>IMFDeviceTransform インターフェイス

[IMFDeviceTransform](https://docs.microsoft.com/windows/desktop/api/mftransform/nn-mftransform-imfdevicetransform)デバイス MFT と対話するインターフェイスを定義します。 このインターフェイスの管理を容易に*m*入力と*n*デバイス MFT を出力します。 その他のインターフェイスとデバイス MFT は、このインターフェイスを実装する必要があります。

### <a name="general-event-propagation"></a>一般的なイベントの伝達

Devproxy (または、デバイス内で)、イベントが発生したときにデバイス MFT して、DeviceSource を伝達する必要があります。

## <a name="device-mft-requirements"></a>デバイス MFT 要件

### <a name="interface-requirements"></a>インターフェイスの要件

デバイスの仕様では、次のインターフェイスをサポートする必要があります。

- [IMFDeviceTransform](https://docs.microsoft.com/windows/desktop/api/mftransform/nn-mftransform-imfdevicetransform)

- [IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nn-ks-ikscontrol)

    - これにより、すべての ksproperties、イベントおよびデバイス MFT を経由するメソッド。 これにより、デバイス MFT はデバイス MFT 内でこれらの関数呼び出しを処理またはだけドライバーに転送する機能。 場所、KsEvent メソッドを処理し、デバイス MFT は、次を実行する必要がありますの場合。

        - デバイス MFT はいずれかが処理する場合**KSEVENT_TYPE_ONESHOT**イベント、その後の受信時に、ハンドルを複製**KSEVENT_TYPE_ENABLE**します。

        - 呼び出し元に戻す設定またはイベントを発生させる場合、 **CloseHandle**重複のハンドル。

        - デバイス MFT KSEVENT_TYPE_ONESHOT 非イベントを処理するかどうかは、受信時にハンドルを複製する必要があります、 **KSEVENT_TYPE_ENABLE**を呼び出すと**CloseHandle** ks イベントを処理で重複しています。最初のパラメーター (ks イベント id) と 2 番目のパラメーター (イベントの長さ) がゼロに設定を持つ KsEvent 関数を呼び出すことによって無効になります。 イベント データと長さが有効になります。 イベント データは、特定 ks イベントを一意に識別します。

        - デバイス MFT KSEVENT_TYPE_ONESHOT 非イベントを処理するかどうかは、受信時にハンドルを複製する必要があります、 **KSEVENT_TYPE_ENABLE**呼び出す必要がありますと**CloseHandle**処理で重複しているときに、ksイベントはすべてのパラメーターを 0 に設定を持つ KsEvent 関数を呼び出すことによって無効になります。

- [IMFRealtimeClientEx](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfrealtimeclientex)

- [IMFMediaEventGenerator](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)

- [IMFShutdown](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfshutdown)

### <a name="notification-requirements"></a>通知の要件

デバイスの仕様では、サンプルや、任意の入力ストリームの状態の変更の有無について DTM を通知するために、次のメッセージを使用する必要があります。

- [METransformHaveOutput](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformhaveoutput)

- [METransformInputStreamStateChanged](https://docs.microsoft.com/windows-hardware/drivers/stream/metransforminputstreamstatechanged)

- [METransformFlushInputStream](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformflushinputstream)

### <a name="thread-requirements"></a>スレッドの要件

デバイス MFT は、独自のスレッドを作成しないでください。 を通じて渡される ID を持つ、MF 作業キューを使用する必要があります代わりに、 [IMFRealtimeClientEx](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfrealtimeclientex)インターフェイス。 これは、デバイス MFT で実行されているすべてのスレッドが位置キャプチャ パイプラインが実行されている適切な優先順位を取得するかどうかを確認します。 それ以外の場合の優先順位の逆転のスレッドを引き起こす可能性が。

### <a name="inputstream-requirements"></a>InputStream 要件

#### <a name="stream-count"></a>Stream の数

- デバイス MFT で入力ストリームの数は、ドライバーでサポートされているストリームの数と同じである必要があります。

#### <a name="mediatypes"></a>MediaTypes

- Mediatypes とデバイス MFT の入力でサポートされている実際のメディアの種類の数は、ドライバーでサポートされている mediatypes の種類と数に一致する必要があります。

- デバイス MFT の入力でサポートされている mediatypes ドライバーでサポートされている mediatypes のサブセットである場合にのみ異なる、数は使用できます。

- ドライバーとデバイス MFT の入力によってサポートされている mediatypes には、標準またはカスタム mediatypes 可能性があります。

### <a name="to-register-device-mft"></a>MFT のデバイスを登録するには

カメラ デバイス INF デバイス MFT のコクラスの CLSID を指定する次のデバイス インターフェイスのエントリが必要です。

```INF
[CaptureAvstrm.Device.NTarm.Interfaces]
AddInterface = %KSCATEGORY_VIDEO_CAMERA%, %Capture.FilterDescBack%, Capture.FilterBack

[Capture.FilterBack]
AddReg = Capture.FilterBack.AddReg, PinNames.AddReg

[Capture.FilterBack.AddReg]
HKR,,FriendlyName,,%Capture.FilterDescBack%
HKR,,CameraDeviceMftClsid,,%CameraDeviceMFT.Clsid%
```

上記の INF エントリは、次のレジストリ キーが入力されている発生します。
    
**注**これは、例のみ (実際のレジストリではありません)

```console
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{E5323777-F976-4f5b-9B55-B94699C46E44}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{E5323777-F976-4f5b-9B55-B94699C46E44}\#GLOBAL\Device Parameters]
"CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
"FriendlyName"="USB Video Device"
"CameraDeviceMftClsid"="{3456A71B-ECD7-11D0-B908-00A0C9223196}"<<< Device MFT CoClass ID >>>
```
