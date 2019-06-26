---
title: 双方向通信の追加
description: 双方向通信の追加
ms.assetid: 30767eda-e456-4928-afac-40edd2ab48fc
keywords:
- 印刷スプーラの WDK、双方向通信をカスタマイズします。
- スプーラが印刷の WDK、双方向通信をカスタマイズします。
- 印刷スプーラー コンポーネント WDK、双方向通信のカスタマイズ
- 双方向通信 WDK の印刷
- 双方向通信 WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bd651baac7d484d957a22b2f16023d34010840a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370500"
---
# <a name="adding-bidirectional-communication"></a>双方向通信の追加





スプーラは、アプリケーションまたはドライバーとプリンターの間の双方向 ("BiDi") の通信をサポートします。 このサポートにより、アプリケーションまたはドライバー、プリンターとプリンターを 1 つまたは複数の要求を送信するこれらの要求に応答します。

![双方向サポートのアーキテクチャを示す図](images/bidi.png)

### <a name="bidirectional-communication-requirements"></a>双方向通信の要件

アプリケーションまたはドライバーには、双方向通信を使用できます、前に、実装する必要があります[双方向の通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index): IBidiSpl COM インターフェイスまたは少なくとも 1 つのと共に、IbidiSpl2 COM インターフェイスのいずれか、IBidiRequest および IBidiRequestContainer COM インターフェイスです。 さらに、次のいずれか要件があります。

-   [ **SendRecvBidiData** ](https://docs.microsoft.com/previous-versions/ff562068(v=vs.85))印刷プロバイダー DLL で関数を実装します。

-   [ **SendRecvBidiDataFromPort** ](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))言語モニター サーバー DLL またはポートの監視サーバー DLL で関数が実装されます。

にプリンターを 1 つの要求を送信するには、アプリケーションまたはプリンター ドライバーは最初の要求を作成し、IBidiSpl::SendRecv メソッドを呼び出して必要があります。 複数の要求を送信するには、要求の一覧を作成、アプリケーションまたはドライバーと IBidiSpl::MultiSendRecv メソッドを呼び出します。

要求を受信した後、スプーラー (Winspool.drv) のクライアント側の部分に渡します (spoolsv.exe) サーバー側のスプーラーです。 サーバー側のスプーラーには、ローカル コンピューターでは、またはリモート ネットワーク プリント サーバーを指定できます。 メソッド、要求内のデータを解析し、格納のメンバー サーバー側のスプーラーは、要求を受け取る、 [ **BIDI\_要求\_コンテナー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ns-winspool-_bidi_request_container)構造体。 サーバー側のスプーラーを呼び出して[ **SendRecvBidiData** ](https://docs.microsoft.com/previous-versions/ff562068(v=vs.85))または[ **SendRecvBidiDataFromPort**](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))します。 いずれかの関数が戻るときにその*ppResData*パラメーターが、入力内のアドレスを格納するメモリ位置を指す[ **BIDI\_応答\_コンテナー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ns-winspool-_bidi_response_container)プリンターの応答を含む構造体。 サーバー側のスプーラーはアプリケーションまたはドライバーによって使用に適したフォームにこの構造体でデータを変換します。 スプーラーにクライアント側に戻してと、最後に、要求の発信元に戻ります。

 

 




