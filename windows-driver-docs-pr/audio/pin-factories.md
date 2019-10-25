---
title: ピン ファクトリ
description: ピン ファクトリ
ms.assetid: 1399b8e1-bd73-4052-afa5-3e992be8789b
keywords:
- オーディオフィルター WDK オーディオ、pin ファクトリ
- ファクトリ WDK オーディオをピン留めする
- WDK オーディオ、ファクトリをピン留めする
- WDK オーディオをフィルター処理し、ファクトリをピン留めします
- 複数の pin ファクトリ WDK オーディオ
- データ形式 WDK オーディオ、pin ファクトリ
- WDK オーディオをフォーマットし、ファクトリをピン留めします
- 複数の pin インスタンス WDK オーディオ
- pin ファクトリの識別
- KSPIN_DESCRIPTOR 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20feaed3e6607852cb2fcf8ab09fb97c374c13cd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830233"
---
# <a name="pin-factories"></a>ピン ファクトリ


## <span id="pin_factories"></span><span id="PIN_FACTORIES"></span>


オーディオフィルターのピンファクトリは、フィルターがインスタンス化できるすべてのピンを記述します。 前述のように、オーディオミニポートドライバーは、 [**pcpin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)の構造体の配列にピン情報を格納します。 各構造体は、ピンファクトリを指定し、ピンファクトリは配列内のインデックスによって識別されます。 このインデックスは、" *PIN ID*" と呼ばれることがよくあります。

PCPIN\_記述子構造体には、オートメーションテーブルと[**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造体が含まれています。

KSPIN\_記述子構造体には、ピンファクトリのピンに関する次の情報が含まれています。

-   フィルター-データフローの相対的な方向

-   フィルター-通信フローの相対的な方向 (現在のすべての Windows バージョンでは、KS フィルターは通信に Irp を使用します)。

-   カテゴリのピン留め

-   フレンドリ名

-   インスタンスの機能

-   データ形式の機能

構造の**カテゴリ**と**名前**のメンバーは、pin ファクトリの pin カテゴリとフレンドリ名を指定します。 フィルター内の各ピンファクトリについて、ミニポートドライバーは、ピンファクトリを一意に識別する**カテゴリ**と**名前**の guid の組み合わせを指定します。 2つ以上の pin ファクトリが同じ**カテゴリ**値を共有している場合、各 pin ファクトリには、他と区別するための**名前**の値があります。 1つの pin ファクトリに特定の**カテゴリ**値がある場合は、その値で pin ファクトリを識別するのに十分です。そのピンファクトリの**名前**値は**NULL**に設定できます。 コーディングの例については、「[フィルタートポロジの公開](exposing-filter-topology.md)」を参照してください。 ピン留めカテゴリの詳細については、「[ピンカテゴリのプロパティ](pin-category-property.md)」を参照してください。

Pin ファクトリは、拡張された[**Ksk datarの**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造体の配列としてサポートされるデータ形式の範囲を指定します。

-   入力ストリームまたは出力ストリームの範囲内の wave または DirectSound データ形式をサポートするピンファクトリは、 [**ksk の\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造体の配列を指定します。

-   入力ストリームまたは出力ストリームに対して MIDI または DirectMusic データ形式の範囲をサポートするピンファクトリでは、 [**ksk の\_ミュージック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)構造体の配列を指定します。

KSK datarの\_AUDIO および KSDATARANGE\_音楽は、KSK の拡張バージョンです。 両方の種類のデータ範囲の例については、「[オーディオデータ形式とデータ範囲](audio-data-formats-and-data-ranges.md)」を参照してください。

あるフィルターのシンクピンを別のフィルターのソースピンに接続する前に、グラフビルダー ( [Sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)など) がデータ範囲で互換性のある形式を検索できます。 通常、グラフビルダーは、フィルター自体が互換性のある形式を選択できるようにするために、フィルターの[データ共通部分ハンドラー](data-intersection-handlers.md)を呼び出します。

フィルターは複数の pin ファクトリを持つことができ、ピンファクトリは複数の pin インスタンスをサポートできます。

-   フィルターに複数の pin ファクトリを配置すると、フィルターを通過するさまざまな種類のデータに対して個別のデータパスを区別するのに役立ちます。 たとえば、1つの pin ファクトリで PCM データストリームがサポートされ、別の pin ファクトリが AC-3 ストリームをサポートする場合があります。

-   1つのフィルターでは、表示とキャプチャのストリームを同時にサポートできます。 レンダリングパスとキャプチャパスには、フィルターファクトリのセットが個別に含まれています。

-   シンクピンファクトリ上に複数の pin インスタンスを配置することは、多くの場合、混合を意味します。この場合、フィルターには SUM ノード ([**KSNODETYPE\_sum**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum)) が含まれます。

フィルターと同様に、ピンはカーネルオブジェクトであり、カーネルハンドルによって識別されます。 Pin インスタンスのハンドルは、 [**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)を呼び出すことによって作成されます。 カーネルオブジェクトとして、pin を IRP のターゲットとして指定できます。 ドライバーのクライアントは、暗証番号 (pin) に IOCTL 要求を送信するときに、ピンハンドルを指定します。

[オーディオフィルターグラフ](audio-filter-graphs.md)を作成するときに、sysaudio はピンを接続して1つのフィルターを別のフィルターにリンクします。 1つのフィルターのソースピンを別のフィルターのシンクピンに接続できます。 ソースピンからのデータと Irp は、この接続を介してシンクピンに送られます。 接続を確立するために、グラフビルダー (通常は SysAudio) は[**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)を呼び出してソースピンを最初に作成し、次に**KsCreatePin**を再度呼び出してシンクピンを作成します。 ただし、2回目の呼び出しでは、クライアントは、最初の呼び出しで作成されたソースピンに新しいシンク pin が接続されるように指定します。

 

 




