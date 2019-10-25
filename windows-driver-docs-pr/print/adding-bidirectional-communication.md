---
title: 双方向通信の追加
description: 双方向通信の追加
ms.assetid: 30767eda-e456-4928-afac-40edd2ab48fc
keywords:
- 印刷スプーラ WDK、双方向通信のカスタマイズ
- スプーラ WDK の印刷、双方向通信のカスタマイズ
- 印刷スプーラコンポーネントのカスタマイズ (WDK)、双方向通信
- 双方向通信の WDK 印刷
- bidi 通信 WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2a130eaf4fc665f390cfb90b9f9af2b0b31572d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824777"
---
# <a name="adding-bidirectional-communication"></a>双方向通信の追加





スプーラでは、アプリケーションまたはドライバーとプリンターの間の双方向 ("BiDi") 通信がサポートされています。 このサポートにより、アプリケーションまたはドライバーはプリンターに1つ以上の要求を送信し、プリンターはこれらの要求に応答できるようになります。

![双方向サポートアーキテクチャを示す図](images/bidi.png)

### <a name="bidirectional-communication-requirements"></a>双方向通信の要件

アプリケーションまたはドライバーが bidi 通信を使用できるようにするには、[双方向通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)を実装する必要があります。これには、IBidiSpl com インターフェイスまたは IbidiSpl2 com インターフェイスのいずれかと、少なくとも1つの IBidiRequest とIBidiRequestContainer COM インターフェイス。 また、次のいずれかまたは両方が true である必要があります。

-   [**SendRecvBidiData**](https://docs.microsoft.com/previous-versions/ff562068(v=vs.85))関数は、印刷プロバイダーの DLL に実装されています。

-   [**SendRecvBidiDataFromPort**](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))関数は、言語モニターサーバー dll またはポートモニターサーバー dll に実装されています。

プリンターに1つの要求を送信するには、まず、アプリケーションまたはプリンタードライバーが要求を作成してから、IBidiSpl:: SendRecv メソッドを呼び出します。 複数の要求を送信するために、アプリケーションまたはドライバーは要求のリストを結合し、IBidiSpl:: MultiSendRecv メソッドを呼び出します。

要求を受信すると、スプーラ (Winspool. drv) のクライアント側の部分で、サーバー側のスプーラ (spoolsv.exe) に渡されます。 サーバー側スプーラは、ローカルコンピュータ上、またはリモートネットワークプリントサーバー上に配置できます。 サーバー側のスプーラが要求を受信すると、要求内のデータを解析し、 [**BIDI\_要求\_コンテナー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ns-winspool-_bidi_request_container)構造体のメンバーに入力します。 次に、サーバー側スプーラは[**SendRecvBidiData**](https://docs.microsoft.com/previous-versions/ff562068(v=vs.85))または[**SendRecvBidiDataFromPort**](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))を呼び出します。 どちらの関数からが返された場合、その*Ppresdata*パラメーターは、プリンターの応答を格納する、入力された[**BIDI\_応答\_コンテナー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/ns-winspool-_bidi_response_container)構造体のアドレスを格納しているメモリ位置を指します。 サーバー側のスプーラは、この構造のデータを、アプリケーションまたはドライバーでの使用に適した形式に変換し、クライアント側のスプーラに渡し、最後に要求の発信元に戻します。

 

 




