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
ms.openlocfilehash: d750f24c78370ecc83d2401dbc2d57d0db034b34
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343166"
---
# <a name="adding-bidirectional-communication"></a>双方向通信の追加





スプーラは、アプリケーションまたはドライバーとプリンターの間の双方向 ("BiDi") の通信をサポートします。 このサポートにより、アプリケーションまたはドライバー、プリンターとプリンターを 1 つまたは複数の要求を送信するこれらの要求に応答します。

![双方向サポートのアーキテクチャを示す図](images/bidi.png)

### <a name="bidirectional-communication-requirements"></a>双方向通信の要件

アプリケーションまたはドライバーには、双方向通信を使用できます、前に、実装する必要があります[双方向の通信インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545163): IBidiSpl COM インターフェイスまたは少なくとも 1 つのと共に、IbidiSpl2 COM インターフェイスのいずれか、IBidiRequest および IBidiRequestContainer COM インターフェイスです。 さらに、次のいずれか要件があります。

-   [ **SendRecvBidiData** ](https://msdn.microsoft.com/library/windows/hardware/ff562068)印刷プロバイダー DLL で関数を実装します。

-   [ **SendRecvBidiDataFromPort** ](https://msdn.microsoft.com/library/windows/hardware/ff562071)言語モニター サーバー DLL またはポートの監視サーバー DLL で関数が実装されます。

にプリンターを 1 つの要求を送信するには、アプリケーションまたはプリンター ドライバーは最初の要求を作成し、IBidiSpl::SendRecv メソッドを呼び出して必要があります。 複数の要求を送信するには、要求の一覧を作成、アプリケーションまたはドライバーと IBidiSpl::MultiSendRecv メソッドを呼び出します。

要求を受信した後、スプーラー (Winspool.drv) のクライアント側の部分に渡します (spoolsv.exe) サーバー側のスプーラーです。 サーバー側のスプーラーには、ローカル コンピューターでは、またはリモート ネットワーク プリント サーバーを指定できます。 メソッド、要求内のデータを解析し、格納のメンバー サーバー側のスプーラーは、要求を受け取る、 [ **BIDI\_要求\_コンテナー** ](https://msdn.microsoft.com/library/windows/hardware/ff545193)構造体。 サーバー側のスプーラーを呼び出して[ **SendRecvBidiData** ](https://msdn.microsoft.com/library/windows/hardware/ff562068)または[ **SendRecvBidiDataFromPort**](https://msdn.microsoft.com/library/windows/hardware/ff562071)します。 いずれかの関数が戻るときにその*ppResData*パラメーターが、入力内のアドレスを格納するメモリ位置を指す[ **BIDI\_応答\_コンテナー**](https://msdn.microsoft.com/library/windows/hardware/ff545202)プリンターの応答を含む構造体。 サーバー側のスプーラーはアプリケーションまたはドライバーによって使用に適したフォームにこの構造体でデータを変換します。 スプーラーにクライアント側に戻してと、最後に、要求の発信元に戻ります。

 

 




