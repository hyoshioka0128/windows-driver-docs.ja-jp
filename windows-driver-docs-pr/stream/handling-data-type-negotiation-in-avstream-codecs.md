---
title: AVStream コーデックのデータ型ネゴシエーションの処理
description: AVStream コーデックのデータ型ネゴシエーションの処理
ms.assetid: b5212429-dbc8-4e9a-b5a9-2431f8a1eb2a
keywords:
- ハードウェアコーデックサポート WDK AVStream、データ型ネゴシエーション
- データ型ネゴシエーション WDK AVStream
- AVStream ハードウェアコーデックサポート WDK、データ型ネゴシエーションの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43d6b005cd759416f24701d4e1aff8c5ec3614d3
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881930"
---
# <a name="handling-data-type-negotiation-in-avstream-codecs"></a>AVStream コーデックのデータ型ネゴシエーションの処理

デバイスが初期化されると、システム提供のデバイスプロキシ (Devproxy) モジュールによって、ドライバーによって提供されるフィルター記述子が解析されます。 さらに、Devproxy は、対応する MFT (メディアファンデーション Transform) の入力ピンと出力ピンでドライバーでサポートされているデータ範囲を公開します。

ストリーミングが開始されると、MF パイプラインとユーザーモードのアプリケーションは、これらの範囲を使用して、ドライバーとのデータ型ネゴシエーションを実行します。

データ型のネゴシエーション中に、次のような対話が行われます。

1. Devproxy は、ハードウェアコーデックフィルターの各 pin 記述子のミニドライバーによって提供されるデータ範囲を取得します。

1. Devproxy は、ドライバーに対してデータ共通部分の要求を発行します。

1. Devproxy は、完全な形式の型を MF に公開します。

1. MF トポロジビルダー (DirectShow graph ビルダーに相当する MF) は、ストリーミングトポロジを構築します。

1. MF トポロジビルダーは、Devproxy 入力/出力ピンのデータ型を終了した後、ミニドライバーの[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat) callback 関数を呼び出すことによって、ピンのデータ型を設定します。 KS pin が存在しない場合、Devproxy は[**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)を呼び出します。

データ型のネゴシエーションが正常に行われるようにするには、ミニドライバーで次の手順を実行する必要があります。

1. ハードウェアコーデックフィルターに含まれる公開された pin ごとに、 [**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)の**DataRanges**メンバーにサポートされるデータ範囲のリストを指定します。 次に、例を示します。

    ```cpp
    const PKSDATARANGE VideoDecoderInputPinDataRanges[8] = {
        (PKSDATARANGE)&H264DataFormat,
        (PKSDATARANGE)&VC_1DataFormat,
        (PKSDATARANGE)&VC_1DataFormatVIH2,
        (PKSDATARANGE)&WMV9DataFormat,
        (PKSDATARANGE)&WMV9DataFormatVIH2,
        (PKSDATARANGE)&DX50DataFormat,
        (PKSDATARANGE)&DX50DataFormatVIH2,
        (PKSDATARANGE)&MPEG2DataFormat
    };
    ```

    この場合、指定された範囲は、 [ **\_MPEG2\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_mpeg2_video)\_、 [**ks DATARANGE\_video**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)、 [**KS\_datarange\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video2)などのラッパー\_型になります。 前に示したコード例では、各範囲が型キャストになり[**ます。** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))

    ラッパー構造体の最後のメンバーは、フォーマットブロック構造体と呼ばれます。たとえば、\_は、\_MPEG2\_ビデオです。**Videoinfoheader**。

    連続データ範囲をサポートするドライバーでは、ブロック構造の形式で最大値を指定する必要があります。 不連続データ範囲をサポートするドライバーでは、ブロック構造体の形式で不連続値を格納する配列を指定する必要があります。

    指定された形式をサポートすることを要求するドライバーが、後で書式設定要求をその形式に失敗させた場合、パフォーマンスが低下する可能性があります。 サポートを保証する形式のみを一覧表示します。

1. KSK 状態\_STOP/KSSTATE\_実行されているときに、pin にメディアの種類を設定できるようにする必要があります。 ドライバーがこれを許可しないようにするために、以外の操作は必要ありません。

1. ドライバーは、 [**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)に intersect ハンドラーを指定する必要があります。各 pin の**IntersectHandler** 。

1. ミニドライバーは、 [**Ksk プロパティ\_接続\_PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-proposedataformat)プロパティのハンドラーを提供する必要があります。

1. 出力メディアの種類が設定されている場合、エンコーダーは、指定された出力メディアの種類に基づいて、使用可能な入力の種類 (pin 記述子を使用) を報告する必要があります。 出力メディアの種類が設定されていない場合、エンコーダーは入力メディアの種類を報告しません。

1. 入力メディアの種類が設定されている場合、デコーダーは、指定された入力メディアの種類に基づいて、使用可能な出力の種類を報告する必要があります。

1. 入力メディアの種類が設定されている場合、ビデオプロセッサは、指定された入力メディアの種類に基づいて出力の種類を報告する必要があります。

1. ドライバーは、 [ICodecAPI](https://docs.microsoft.com/previous-versions/ms784893(v%3Dvs.85))インターフェイスをサポートする必要があります。 ユーザーモードのコンポーネントは、このユーザーモードインターフェイスを使用して、コーデックの構成情報を取得できます。

1. エンコーダーのセットアップ中に、最初に ICodecAPI プロパティが設定され、その後に出力メディアの種類が設定されます。 この後、エンコーダーは、現在の構成でサポートできる入力型のみを提供する必要があります。

1. **ICodecAPI**のプロパティとコーデック API のメディアの種類のプロパティは、プロファイルやレベルなど、一部の領域で重複しています。 このような場合、メディアの種類に関連するコーデック API のプロパティは、ICodecAPI のプロパティよりも優先されます。 メディアの種類を設定した後、ミニドライバーは、これらの重複するプロパティを変更できないようにする必要があります。

1. デコーダーのセットアップ時に、入力の種類が最初に設定されます。 この後、デコーダーは、現在の入力の種類でサポートできる出力の種類のみを提供する必要があります。

1. エンコーダーへの予期される入力は、4:2:0、少なくとも NV12 インターレース/プログレッシブである必要があります。 予想される出力は、MPEG2 PS/TS または h.264 付属 B という形式の圧縮された基本ストリームです。

1. デコーダーへの予期される入力は、基本ストリームです。 予想される出力は、圧縮されていない NV12 のソースストリームのバージョンです。

1. AVStream ドライバーのピンは、互いに独立した状態を持つ必要があります。 これは、入力ピンが ksk 状態 **\_** から移行して、**実行\_ksk**状態に遷移し、出力ピンが ksk 状態 **\_停止**状態のままである場合に実行されることを意味します。

1. ミニドライバーが変数のデータバッファーサイズでプロパティ GET 要求を受信すると、ミニドライバーは、必要なバッファーサイズのクエリとして**NULL**バッファーを解釈する必要があります。 この場合、ドライバーは、Irp&gt;IoStatus. 情報フィールドに必要な長さを指定し、\_バッファー\_OVERFLOW の状態を返します。 また、ミニドライバーは、リターンコードをエラーではなく警告として設定する必要があります。 たとえば、次のガイダンスに従ってデータの共通部分がハンドラーになります。
