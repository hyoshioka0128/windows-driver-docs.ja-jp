---
title: AVStream コーデックのデータ型ネゴシエーションの処理
description: AVStream コーデックのデータ型ネゴシエーションの処理
ms.assetid: b5212429-dbc8-4e9a-b5a9-2431f8a1eb2a
keywords:
- ハードウェアのコーデック サポート WDK AVStream、データ型のネゴシエーション
- データの種類のネゴシエーション WDK AVStream
- AVStream ハードウェア コーデック WDK、データの種類のネゴシエーションを処理のサポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd97a63202e9d56b6d62228536be2a99a3e80da2
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419558"
---
# <a name="handling-data-type-negotiation-in-avstream-codecs"></a>AVStream コーデックのデータ型ネゴシエーションの処理

デバイスが初期化されると、システム提供のデバイス プロキシ (Devproxy) モジュールは、ドライバーによって提供されるフィルター記述子を解析します。 さらに、Devproxy は、対応する MFT (Media Foundation の変換) の入力と出力ピンのドライバーでサポートされているデータの範囲を公開します。

ストリーミングの開始時に、MF のパイプラインとユーザー モード アプリケーションは、ドライバーを使用したデータの種類のネゴシエーションを実行するのにこれらの範囲を使用します。

次の操作は、データの種類のネゴシエーション中に発生します。

1.  Devproxy では、ハードウェアのコーデック フィルターの場合は、各ピン記述子にミニドライバーによって提供されるデータの範囲を取得します。

2.  Devproxy は、ドライバーにデータの積集合要求を発行します。

3.  Devproxy MF に完全な型を公開します。

4.  MF トポロジ ビルダー (DirectShow グラフ ビルダーの MF に相当) は、ストリーミング トポロジを構築します。

5.  ミニドライバーを呼び出すことによって、暗証番号 (pin) のデータ型が設定、MF トポロジ ビルダーが Devproxy 入力/出力ピンのデータ型を終了後[ *AVStrMiniPinSetDataFormat* ](https://msdn.microsoft.com/library/windows/hardware/ff556355)コールバック関数。 Devproxy を呼び出す KS 暗証番号 (pin) が存在しない場合[ **KsCreatePin**](https://msdn.microsoft.com/library/windows/hardware/ff561652)します。

成功したデータの種類のネゴシエーションを有効にするには、ミニドライバーは以下の手順を実行する必要があります。

1.  サポートされているデータの範囲の一覧を指定、 **DataRanges**のメンバー [ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)ハードウェア コーデックのフィルターに含まれる公開されている各ピンにします。 以下に例を示します。

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

    ラッパー型で指定した範囲をここではなど[ **KS\_DATARANGE\_MPEG2\_ビデオ**](https://msdn.microsoft.com/library/windows/hardware/ff567362)、 [ **KS\_DATARANGE\_ビデオ**](https://msdn.microsoft.com/library/windows/hardware/ff567628)、および[ **KS\_DATARANGE\_VIDEO2**](https://msdn.microsoft.com/library/windows/hardware/ff567629)します。 前述のコード例で、各範囲に型キャスト[ **KSDATARANGE**](https://msdn.microsoft.com/library/windows/hardware/ff561658)します。

    ラッパーの構造体の最後のメンバーと呼ばれる形式のブロック構造体など、KS\_DATARANGE\_MPEG2\_ビデオ **。VideoInfoHeader**します。

    継続的なデータ範囲をサポートしているドライバーでは、形式のブロック構造体で最大の値を指定する必要があります。 不連続のデータ範囲をサポートするドライバーは、形式のブロック構造の不連続値を格納する配列を指定します。

    後で、特定形式のサポートを要求しているドライバーには、その形式に一連の書式設定要求が失敗した場合、パフォーマンスが低下する可能性があります。 リスト形式のみがサポートを保証します。

2.  ドライバーは KSSTATE 中に暗証番号 (pin) に設定するメディアの種類を許可する必要があります\_停止/KSSTATE\_を実行します。 アクションは必要ありませんは、ここ以外のこと、ドライバーは拒否する場合これを確認します。

3.  ドライバーに intersect ハンドラーを指定する必要があります[ **KSPIN\_記述子\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534).**IntersectHandler**各ピンにします。

4.  ミニドライバーのハンドラーを指定する必要があります、 [ **KSPROPERTY\_接続\_PROPOSEDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff565107)プロパティ。

5.  出力メディアの種類を設定すると、エンコーダーがメディアの種類の指定された出力に基づいて (暗証番号 (pin) の記述子を使用) して可能な入力の種類を報告する必要があります。 出力メディアの種類が設定されていない場合エンコーダーは任意の入力メディアの種類を報告する必要があります。

6.  入力メディアの種類が設定されている場合、デコーダーは、指定された入力メディアの種類に基づく使用可能な出力の種類を報告する必要があります。

7.  入力メディアの種類が設定されている場合、ビデオ プロセッサは、指定された入力メディアの種類に基づいて、出力の種類を報告する必要があります。

8.  ドライバーをサポートする必要があります、 [ICodecAPI](https://docs.microsoft.com/en-us/previous-versions/ms784893(v%3Dvs.85))インターフェイス。 ユーザー モード コンポーネントは、このユーザー モード インターフェイスを使用してコーデック構成情報を取得できます。

9.  エンコーダーのセットアップ中に最初に、ICodecAPI プロパティを設定後に、出力メディアの種類。 次に、エンコーダーは入力の種類でサポートできるを現在の構成でのみ提供する必要があります。

10. **ICodecAPI**プロパティとコーデックの API のメディアのプロファイルとレベルなど、一部の地域でプロパティの重複を入力します。 このような場合は、メディアの種類に関連付けられているコーデック API プロパティは、ICodecAPI プロパティをオーバーライドします。 メディアの種類を設定すると後、ミニドライバーはプロパティが重複しているこれらの変更を許可しないでください。

11. デコーダーのセットアップ中に、入力の型が最初に設定します。 次に、デコーダーはのみ出力の種類でサポートできると、現在の入力型を提供する必要があります。

12. エンコーダーに入力する必要がある 4 にする必要があります: 2:0 と、少なくとも NV12 インター レース/プログレッシブします。 予想される出力は MPEG2 PS の形式で圧縮された基本ストリーム/TS または H.264 Annex B

13. デコーダーに想定される入力は、基本ストリームです。 予想される出力は、圧縮されていない NV12 としてソース ストリームのスケールなしバージョンです。

14. AVStream ドライバーでピンは互いに依存しない状態が必要です。 つまり、入力ピンがからに移行できます、 **KSSTATE\_停止**まで、 **KSSTATE\_実行**で出力ピン留めしたまま、 **KSSTATE\_停止**状態。

15. ミニドライバーを解釈する必要があります、ミニドライバーは、変数のデータ バッファーのサイズとプロパティの GET 要求を受信すると、 **NULL**としてクエリに必要なバッファーのサイズのバッファー。 ここでは、ドライバーは Irp の必要な長さを指定する必要があります&gt;IoStatus.Information フィールドと状態の戻り値\_バッファー\_オーバーフローが発生します。 さらに、ミニドライバーは、警告とエラーではなく、リターン コードを設定する必要があります。 たとえば、データの積集合のハンドラーを使用して、このガイダンスに従ってください。
