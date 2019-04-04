---
title: セッション プロトコルの使用
description: セッション プロトコルの使用
ms.assetid: 355286f9-ef85-4ba6-b21a-fc51e0b93fed
keywords:
- セッション プロトコル WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72aa62121eb1546eaf41390f229e387aead420c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581230"
---
# <a name="using-session-protocol"></a>セッション プロトコルの使用





Windows Sockets スイッチは、SAN 接続経由でデータを転送するのに、セッション プロトコルを使用します。 スイッチは、少量のデータを転送する場合は、コントロール メッセージ内のデータを転送します。 各コントロール メッセージは、ヘッダーと省略可能なアプリケーション データのペイロードで構成されます。 スイッチは、大量のデータを転送する場合は、rdma を使用してそのデータを転送します。

このセクションでは、設定し、データ転送を実行する方法について説明します。

**注**  スイッチ、スイッチを読み込むアプリケーションの動作、によってアプリケーション データの転送に関連するオーバーヘッドを削減するには、そのセッション プロトコルが最適化されます。

 

また、このセクションでは、スイッチのセッション プロトコルがデータ転送を実行する方法の例を示します。 ただし、これらの例では、これらの操作の明確な説明は含まれません。

### <a name="setting-up-a-data-transfer"></a>データ転送の設定

スイッチは、接続されたソケットごとのメッセージ バッファーをコントロールのプールに割り当てます。 スイッチを SAN サービス プロバイダーの呼び出しが、 [ **WSPRegisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566311)の物理メモリの領域にこれらのメッセージ バッファーを登録する関数。 スイッチは、バッファー プールの一部を使用して、SAN サービス プロバイダーの呼び出し時に、フロー制御情報をリモート ピアに送信する[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)関数。 スイッチは、プールの他の部分を使用して SAN サービス プロバイダーの呼び出し時に、リモート ピアからフロー制御情報を受信するメッセージ バッファーの投稿を[ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)関数。 スイッチは、コントロール メッセージを受信後にそれらをすぐに使用します。 コントロールのメッセージを処理した後、スイッチが SAN サービス プロバイダーを呼び出す**WSPRecv**受信リモート ピアから追加のコントロール メッセージを受信できるように再度投稿するバッファーの関数を渡します。

### <a name="transferring-application-data"></a>アプリケーション データを転送します。

データ転送のサイズは、スイッチが、データ転送操作を処理する方法に影響します。

」の説明に従って、スイッチがそのデータを転送場合は、アプリケーションは、少量のデータを送信する要求、 [SAN 上の緊急のデータを送信する](sending-urgent-data-on-a-san.md)します。

アプリケーションは、大量のデータを送信する要求している場合、スイッチは、データの最初の部分を送信するために使用するコントロール メッセージ バッファーにコピーします。 このコントロール メッセージのヘッダーには、アプリケーション データの量を指定する情報が含まれています。 スイッチを呼び出して、SAN サービス プロバイダーの[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316) SAN ソケットのリモート ピアにこのコントロール メッセージを送信します。

サービス プロバイダーがサポートするかどうかによって異なります、スイッチがアプリケーション データの転送を完了する方法、 [ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304)関数。

### <a name="data-transfer-to-a-provider-that-supports-the-wsprdmaread-function"></a>WSPRdmaRead 関数をサポートするプロバイダーへのデータ転送

次の図は、WSPRdmaRead 関数をサポートする SAN サービス プロバイダーではリモート ピアの場合に、スイッチがアプリケーション データの転送を完了する方法の概要を示します。 これに続くシーケンスより詳細なアプリケーション データの転送について説明します。

![リモート ピアが wsprdmaread をサポートしています](images/wsprdmaread.png)

### <a name="to-transfer-data-when-the-remote-peer-supports-wsprdmaread"></a>リモート ピアが WSPRdmaRead をサポートしている場合は、データを転送するには

-   -Local スイッチは、SAN サービス プロバイダーを呼び出す必要があります[ **WSPRegisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566313) RDMA メモリに対して読み取りアクセスを登録する関数。 この場合、メッセージ バッファーのコントロールのヘッダーには、アプリケーションの残りのデータを保持する RDMA メモリの記述子も特定します。
-   リモートにあるスイッチをピアリングし、呼び出し[ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304) RDMA メモリからではリモート ピアのスイッチが以前に登録されているバッファーを受信するアプリケーションのデータを転送する[**WSPRegisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566311)呼び出し。 SAN サービス プロバイダーは、バック グラウンドでは、バッファー内のデータを送信します。 これにより、別の投稿に一度に 1 つ以上の送信を投稿しないアプリケーションが SAN サービス プロバイダーがバッファー内のデータを送信中に、要求を送信します。
-   リモートにあるスイッチをピアリングし、呼び出し[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)転送が完了したことを示す-local スイッチをコントロール メッセージを送信します。
-   -Local スイッチ呼び出し、 [ **WSPDeregisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566281) RDMA のメモリを解放する関数。
-   -Local スイッチでは、アプリケーションの送信要求を完了します。 スイッチは、アプリケーションのデータ バッファー用のメモリを登録できませんまたは一時的なメモリを完全に割り当てができない場合で、アプリケーションの送信要求を完了する場合、 **WSAENOBUFS**エラー コード。

### <a name="data-transfer-to-a-provider-that-does-not-support-the-wsprdmaread-function"></a>WSPRdmaRead 関数がサポートされていないプロバイダーへのデータ転送

次の図ではリモート ピアの SAN サービス プロバイダーがサポートされていない場合に、スイッチがアプリケーション データの転送を完了する方法の概要を示しています、 [ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304)関数。 これに続くシーケンスより詳細なアプリケーション データの転送について説明します。

![リモート ピアが wsprdmaread をサポートしていません](images/wsprdmaread2.png)

### <a name="to-transfer-data-when-the-remote-peer-does-not-support-wsprdmaread"></a>リモート ピアが WSPRdmaRead をサポートしていない場合は、データを転送するには

-   リモート ピアの呼び出しにあるスイッチ[ **WSPRegisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566313) RDMA メモリに対する書き込みアクセスを登録します。
-   リモートにあるスイッチをピアリングし、呼び出し[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316) -local スイッチを記述できます RDMA メモリの場所を示す-local スイッチをコントロール メッセージを送信します。
-   -Local スイッチ呼び出し、 [ **WSPRdmaWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff566306) RDMA メモリにアプリケーション データを転送する関数。 SAN サービス プロバイダーは、バック グラウンドでは、バッファー内のデータを送信します。 これにより、別の投稿に一度に 1 つ以上の送信を投稿しないアプリケーションが SAN サービス プロバイダーがバッファー内のデータを送信中に、要求を送信します。
-   -Local スイッチ呼び出し、 [ **WSPGetOverlappedResult** ](https://msdn.microsoft.com/library/windows/hardware/ff566288)転送の結果を取得します。 詳細については、[データの転送要求の完了](completing-data-transfer-requests.md)を参照してください。
-   -Local スイッチ呼び出し[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)転送が完了したことを示すために、リモート ピアをコントロール メッセージを送信します。
-   リモート ピアの呼び出しにあるスイッチ[ **WSPDeregisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566281) RDMA のメモリを解放します。
-   -Local スイッチでは、アプリケーションの送信要求を完了します。 スイッチは、アプリケーションのデータ バッファー用のメモリを登録できませんまたは一時的なメモリの割り当てができない場合で、アプリケーションの送信要求を完了する場合、 **WSAENOBUFS**エラー コード。

## <a name="related-topics"></a>関連トピック


[SAN 上にデータを転送](transferring-data-on-a-san.md)

 

 






