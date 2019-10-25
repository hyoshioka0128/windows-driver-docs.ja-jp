---
title: AVStream スプリッター
description: AVStream スプリッター
ms.assetid: c2cfc183-0f4c-4104-a580-234e0483eee4
keywords:
- スプリッターの WDK AVStream
- AVStream スプリッター (WDK)
- データストリームの分割 WDK AVStream
- KSPIN_FLAG_SPLITTER
- WDK AVStream の自動分割
- 入力ピン分割 WDK AVStream
- 出力ピンスプリッター処理 WDK AVStream
- 固定の WDK AVStream の分割
- プロセス pin WDK AVStream
- WDK AVStream のフレーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4bab8ff64453ff32a6b72abb075496008264889
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840623"
---
# <a name="avstream-splitters"></a>AVStream スプリッター





AVStream ミニドライバーは、AVStream クラスドライバー機能を使用して、ストリームが特定の pin を通過するときにデータストリームを複数のコピーに分割することができます。 この分割プロセスは、ドライバーが2つの同じ出力ストリームを生成するために入力ストリームをコピーする必要がある場合に便利です。

これを行うには、ピンの[**kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**FLAGS**メンバーに kspin\_フラグ\_スプリッターを設定します。 Pin にこのフラグが設定されている場合、pin は自動スプリッターとして機能します。 AVStream は、ストリームを分割するために必要なすべてのデータを自動的にコピーします。

DirectX 8.0 より後のリリースでは、[フィルター中心](filter-centric-processing.md)のフィルターと[ピン中心](pin-centric-processing.md)のフィルターの両方で、kspin\_フラグ\_スプリッターフラグがピンに対して機能します。 以前のリリースでは、フィルター中心のフィルターのピンに対してのみこのフラグがサポートされています。

次の図は、入力ピンによってストリームが2つの出力ピンに分割されるフィルターの構成を示しています。 この出力ピンの下流フィルターは、データの*インプレース*を変更します。

![スプリッター出力ピンを持つ avstream フィルターを示す図 ](images/split1.png)

フレームは入力ピンに到達し、入力キューに格納されます。 ミニドライバーは、元の pin の入力キューと出力キューのみと対話します。 AVStream は、最初のピンのキューから2番目のピンのキューにデータを自動的にコピーします。

わかりやすくするために、この図は、出力ピンにフレームがどのように提供されるかを示していません。 たとえば、出力ピンにフレームを提供するには、要求元と、各キューに関連付けられ、このパイプセクションに属するアロケーターが必要になることがあります。 また、フレームを下流フィルターから取得することもできます。

ミニドライバーは、 [ **\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)構造体で、ベンダが提供した[*Avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)コールバックルーチンへのポインターを指定します。 このコールバックルーチンは、次に示す[**Ksk Processpin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin)構造体の配列を含む[**ksk PROCESSPIN\_indexentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin_indexentry)構造体へのポインターを受け取る場所です。

この図は、ミニドライバーが、プロセスピンリスト内の2つの出力ピンを区別する方法を示しています。

![2つの分割ピンのプロセスピンテーブルの図](images/splitppin1.png)

この図では、DB が[**Ksk Processpin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin)構造体の**DelegateBranch**メンバーを参照し、CS は**copysource**メンバーを参照しています。 入力ピンの**DelegateBranch**および**copysource**メンバーと最初の出力ピンの両方が**NULL**です。 これは、ミニドライバーがこれらのピンのフレームを処理することを示します。

ただし、2番目の出力ピンには、最初の出力ピンを指す**Copysource**があります。 これは、2番目の出力ピンが最初の出力ピンとは別のパイプにあることを示し、AVStream は、最初の出力ピンのキューに格納されているすべてのデータを2番目の出力ピンのキューに自動的にコピーします。

2つの出力ピンが同じパイプに組み込まれていると、より複雑なスプリッターケースが発生する可能性があります。 ミニドライバーには、同じパイプに2つのスプリッターベースの出力ピンを含めることができます。たとえば、ダウンストリームフィルターによって、これらのピンから送信されるデータが変更されない限りです。 データは変更されないため、出力ピンは読み取り専用と見なされます。どちらのダウンストリームフィルターも、同じバッファーを受け取ります。

スプリッターピンに自動的にアタッチされるダウンストリームフィルターの中には、データが変更されないものもあります。

この場合、フィルターレイアウトは次の図のようになります。これは、分割出力ピンの3つのインスタンスを含むフィルターを示しています。

![3つの分割された出力ピンを持つ avstream フィルターを示す図 ](images/split2.png)

ダウンストリームフィルターによってデータが変更されないため、ピン A と B は同じパイプに割り当てられます。A および B の下流のフィルターは、同じバッファーポインターを受け取ります。

*ミニドライバーは、入力キューと1つの出力キューだけを操作します。* AVStream は A/B キューと C キューから自動的にコピーします。 また、ピン A とピン B を使用して同じデータフレームを送信する splitter オブジェクトも作成します (ストリームヘッダーが異なることに注意してください)。

[**Ksprocesspin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin)構造体の配列は次のとおりです。

![3つの分割出力ピンのプロセスピンテーブルの図](images/splitppin2.png)

通常の状況下でミニドライバーが操作する必要があるピンは、ピン A だけです。

上の図を簡略化するために、要求者とアロケーターは図から除外されました。 図は、フレーム分割プロセスのみを示すことを目的としています。

 

 




