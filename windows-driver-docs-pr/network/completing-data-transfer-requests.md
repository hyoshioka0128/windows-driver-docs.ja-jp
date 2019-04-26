---
title: データ転送要求の完了
description: データ転送要求の完了
ms.assetid: 4c187202-c7a8-4fd8-984a-5bae647b74b0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dad5ee2937b9810d0076ac3ab6dfca612f1e1a13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344250"
---
# <a name="completing-data-transfer-requests"></a>データ転送要求の完了





Windows ソケットは、SAN ソケットでのデータの転送を非同期的に切り替えます。 スイッチが SAN サービス プロバイダーを呼び出すたびに[ **WSPSend**](https://msdn.microsoft.com/library/windows/hardware/ff566316)、 [ **WSPRecv**](https://msdn.microsoft.com/library/windows/hardware/ff566309)、 [ **WSPRdmaWrite**](https://msdn.microsoft.com/library/windows/hardware/ff566306)、または[ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304)データ転送の関数をオーバー ラップ構造体 (WSAOVERLAPPED)へのポインターを指定します**NULL**完了ルーチンの。 スイッチは、SAN サービス プロバイダーを呼び出した場合でも[ **WSPEventSelect** ](https://msdn.microsoft.com/library/windows/hardware/ff566287)関数をソケットは非ブロッキング モードでは、SAN サービス プロバイダーが実装する必要はないことを示すために非ブロッキングこれらのデータ転送関数のセマンティクスです。

前述のように、Microsoft Windows SDK ドキュメントでは、Windows ソケット API および SPI のドキュメント、ブロッキングと非ブロッキング ソケット オーバー ラップした操作、同じ処理します。 つまり、SAN サービス プロバイダーは、特定のデータ転送操作を開始し、スイッチにすぐに制御を戻します。 これらのデータ転送関数はエラー コード WSA を返す\_IO\_を非同期操作が開始されていると、その操作の完了が後で発生することを示すために保留します。 操作の完了後、SAN サービス プロバイダーは、スイッチでは、次の段落で説明されているように、完了の通知が必要とかどうか完了を通知します。

スイッチは常に指定されているので**NULL**重複したデータ転送操作の完了のルーチン、SAN サービス プロバイダーは必要ありません非同期プロシージャ コール (Apc) を使用して補完をサポートします。

スイッチが SAN サービス プロバイダーを呼び出そうとすると、可能な限り[ **WSPGetOverlappedResult** ](https://msdn.microsoft.com/library/windows/hardware/ff566288)データ転送の要求の完了をポーリングする関数。 この方法で、スイッチがアクティブなオーバー ラップの完了メカニズムに関連するオーバーヘッドを回避できます。 SAN サービス プロバイダーに、特定の重複したデータの転送操作の完了通知は、スイッチによって必要ないことを示す、スイッチがの下位ビットを設定、 **hEvent**内のメンバー、 [ **WSAOVERLAPPED** ](https://msdn.microsoft.com/library/windows/hardware/ff565952)構造体。 SAN サービス プロバイダーは、この方法で送信された要求の完了のスイッチを通知する必要があります。

スイッチは、重複したデータの転送操作の完了の通知を必要とする場合の下位ビットは設定、 **hEvent**をゼロに WSAOVERLAPPED 構造体のメンバー。 SAN サービス プロバイダーは、この方法で呼び出すことによって開始されるデータ転送操作を完了する必要があります、 **WPUCompleteOverlappedRequest**完了を通知する関数。 この呼び出しでは、SAN サービス プロバイダーは、完成したデータの転送操作に対応する WSAOVERLAPPED 構造体へのポインターを渡します。 この**WPUCompleteOverlappedRequest**呼び出し、SAN サービス プロバイダーも渡します取得されたソケット記述子への呼び出しで、スイッチ、 **WPUCreateSocketHandle**関数。 スイッチ完了通知を受信するには、アプリケーションの I/O 要求を照合しますおよびに応じて、アプリケーション、それらの I/O 要求が完了するとします。 については、 **WPUCompleteOverlappedRequest**と**WPUCreateSocketHandle**関数は、Windows SDK のドキュメントを参照してください。

 

 





