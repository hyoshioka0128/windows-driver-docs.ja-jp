---
title: AVStream のパイプと回路
description: AVStream のパイプと回路
ms.assetid: 7e4db0da-7faf-4155-ab9d-f8651db834ec
keywords:
- AVStream allocators WDK
- アロケーター WDK AVStream
- ユーザー モード WDK AVStream をソースします。
- WDK AVStream フレーム
- WDK AVStream のフィルターを変換します。
- パイプを使用して WDK AVStream
- AVStream パイプ WDK
- アロケーター WDK AVStream の共有
- インプレース変換を使用して WDK AVStream
- ソース フィルター WDK AVStream
- レンダラーが WDK AVStream をフィルター処理します。
- 非インプレース変換を使用して WDK AVStream
- WDK AVStream の回路
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 195d552a0c888a9dbf8faa0e61fd25da45c8e2e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384818"
---
# <a name="avstream-pipes-and-circuits"></a>AVStream のパイプと回路





A*パイプ*は一連の共通 AVStream フィルター[アロケーター](avstream-allocators.md)します。

次の図は、パイプから成る AVStream の 3 つのフィルター: ソース フィルター、*インプレース*フィルター、およびレンダラーのフィルターを変換します。

![avstream のすべてのフィルターを使用してパイプを示す図](images/pipe1.png)

この例で[KSProxy](https://msdn.microsoft.com/library/windows/hardware/ff560877) (非表示) で表される、アロケーターは、選択した、**アロケーション**の図は、ブロックします。

AVStream は、ソース フィルターに関連付けられた内部の要求元オブジェクトを作成します。 図では、依頼者として表示されます。 **Req**します。ミニドライバーを指定します、 **AllocatorFraming**のメンバー [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)メモリとの継続的な量の種類フレームに割り当てるメモリ。 それに応じて、依頼者は、アロケーターからフレームを取得および回路の次のコンポーネントに渡します。

ソース フィルターからのデータは、別の AVStream ドライバーによって実装される変換のフィルターに渡されます。

最後に、データは、サードパーティ AVStream フィルターによって実装されているレンダラーのフィルターに渡されます。

AVStream で独自のトランスポートの内部インターフェイスを使用して、Irp を送信する代わりに AVStream ピンをすべてのこのグラフのピンは[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)待ち時間の短縮とパフォーマンスの向上.

具体的には、アプリケーションがグラフへの移行を原因と[ **KSSTATE\_ACQUIRE** ](https://msdn.microsoft.com/library/windows/hardware/ff566856) (ユーザーがクリックすると、**再生**GraphEdit で)、直接 AVStream は、上記のように、キューにフィルターを接続します。

そのため、ダウン ストリームに送信されたフレームを返す、要求元にできます再利用されるレンダリングが完了するとします。 この AVStream データ パスは、*回線*します。

次の図で、変換、フィルターは AVStream フィルターでは、なくカーネル モードのフィルターが示すように、2 番目の例を検討してください。

![非 avstream カーネル モードの変換のフィルターを使用してパイプを示す図](images/pipe2.png)

最初の例では、この例では 3 つのフィルター: AVStream ソースを (これは KS を直接使用するドライバーまたはストリーム クラスの下のミニドライバー) KS 変換、および、AVStream レンダラーです。

最初の図のように、pin が最初に相互接続します。 フィルターのグラフに遷移するときに**KSSTATE\_ACQUIRE**、ただし、カーネル ストリーミング 1.0 フィルターが AVStream 転送インターフェイスをサポートしません。 その結果、AVStream が; ピンをバイパスしません。代わりに、I/O を使用して、フィルターの間でデータを移動するがあります。

具体的には、フレームを離れると、ソース フィルターのキュー、AVStream 呼び出し[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。 この呼び出しで、 *Irp*パラメーターには、ソースの出力ピンから変換フィルターに渡すフレームが含まれています。

レンダラーの入力ピンは IRP を受信すると、pin は IRP をキューに配置します。 レンダラーのドライバーには、フレームが完了すると、そのフレームを返します、レンダラーの入力ピンに 2 番目の例で示すように。

AVStream 呼び出し[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)をアップ ストリームにフレームを返します。 ソース フィルターの出力ピンは、完了通知を受信します。 ミニドライバーの[*暗証番号 (pin) プロセスのコールバック*](https://msdn.microsoft.com/library/windows/hardware/ff556351)ルーチンを呼び出して[ **KsStreamPointerUnlock** ](https://msdn.microsoft.com/library/windows/hardware/ff567137)フレームを要求元に戻す回線を再利用します。

フレームのソースがユーザー モードでの最後の例を検討してください。 (または、フレームの最終的な宛先できますユーザー モードでします。)

カーネル モードを次の図の*非-force-inplace*変換フィルターがユーザー モード DirectShow フィルターからフレームを受信し、カーネル モードの AVStream レンダラーに変換されたフレームを送信。

![ユーザー モードのソースから受け取るし、avstream レンダラーに送信されたフレームを示す図](images/pipe3.png)

フレームがユーザー モードから届いたら、AVStream 暗証番号 (pin) のオブジェクトはそれらを入力パイプでのキューに配置します。

非-force-inplace 変換フィルターでは、カーネル モードで変換されたフレームを割り当て、回線としてこれらのフレームの 2 つ目のパイプを使用し、します。 レンダラーが、AVStream フィルターであるため、AVStream はピンをバイパスし、AVStream 転送インターフェイスを使用して表示フィルターのキューで直接、フレームを配置しています。

ミニドライバーは[フレームを挿入](frame-injection.md)呼び出すことで、回線に[ **KsPinSubmitFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff563529)または[ **KsPinSubmitFrameMdl**](https://msdn.microsoft.com/library/windows/hardware/ff563530). ミニドライバーは、このメソッドを使用して、AVStream 依頼者はカーネル モード アロケーターからではなく、これらの呼び出しの結果として、フレームを受け取ります。

 

 




