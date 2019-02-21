---
title: 暗証番号 (pin) ファクトリ
description: 暗証番号 (pin) ファクトリ
ms.assetid: 1399b8e1-bd73-4052-afa5-3e992be8789b
keywords:
- オーディオは、WDK のオーディオ、ピン留めするファクトリをフィルター処理します。
- 暗証番号 (pin) ファクトリ WDK オーディオ
- ピン WDK のオーディオ、ファクトリ
- WDK のオーディオ、ピン留めするファクトリをフィルター処理します。
- 複数の pin ファクトリ WDK オーディオ
- WDK のオーディオ、ピン留めするファクトリのデータ形式します。
- WDK のオーディオ、ピン留めするファクトリを書式設定します。
- 複数の暗証番号 (pin) のインスタンスの WDK オーディオ
- ピン留めするファクトリを識別します。
- KSPIN_DESCRIPTOR 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa2f3cd4858e895d6b599817881210b8a8abbf20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528447"
---
# <a name="pin-factories"></a>暗証番号 (pin) ファクトリ


## <span id="pin_factories"></span><span id="PIN_FACTORIES"></span>


オーディオ フィルターの暗証番号 (pin) ファクトリでは、すべてのフィルターをインスタンス化できるピンについて説明します。 オーディオのミニポート ドライバーがの配列の暗証番号 (pin) 情報を格納する前述のように、 [ **PCPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537721)構造体。 暗証番号 (pin) ファクトリが、配列内のインデックスで識別され、各構造体は、ピン留めするファクトリを指定します。 このインデックスと呼ばれるよく、 *ID をピン留め*します。

PCPIN\_記述子構造体には、automation のテーブルが含まれています、 [ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)構造体。

KSPIN\_記述子構造体には、ピン留めするファクトリのピンに関する次の情報が含まれています。

-   データ フローの相対パスのフィルター方向

-   フィルターの相対方向の通信フローの (現在のすべての Windows バージョンでは、KS フィルター Irp 通信に使用します)。

-   ピン留めするカテゴリ

-   フレンドリ名

-   インスタンスの機能

-   データ形式の機能

構造体の**カテゴリ**と**名前**メンバーが、ピン留めするファクトリの暗証番号 (pin) のカテゴリとフレンドリ名を指定します。 各ピン留めするには、フィルターでのファクトリが、ミニポート ドライバーの組み合わせを指定**カテゴリ**と**名前**Guid があり、合わせて pin ファクトリを一意に識別します。 2 つ以上の pin ファクトリは同じを共有している場合**カテゴリ**値、各ピン ファクトリが、**名前**他と区別する値。 ピンが 1 つのファクトリがある特定の場合のみ**カテゴリ**値、値が、ピン留めするファクトリを識別するために十分であると、**名前**にピン留めするファクトリを設定できる値**NULL**. コーディングの例では、次を参照してください。[フィルター トポロジを公開する](exposing-filter-topology.md)します。 Pin のカテゴリについては、次を参照してください。 [Pin Category プロパティ](pin-category-property.md)します。

暗証番号 (pin) ファクトリでは、サポートされるデータ形式の範囲を指定の配列として拡張[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)構造体。

-   Wave または DirectSound データの範囲をサポートする、ピン留めするファクトリ形式の配列を指定する、入力または出力ストリームの[ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096)構造体。

-   MIDI の範囲または DirectMusic データをサポートする、ピン留めするファクトリ形式の配列を指定する、入力または出力ストリームの[ **KSDATARANGE\_音楽**](https://msdn.microsoft.com/library/windows/hardware/ff537097)構造体。

KSDATARANGE\_オーディオおよび KSDATARANGE\_音楽拡張 KSDATARANGE のバージョン。 両方の種類のデータ範囲の例については、次を参照してください。[オーディオ データ形式とデータ範囲](audio-data-formats-and-data-ranges.md)します。

1 つのフィルターでシンク暗証番号 (pin) を別のフィルター、グラフ ビルダーのソースのピンに接続する前に (たとえば、 [SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)) 互換性のある形式のデータ範囲を検索することができます。 グラフ ビルダーには、フィルターの[交差部分のデータ ハンドラー](data-intersection-handlers.md)、フィルター自体の互換性のある形式を選択することができます。

フィルターは、複数のピン留めするファクトリを持つことができ、pin ファクトリは、暗証番号 (pin) の複数のインスタンスをサポートできます。

-   フィルターに複数の pin ファクトリは、フィルターを通過するデータのさまざまな種類の別のデータ パスを区別するのに便利です。 たとえば、暗証番号 (pin) の 1 つのファクトリが PCM データ ストリームをサポートし、別のピン留めするファクトリ サポート ac-3 ストリーム。

-   1 つのフィルターでは、レンダリングをサポートでき、同時にストリームをキャプチャすることができます。 レンダリングとキャプチャのパスは、フィルター ファクトリの別のセットを持っています。

-   シンク pin ファクトリで頻繁に複数の暗証番号 (pin) インスタンスを持つことを意味の混在を場合、フィルターには合計ノードが含まれます ([**KSNODETYPE\_合計**](https://msdn.microsoft.com/library/windows/hardware/ff537196))。

フィルターのように、pin はカーネル オブジェクトし、カーネル ハンドルによって識別されます。 暗証番号 (pin) のインスタンスのハンドルが呼び出すことによって作成された[ **KsCreatePin**](https://msdn.microsoft.com/library/windows/hardware/ff561652)します。 カーネル オブジェクトとして IRP の対象として、暗証番号 (pin) を指定できます。 ドライバーのクライアントは、pin、IOCTL 要求を送信するときに、暗証番号 (pin) のハンドルを指定します。

作成するときに、[オーディオ フィルター グラフ](audio-filter-graphs.md)SysAudio は、自分の pin を接続することで別に 1 つのフィルターをリンクします。 1 つのフィルターからソース暗証番号 (pin) は、別のフィルターのシンクのピンに接続できます。 データと、ソースからの Irp にこの接続を介してシンク ピンのフローをピン留めします。 接続するには、グラフ ビルダー (通常は SysAudio) 最初に作成ソースの暗証番号 (pin) を呼び出して[ **KsCreatePin** ](https://msdn.microsoft.com/library/windows/hardware/ff561652)し、シンクの暗証番号 (pin) を呼び出すことによって作成**KsCreatePin**もう一度です。 2 番目の呼び出しでは、ただし、クライアントを指定します、新しい pin をシンクの最初の呼び出しで作成されたソースの暗証番号 (pin) に接続します。

 

 




