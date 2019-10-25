---
title: デバイス MFT 設計ガイド
description: このトピックでは、すべてのストリームに共通する後処理を実行するために使用できる、ユーザーモードで実行されるデバイス全体の拡張機能の設計の概要について説明します。
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 66d1b9bd208f31be1b7bcb17e5f0b4dcadef9f77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842642"
---
# <a name="device-mft-design-guide"></a>デバイス MFT 設計ガイド

Windows のビデオキャプチャスタックでは、DMFT の形式でユーザーモードの拡張機能をサポートしています。 これは、Ihv が提供するデバイスごとの拡張コンポーネントであり、キャプチャパイプラインは最初の変換であるキャプチャとして挿入されます。 DMFT は、デバイスから処理後のフレームを受信します。 さらに、フレームに対する後処理操作は、DMFT 内で行うことができます。 DMFT は、デバイスのすべてのストリームからフレームを受け取ることができ、要件に従って任意の数の出力ストリームを公開できます。

このトピックでは、すべてのストリームに共通する後処理を実行するために使用できる、ユーザーモードで実行されるデバイス全体の拡張機能の設計の概要について説明します。

## <a name="terminology"></a>用語

| 用語       | 説明                                                                                         |
|------------|-----------------------------------------------------------------------------------------------------|
| KS         | カーネルストリーミングドライバー                                                                             |
| AvStream   | オーディオビデオストリーミングドライバーモデル                                                                  |
| フィルター     | デバイスインスタンスを表すオブジェクト                                                            |
| デバイスの MFT | Ihv によって提供されるユーザーモードキャプチャドライバーの拡張機能                                                 |
| Devproxy   | MF <-> AvStream マーシャラー                                                                           |
| DTM        | Devproxy とデバイス MFT を管理するデバイス変換マネージャー。 MF パイプラインのデバイスを表します。|

## <a name="design-goals"></a>設計目標

- デバイスフィルターと同じ有効期間を持つデバイスフィルター全体のユーザーモード拡張機能
- デバイスから受信する任意の数の入力をサポートします。
- 任意の数の出力をサポートします (現在の要件は、プレビュー、レコード、写真の3つのストリームです)
- すべてのデバイスコントロールをデバイス MFT にルーティングします (必要に応じてデバイスを処理またはデバイスに渡します)。
- キャプチャされたストリームの並列ポスト処理
- フレームレートに依存しない3A の処理を許可する
- 1つのストリームのメタデータを他のストリーム間で共有できるようにする
- GPU リソースへのアクセス
- MF MMCSS Work キューへのアクセス
- MF アロケーターへのアクセス
- 単純なインターフェイス (MFT に似ています)
- IHV/OEM の拡張性のための柔軟な内部アーキテクチャ

## <a name="design-constraints"></a>設計上の制約

- Capture API サーフェイスに変更はありません
- 旧バージョンとの互換性を確保します。 たとえば、レガシアプリとシナリオでの作業中に回帰が発生することはありません。

## <a name="capture-stack-architecture"></a>キャプチャスタックのアーキテクチャ

このトピックでは、キャプチャドライバーに対するフィルターレベルのユーザーモード拡張機能のサポートについて説明します。 このコンポーネントは、MF Api、スレッドプール、GPU、および ISP リソースにアクセスできます。 フィルターのワイド拡張では、それ自体とデバイス Ks フィルターの間に任意の数のストリームを柔軟に含めることができます。 この柔軟性により、ユーザーモード拡張機能とドライバーの間で帯域外通信をシームレスにことができるようになります。これは、専用のメタデータおよび3A 処理ストリームに使用できます。

![キャプチャスタックのアーキテクチャ](images/capture-stack-architecture.png)

<br>
<br>

![デバイスの mft アーキテクチャ](images/device-mft-architecture.png)

### <a name="device-transform-manager-dtm"></a>デバイス変換マネージャー (DTM)

キャプチャスタックには、新しいシステム指定のコンポーネントである Device Transform Manager (DTM) が導入されています。 これは、デバイス Ource 内に存在し、Devproxy MFT とデバイス MFT を管理します。 DTM は、MediaType ネゴシエーション、サンプル伝達、およびすべての MFT イベント処理を行います。 また、デバイス ource の IMFTransform インターフェイスと、デバイスのストリームを管理するために必要なその他のプライベートインターフェイスも公開されています。 このコンポーネントは、パイプラインから Devproxy と Device MFT を抽象化します。 パイプラインは、デバイスとして DTM を、デバイスストリームとして DTM からストリームアウトします。

### <a name="devproxy"></a>Devproxy

Devproxy は、AvStream カメラドライバーとメディアファンデーションの間でコマンドとビデオフレームをマーシャリングする非同期の MFT です。 これは Windows によって提供され、カメラドライバーからの*n 個*の出力をサポートしています。 また、これは、デバイスによって公開されているすべてのピンのアロケーターを所有しています。

### <a name="device-mft"></a>デバイスの MFT

デバイス MFT は、キャプチャドライバーに対するユーザーモードの拡張機能です。 これは*m x n*非同期 MFT です。 キャプチャドライバーを使用してシステムにインストールされ、capture driver ベンダによって提供されます。

デバイス MFT の入力ストリームの数は、デバイスによって公開されている Ks pin の数と同じである必要があります。 デバイスの MFT の入力ストリームでサポートされる mediatypes は、KS ピンによって公開されている mediatypes と同じである必要があります。

デバイス MFT によって公開される出力ストリームの数は、デバイス Ource とキャプチャスタック、キャプチャ API、およびアプリケーションによって見られるストリームであり、1つ、2つ、または3つのストリームにすることができます。 デバイス MFT の入力ストリームと出力ストリームの数は、同じである必要はありません。 また、入力ストリームと出力ストリームは同じ mediatypes を持つ必要はなく、通常は異なる mediatypes を持ちます。 Mediatypes の数が一致していない必要があります。

Devproxy の出力ストリームによってユーザーモードで表される最初の Ks Pin は、デバイス MFT の最初の入力ストリームに関連付けられます。ユーザーモードで表される2番目の Ks ピンは、デバイス MFT の2番目の入力ストリームと共に、Devproxy の出力ストリームによって表されます。

デバイス MFT には、Devproxy、DX デバイス、および MF ワークキュー ID へのポインターが付与されます。 デバイスから送られるフレームは、対応するデバイスの MFT の入力に、MF サンプルとして直接取り込まれます。 これらすべてを使用して、デバイスの MFT は、キャプチャしたサンプルを処理し、プレビュー、レコード、およびフォトピンのサンプルを提供できます。

デバイスに送られるすべてのコマンドとコントロールがデバイス MFT に再ルーティングされます。 デバイス MFT は、コントロールを処理するか、Devproxy を使用してドライバーに渡します。 これにより、キャプチャドライバースタックによるコマンド処理が効率化されます。

## <a name="functional-overview"></a>機能の概要

キャプチャパイプラインの初期化時に、デバイスのデバイス MFT がある場合は、デバイス Ource によって DTM がインスタンス化されます。 このメソッドは、デバイスを表す Devproxy のインスタンスを DTM の初期化ルーチンに渡します。 DTM co はデバイス MFT を共同で作成し、基本的な検証を実行します。たとえば、Devproxy の出力ピンの数は、デバイスの MFT の入力ピンの数と同じであること、必須インターフェイスのサポートなどが verifes ます。

サポートされている出力 mediatypes を取得するためのデバイスの Ource。 これらの値は、デバイスの MFT の出力ピンから取得されます。 デバイス Ource は、この情報に基づいてプレゼンテーション記述子とストリーム記述子をキャプチャパイプラインに公開します。

SourceReader は、デバイス Ource の公開された mediatypes を使用し、各ストリームに既定の mediatypes を設定します。 さらに、デバイス Ource は DTM の出力ストリームに既定の mediatypes を設定します。 DTM は、 [Setoutputstreamstate](https://docs.microsoft.com/windows/desktop/api/mftransform/nf-mftransform-imfdevicetransform-setoutputstreamstate)メソッドを使用して、デバイスの MFT の出力ストリームに mediatype を設定します。

**Setoutputstreamstate**が呼び出されると、デバイス MFT は、選択された出力の mediatype と待機に基づいて入力ストリームの mediatype を変更するために、dtm にメッセージを送信します。 このメッセージに対する応答として、DTM は[GetPreferredInputStreamState](https://docs.microsoft.com/windows/desktop/api/mftransform/nf-mftransform-imfdevicetransform-getinputstreampreferredstate)を使用してデバイス MFT の入力ストリームに対して優先入力メディアを指定します。 これにより、Devproxy の対応する出力ストリームに mediatype が設定されます。 これが成功した場合、DTM は SetInputStreamState を使用して、デバイスの MFT の入力ストリームに同じ mediatype を設定します。 この呼び出しを受け取った後、デバイスの MFT は**Setoutputstreamstate**を完了します。

CaptureEngine は、デバイス Ource で特定のストリームを有効にすることで、個々のストリームを選択します。 これは、 **Setoutputstreamstate**呼び出しによって dtm によってデバイス MFT に反映されます。 デバイス MFT は、要求された状態で特定の出力ストリームを配置します。 前述のように、デバイス MFT は、有効にする必要がある必要な入力ストリームについても DTM に通知します。 結果として、ストリームの選択が Devproxy に反映されます。 このプロセスの最後に、Devproxy と Device MFT で必要なすべてのストリームをストリーム配信する準備ができました。

SourceReader は、CaptureEngine が ReadSample を呼び出すときに、デバイス Ource を開始します。 さらに、デバイス Ource は、パイプラインの開始を示す MFT_MESSAGE_NOTIFY_BEGIN_STREAMING メッセージと MFT_MESSAGE_NOTIFY_START_OF_STREAM メッセージを送信することによって DTM を開始します。 DTM は、MFT_MESSAGE_NOTIFY_BEGIN_STREAMING メッセージと MFT_MESSAAGE_NOTIFY_START_OF_STREAM メッセージを伝達することによって Devproxy とデバイス MFT を起動します。 

**メモ**Device MFT initialize ではなく、開始ストリーミングに必要なリソースを割り当てます。

DTM は、ストリーミング状態パラメーターを使用して、デバイスの MFT の出力で**Setoutputstreamstate**を呼び出します。 デバイス MFT は、これらの出力ストリームでストリーミングを開始します。 DTM は、有効な mediatype が設定されている Devproxy 出力ストリームでストリーミングを開始します。 Devproxy はサンプルを割り当て、デバイスからそれらをフェッチします。 これらのサンプルは、関連する入力ピンのデバイス MFT に取り込まれます。 デバイス MFT は、これらのサンプルを処理し、出力をデバイス Ource に渡します。 デバイス Ource から、サンプルは SourceReader から CaptureEngine に流れます。

CaptureEngine は、デバイス Ource の内部インターフェイスを介して個々のストリームを無効にすることで、個々のストリームを停止します。 これは、 **Setoutputstreamstate**を通じてデバイス MFT で特定の出力ストリームを無効にするために変換されます。 デバイスの MFT は、 **METransformInputStreamStateChanged**イベントを使用して特定の入力ストリームの無効化を要求する場合があります。 DTM は、対応する Devproxy ストリームにこれを反映します。

デバイスの MFT 自体がストリーミング状態である限り、任意の入力ストリームを任意の有効な DeviceStreamState に移行するように要求できます。 たとえば、他のストリームに影響を与えずに、DeviceStreamState_Stop、DeviceStreamState_Run、DeviceStreamState_Pause などに送信できます。

ただし、出力ストリームの遷移は、キャプチャパイプラインによって制御されます。 たとえば、プレビュー、レコード、およびフォトストリームは、キャプチャパイプラインによって有効または無効にされます。 出力が無効になっている場合でも、デバイスの MFT 自体がストリーミング状態である限り、入力ストリームがストリーミングされる可能性があります。

![デバイス mft パイプラインのプレビューシーケンス](images/device-mft-pipeline-preview-sequence.png)

<br>
<br>

![デバイスの mft による写真の撮影](images/device-mft-take-photo-sequence.png)


### <a name="lifetime-of-device-mft"></a>デバイス MFT の有効期間

KS フィルターを作成した後に、デバイスの MFT が読み込まれます。 これは、KS フィルターを閉じる前にアンロードされます。

パイプラインの観点からは、デバイス Ource が作成されるとデバイスの MFT が作成され、デバイスの Ource がシャットダウンされると、デバイスの MFT は同期的にシャットダウンされます。

シャットダウンをサポートするには、デバイスの MFT が**Imfshutdown**インターフェイスをサポートしている必要があります。 **デバイス mft の > シャットダウン**が呼び出された後、デバイス mft へのその他のインターフェイス呼び出しでは、MF_E_SHUTDOWN エラーが返される必要があります。

### <a name="memory-type"></a>メモリの種類

フレームは、カメラドライバーの設定に従って、システムメモリバッファーまたは DX メモリバッファーにキャプチャできます。 カメラドライバーから取得されたすべてのバッファーは、さらに処理するためにデバイス MFT に直接取り込まれます。

Devproxy は、ドライバーの設定に基づいてバッファーを割り当てます。 デバイス MFT では、MF アロケーター Api を使用して、非インプレース変換の出力ピンに必要なサンプルを割り当てる必要があります。

### <a name="mediatype-change-while-streaming"></a>ストリーミング中の Mediatype の変更

SourceReader のクライアントは、ネイティブでサポートされている mediatypes として、デバイスの MFT の出力ストリームによって公開されている mediatypes を表示できます。 ネイティブの mediatype が変更されると、SourceReader は、デバイスの Ource を介して、mediatype 通知呼び出しをデバイス MFT に送信します。 デバイス MFT は、そのストリームのキューから保留中のすべてのサンプルをフラッシュし、そのストリームの新しい mediatype に適切なタイミングで切り替える必要があります。 入力 mediatype を変更する必要がある場合は、現在の入力 mediatype をそのメディアに変更する必要があります。 DTM は、デバイスの MFT の入力ストリームから現在のメディアを取得し、Devproxy の出力ストリームに設定し、各ネイティブメディアが変更された後にデバイスの MFT の入力を設定します。

### <a name="input-mediatype-change-in-device-mft"></a>デバイス MFT での入力メディアの変更

これは*m x n*の MFT であるため、出力ストリームピンの mediatypes または状態が変更された場合、入力ストリームピンの mediatypes と状態の変化に悪影響がある可能性があります。 具体的には、次の変更が発生します。

- 出力の Mediatype の変更

    - アプリケーションは、ネイティブメディアを変更すると、出力ピンの mediatype 変更として、キャプチャスタックを介してデバイス MFT にカスケードされます。

    - 出力 mediatype が変更されると、入力メディアの変更がトリガーされることがあります。 たとえば、すべての出力ピンが720p でストリーミングされているとします。 これにより、720p でカメラからストリーミングが行われます。 次に、レコードストリームのネイティブメディアが1080p に変更されるとします。 その場合、レコードストリームにデータをフェッチしていたデバイスの MFT 入力ストリームの1つで、メディアの mediatype を変更する必要があります。

- 出力ピンが無効です

    - 同じ入力が複数の出力によって共有されている場合に、アプリケーションがデバイスの MFT の出力の1つを無効にすると、その入力によって mediatype の変更が必要になることがあります。 たとえば、1080p 出力ストリームが停止し、1つの入力を共有している他のすべてのストリームが720p でストリーミングされている場合、入力ストリームによってメディアの mediatype が720p に変わり、電力が節約され、パフォーマンスが向上します。

DTM は、デバイス MFT からの[METransformInputStreamStateChanged](https://docs.microsoft.com/windows-hardware/drivers/stream/metransforminputstreamstatechanged)通知を処理して、これらの条件下でデバイス mft 入力と devproxy 出力の mediatype と状態を変更します。

### <a name="flush-device-mft"></a>デバイス MFT をフラッシュする

デバイス MFT を管理する際には、次の2種類のフラッシュが必要です。

- グローバルフラッシュ

    - デバイスの MFT 全体のフラッシュ。 これは通常、DTM が停止ストリーミングメッセージをデバイス MFT に送信しようとしているときに発生します。

    - デバイス MFT は、入力キューと出力キューからすべてのサンプルを削除し、同期的に返すことが想定されています。

    - デバイス MFT は、新しい入力を要求したり、新しい利用可能な出力に通知を送信したりすることはできません。

- ローカルフラッシュ

    - ピン固有のフラッシュを出力します。 これは通常、ストリームが停止したときに発生します。

フラッシュの前にポストされたすべてのイベントは、デバイスの MFT マネージャーによって削除されます。 フラッシュ後、デバイスの MFT は内部の[Metransformが出力](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformhaveoutput)追跡カウントをリセットします。

### <a name="drain-of-device-mft"></a>デバイス MFT のドレイン

ライブキャプチャソースにドレインを行う必要がないため、デバイス MFT は、個別のドレインメッセージを受信しません。

### <a name="photo-trigger"></a>フォトトリガー

このモデルでは、フォトトリガーとフォトシーケンスの開始と停止を直接ドライバーに送信するのではなく、デバイスの MFT に再ルーティングされます。 デバイス MFT は、トリガーを処理するか、必要に応じてカメラドライバーに転送します。

### <a name="warm-start"></a>ウォームスタート

デバイス Ource は、ストリームを一時停止状態に遷移させることによって、特定の出力ストリームをウォーム開始しようとします。 次に、DTM はデバイス MFT の[Imfdevicetransform:: SetOutputStreamState](https://docs.microsoft.com/windows/desktop/api/mftransform/nf-mftransform-imfdevicetransform-setoutputstreamstate)メソッドを呼び出して、特定の出力ストリームを一時停止状態に遷移させるようにします。 これにより、対応する入力ストリームが一時停止になります。 これは、デバイスの MFT によって実現されます。そのためには、 **METransformInputStreamStateChanged**を dtm に要求し、 [Imfdevicetransform:: SetInputStreamState](https://docs.microsoft.com/windows/desktop/api/mftransform/nf-mftransform-imfdevicetransform-setinputstreamstate)メソッドを処理します。

### <a name="variable-photo-sequence"></a>可変の写真シーケンス

このアーキテクチャでは、カメラデバイスドライバーとデバイス MFT を使用してフォトシーケンスが実装されているため、カメラデバイスドライバーの複雑さが大幅に軽減されます。 開始および停止フォトシーケンストリガーはデバイス MFT に送信され、写真シーケンスをより簡単に処理できます。

### <a name="photo-confirmation"></a>写真の確認

デバイス MFT では、 **IMFCapturePhotoConfirmation**インターフェイスを使用した写真の確認がサポートされています。 パイプラインは、 [IMFGetService:: GetService](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfgetservice-getservice)メソッドを使用してこのインターフェイスを取得します。

### <a name="metadata"></a>メタデータ

Devproxy は、ドライバーにメタデータバッファーサイズを照会し、メタデータ用のメモリを割り当てます。 ドライバーから取得されたメタデータは、サンプルの Devproxy によってまだ設定されています。 デバイス MFT は、サンプルのメタデータを使用します。 メタデータは、サンプルと共に出力ストリームから渡すか、またはポスト処理に使用することができます。

デバイス MFT で任意の数の入力をサポートしている場合は、専用の入力ピンを使用して、メタデータや帯域外のメタデータのみを使用できます。 この pin の mediatype はカスタムであり、ドライバーはバッファーのサイズと数を決定します。

このメタデータストリームは DTM 以外で公開されています。 ストリームは、デバイスの MFT がストリーミングを開始するときにストリーミング状態にすることができます。 たとえば、ストリーミング用の出力ストリームを選択すると、デバイスの MFT は、 **METransformInputStreamStateChanged**イベントを使用して、1つ以上のビデオストリームとメタデータストリームを開始するよう dtm に要求できます。 

注: このモデルでは、入力ピンの数が出力ピンの数と一致する必要はありません。 メタデータまたは3A 専用の暗証番号 (pin) のみを使用できます。

## <a name="device-transform-manager-dtm-event-handling"></a>デバイス変換マネージャー (DTM) イベント処理

[デバイス変換マネージャーのイベント](https://docs.microsoft.com/windows-hardware/drivers/stream/device-mft-events)は、次の参照トピックで定義されています。

- [METransformFlushInputStream](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformflushinputstream)
- [Metransformの出力](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformhaveoutput)
- [METransformInputStreamStateChanged](https://docs.microsoft.com/windows-hardware/drivers/stream/metransforminputstreamstatechanged)
- [Metransformの場合の入力](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformneedinput)


## <a name="imfdevicetransform-interface"></a>IMFDeviceTransform インターフェイス

[Imfdevicetransform](https://docs.microsoft.com/windows/desktop/api/mftransform/nn-mftransform-imfdevicetransform)インターフェイスは、デバイスの MFT と対話するように定義されています。 このインターフェイスにより、 *m*入力と*n*出力デバイス MFT の管理が容易になります。 デバイス MFT は、他のインターフェイスと共にこのインターフェイスを実装する必要があります。

### <a name="general-event-propagation"></a>一般的なイベントの伝達

Devproxy (またはデバイス内) でイベントが発生した場合、それをデバイスの MFT およびデバイスの Ource に伝達する必要があります。

## <a name="device-mft-requirements"></a>デバイス MFT の要件

### <a name="interface-requirements"></a>インターフェイスの要件

デバイスの MFTs は、次のインターフェイスをサポートしている必要があります。

- [IMFDeviceTransform](https://docs.microsoft.com/windows/desktop/api/mftransform/nn-mftransform-imfdevicetransform)

- [Iksk コントロール](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nn-ks-ikscontrol)

    - これにより、すべての ksk プロパティ、イベント、およびメソッドがデバイスの MFT を通過できるようになります。 これにより、デバイス mft はデバイス MFT 内でこれらの関数呼び出しを処理したり、ドライバーに転送したりすることができます。 KsEvent メソッドを処理する場合、デバイスの MFT は次の操作を行う必要があります。

        - デバイス MFT が任意の**KSEVENT_TYPE_ONESHOT**イベントを処理する場合は、 **KSEVENT_TYPE_ENABLE**を受信したときにハンドルを複製します。

        - イベントの設定または発生が完了すると、重複するハンドルで**CloseHandle**が呼び出されます。

        - デバイス MFT が非 KSEVENT_TYPE_ONESHOT イベントを処理する場合は、 **KSEVENT_TYPE_ENABLE**を受信したときにハンドルを複製し、KSEVENT 関数を使用して関数を呼び出して ks イベントが無効になったときに、重複するハンドルで**CloseHandle**を呼び出します。最初のパラメーター (ks イベント id) と2番目のパラメーター (イベントの長さ) が0に設定されています。 イベントデータと長さが有効になります。 イベントデータは、特定の ks イベントを一意に識別します。

        - デバイス MFT が非 KSEVENT_TYPE_ONESHOT イベントを処理する場合は、 **KSEVENT_TYPE_ENABLE**を受信したときにハンドルを複製する必要があります。 KSEVENT を呼び出すことで ks イベントが無効になっている場合は、重複するハンドルで**CloseHandle**を呼び出す必要があります。すべてのパラメーターが0に設定された関数。

- [IMFRealtimeClientEx](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfrealtimeclientex)

- [IMFMediaEventGenerator](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)

- [IMFShutdown](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfshutdown)

### <a name="notification-requirements"></a>通知の要件

デバイスの MFTs は、次のメッセージを使用して、サンプルの可用性、入力ストリームの状態の変更などについての情報を DTM に通知する必要があります。

- [Metransformの出力](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformhaveoutput)

- [METransformInputStreamStateChanged](https://docs.microsoft.com/windows-hardware/drivers/stream/metransforminputstreamstatechanged)

- [METransformFlushInputStream](https://docs.microsoft.com/windows-hardware/drivers/stream/metransformflushinputstream)

### <a name="thread-requirements"></a>スレッドの要件

デバイスの MFT は、独自のスレッドを作成することはできません。 代わりに、 [IMFRealtimeClientEx](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfrealtimeclientex)インターフェイスを通じて ID が渡される MF ワークキューを使用する必要があります。 これは、デバイスの MFT で実行されているすべてのスレッドが、キャプチャパイプラインが実行されている正しい優先順位を持つようにするためです。 それ以外の場合は、スレッドの優先度逆転が発生する可能性があります。

### <a name="inputstream-requirements"></a>InputStream の要件

#### <a name="stream-count"></a>ストリーム数

- デバイス MFT の入力ストリームの数は、ドライバーでサポートされているストリームの数と同じである必要があります。

#### <a name="mediatypes"></a>MediaTypes

- Mediatypes の数と、デバイスの MFT の入力でサポートされている実際のメディアの種類は、ドライバーでサポートされている mediatypes の数と種類と一致している必要があります。

- この数値は、デバイス MFT の入力でサポートされている mediatypes が、ドライバーでサポートされている mediatypes のサブセットである場合にのみ異なる可能性があります。

- ドライバーでサポートされている mediatypes とデバイス MFT の入力は、standard または custom mediatypes になります。

### <a name="to-register-device-mft"></a>デバイス MFT を登録するには

カメラデバイスの INF には、デバイスの MFT のコクラスの CLSID を指定する次のデバイスインターフェイスエントリが必要です。

```INF
[CaptureAvstrm.Device.NTarm.Interfaces]
AddInterface = %KSCATEGORY_VIDEO_CAMERA%, %Capture.FilterDescBack%, Capture.FilterBack

[Capture.FilterBack]
AddReg = Capture.FilterBack.AddReg, PinNames.AddReg

[Capture.FilterBack.AddReg]
HKR,,FriendlyName,,%Capture.FilterDescBack%
HKR,,CameraDeviceMftClsid,,%CameraDeviceMFT.Clsid%
```

上記の INF エントリによって、次のレジストリキーが入力されます。
    
**メモ**これは例です (実際のレジストリキーではありません)。

```console
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{E5323777-F976-4f5b-9B55-B94699C46E44}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{E5323777-F976-4f5b-9B55-B94699C46E44}\#GLOBAL\Device Parameters]
"CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
"FriendlyName"="USB Video Device"
"CameraDeviceMftClsid"="{3456A71B-ECD7-11D0-B908-00A0C9223196}"<<< Device MFT CoClass ID >>>
```
