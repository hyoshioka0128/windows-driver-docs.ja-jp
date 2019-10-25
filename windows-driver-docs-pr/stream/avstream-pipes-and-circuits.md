---
title: AVStream パイプと回線
description: AVStream パイプと回線
ms.assetid: 7e4db0da-7faf-4155-ab9d-f8651db834ec
keywords:
- AVStream アロケーター WDK
- アロケーター WDK AVStream
- ユーザーモードのソース WDK AVStream
- WDK AVStream のフレーム
- 変換フィルター WDK AVStream
- パイプ WDK AVStream
- AVStream パイプ WDK
- アロケーター WDK AVStream の共有
- インプレース変換フィルター WDK AVStream
- ソースフィルター WDK AVStream
- レンダラーフィルター WDK AVStream
- 非インプレース変換フィルター WDK AVStream
- 接続 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d96576f9a23798707e9de816dea80ce69e51cdc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840620"
---
# <a name="avstream-pipes-and-circuits"></a>AVStream パイプと回線





*パイプ*は、共通の[アロケーター](avstream-allocators.md)を共有する avstream フィルターのセットです。

次の図は、3つの AVStream フィルター (ソースフィルター、*インプレース*変換フィルター、およびレンダラーフィルター) で構成されるパイプを示しています。

![すべての avstream フィルターを使用したパイプを示す図](images/pipe1.png)

この例では、 [Ksk プロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)(示されていません) は、図の**Alloc**ブロックで表されるアロケーターを選択しています。

AVStream は、ソースフィルターに関連付けられた内部要求者オブジェクトを作成します。 この図では、要求元が要求**として**表示されます。ミニドライバーは、 [**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)の**allocatorframing**メンバーで、メモリの種類とフレームに割り当てる連続メモリの量\_を指定します。 それに応じて、要求者はアロケーターからフレームを取得し、それらを回線内の次のコンポーネントに渡します。

ソースフィルターのデータは、別の AVStream ドライバーによって実装された変換フィルターにフローします。

最後に、データは3番目の AVStream フィルターによって実装されたレンダラーフィルターに送られます。

このグラフ内のすべてのピンが AVStream の pin であるため、AVStream は、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して irp を送信するのではなく、独自の内部トランスポートインターフェイスを使用して、待機時間を短縮し、パフォーマンスを向上させます。

具体的には、アプリケーションによってグラフが[**ksk\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)に遷移する場合 (たとえば、ユーザーが graphedit で **[Play]** をクリックしたとき)、avstream は、上記のようにフィルターキューに直接接続します。

したがって、ダウンストリームで送信されたフレームは、要求元に戻ります。この要求は、レンダリングの完了時に再利用できます。 この AVStream データパスは*回線*です。

次の図に示すように、変換フィルターは AVStream フィルターではなくカーネルモードフィルターである2番目の例を考えてみます。

![avstream 以外のカーネルモードの変換フィルターを使用するパイプを示す図](images/pipe2.png)

最初の例と同様に、この例には3つのフィルターが含まれています。 AVStream ソース、KS 変換 (これは、KS を直接使用するドライバーか、ストリームクラスでミニドライバーを使用するドライバーであり、AVStream レンダラー) です。

最初の図と同様に、ピンは最初に相互接続されます。 ただし、フィルターグラフが Ksk 状態に遷移すると **\_取得**しますが、カーネルストリーミング1.0 フィルターでは avstream トランスポートインターフェイスがサポートされません。 その結果、AVStream は pin をバイパスしません。代わりに、フィルター間でデータを移動するには i/o を使用する必要があります。

具体的には、フレームがソースフィルターのキューから出たときに、AVStream は[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出します。 この呼び出しでは、 *Irp*パラメーターに、ソースの出力ピンから変換フィルターに渡すフレームが格納されます。

レンダラーの入力ピンが IRP を受け取ると、pin は IRP をキューに配置します。 レンダラードライバーがフレームを完了すると、2番目の例に示すように、レンダラーの入力ピンにフレームが返されます。

AVStream は[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出し、フレームアップストリームを返します。 ソースフィルターの出力ピンは、完了通知を受け取ります。 ミニドライバーの[*ピンプロセスコールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)ルーチンは、 [**ksk ストリームポインターのロックを解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)し、フレームを要求元に戻して回線に再利用できるようにします。

フレームソースがユーザーモードである最後の例を考えてみましょう。 (または、最終的なフレームの変換先がユーザーモードである可能性があります)。

次の図では、カーネルモードの*非インプレース*変換フィルターは、ユーザーモードの DirectShow フィルターからフレームを受け取り、変換されたフレームをカーネルモード avstream レンダラーに送信します。

![ユーザーモードのソースから受信し、avstream レンダラーに送信されたフレームを示す図](images/pipe3.png)

フレームがユーザーモードから到着すると、AVStream のピンオブジェクトによって、入力パイプセクションのキューに配置されます。

非インプレース変換フィルターでは、変換されたフレームがカーネルモードで割り当てられ、2番目のパイプがこれらのフレームの回線として使用されます。 レンダラーは AVStream フィルターであるため、AVStream はピンをバイパスし、AVStream トランスポートインターフェイスを使用してフレームをレンダリングフィルターのキューに直接配置します。

ミニドライバーは、 [**KsPinSubmitFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinsubmitframe)または[**KsPinSubmitFrameMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinsubmitframemdl)を呼び出すことによって、回線に[フレームを挿入](frame-injection.md)できます。 ミニドライバーがこのメソッドを使用する場合、AVStream リクエスターは、カーネルモードアロケーターではなく、これらの呼び出しの結果としてフレームを受け取ります。

 

 




