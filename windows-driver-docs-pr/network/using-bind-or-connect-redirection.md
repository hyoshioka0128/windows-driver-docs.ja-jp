---
title: バインドまたは接続リダイレクトの使用
description: バインドまたは接続リダイレクトの使用
ms.assetid: 6b27a9ad-53e9-4e80-bf03-79665f8a82a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97183ea47da2174722cac9b6316375dbb92261af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372139"
---
# <a name="using-bind-or-connect-redirection"></a>バインドまたは接続リダイレクトの使用


接続またはバインド リダイレクト機能 Windows フィルタ リング プラットフォーム (WFP) のでは、アプリケーション レイヤーの強制 (ALE) コールアウト ドライバーを検査し、必要な場合は、接続をリダイレクトできるようにします。

この機能は、以降 Windows 7 で使用できます。

**注**  、ClassifyFunctions\_ProxyCallouts.cpp モジュールで、 [WFP ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618934)接続/バインドのリダイレクトを示すコードが含まれています。

 

WFP 接続のリダイレクト コールアウトは、アプリケーションが元の送信先の代わりにプロキシ サービスに接続するために、アプリケーションの接続要求をリダイレクトします。 プロキシ サービスが 2 つのソケット: 1 つは、リダイレクトされた元の接続、新しいプロキシ送信接続のいずれか。

WFP リダイレクト レコードとは、WFP に送信プロキシ接続を設定する必要があります非透過データのバッファー、 **FWPM\_レイヤー\_ALE\_AUTH\_CONNECT\_リダイレクト\_V4**と**FWPM\_レイヤー\_ALE\_AUTH\_CONNECT\_リダイレクト\_V6**レイヤー、ようにリダイレクトされた接続元の接続を論理的に関連します。

バインドのリダイレクトは、可能であるために、接続のリダイレクトでローカル アドレスとポートの変更をサポートする必要はありません。 リダイレクトの接続の一部として、ローカル アドレスとポートを変更することはできません。

### <a name="layers-used-for-redirection"></a>レイヤーのリダイレクトに使用

リダイレクトは、「レイヤーをリダイレクト」と呼ばれる次のレイヤーでのコールアウト ドライバーを実行できます。

-   FWPM\_レイヤー\_ALE\_バインド\_リダイレクト\_V4 (FWPS\_レイヤー\_ALE\_バインド\_リダイレクト\_V4)

-   FWPM\_レイヤー\_ALE\_バインド\_リダイレクト\_V6 (FWPS\_レイヤー\_ALE\_バインド\_リダイレクト\_V6)

-   FWPM\_レイヤー\_ALE\_CONNECT\_リダイレクト\_V4 (FWPS\_レイヤー\_ALE\_CONNECT\_リダイレクト\_V4)

-   FWPM\_レイヤー\_ALE\_CONNECT\_リダイレクト\_V6 (FWPS\_レイヤー\_ALE\_CONNECT\_リダイレクト\_V6)

レイヤーのリダイレクトを実行するには、変更の結果が決定します。 接続のレイヤーでの変更では、接続されているフローのみに影響します。 変更は、ソケットを使用しているすべての接続層に影響をバインドします。

リダイレクトのレイヤーで、Windows 7 および Windows の以降のバージョンのみ利用します。 使用してこれらの層での分類をサポートするコールアウト ドライバーを登録する必要があります[ **FwpsCalloutRegister1** ](https://msdn.microsoft.com/library/windows/hardware/ff551143)またはそれ以降、いない古い[ **FwpsCalloutRegister0**](https://msdn.microsoft.com/library/windows/hardware/ff551140)関数。

> [!IMPORTANT]
> リダイレクトでは、すべての種類のネットワーク トラフィックで使用するため使用できません。 リダイレクトがサポートされているパケットの種類は、次のリストに表示されます。
> - TCP
> - UDP
> - ヘッダーなし生を通じて、UDPv4 オプションを含める
> - 生の ICMP

### <a name="performing-redirection"></a>リダイレクトを実行します。

コールアウト ドライバーが TCP 4 組の情報の書き込み可能なコピーを取得する必要がありますの接続をリダイレクトするには、必要に応じて、変更を加えるし、変更を適用します。 書き込み可能な層のデータを取得して、エンジンを適用することを一連の新しい関数が提供されます。 コールアウト ドライバーのいずれかでインラインで変更を行うオプションがあります、 [classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)関数、または別の関数に非同期的にします。

リダイレクトを実装してコールアウト ドライバーを使用する必要があります[ *classifyFn1* ](https://msdn.microsoft.com/library/windows/hardware/ff544893)以降の代わりに[ *classifyFn0* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)として分類吹き出し関数。 使用する*classifyFn1*後で、吹き出しを呼び出すことで登録する必要がありますまたは[ **FwpsCalloutRegister1** ](https://msdn.microsoft.com/library/windows/hardware/ff551143)または、後でない旧[ **FwpsCalloutRegister0**](https://msdn.microsoft.com/library/windows/hardware/ff551140)します。

インラインのリダイレクトを実行するコールアウト ドライバーは、の実装で、次の手順を実行する必要があります[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887):

1.  呼び出す[ **FwpsRedirectHandleCreate0** ](https://msdn.microsoft.com/library/windows/hardware/hh439681) TCP 接続をリダイレクトするために使用できるハンドルを取得します。 このハンドルをキャッシュして、すべてのリダイレクトに使用する必要があります。 (この手順を省略すると Windows 7 以降。)

2.  Windows 8 以降を使用して、接続のリダイレクトの状態を照会する必要があります、 [ **FwpsQueryConnectionRedirectState0** ](https://msdn.microsoft.com/library/windows/hardware/hh439677)コールアウト ドライバー関数。 これは、無限のリダイレクトを防ぐために実行する必要があります。

3.  呼び出す[ **FwpsAcquireClassifyHandle0** ](https://msdn.microsoft.com/library/windows/hardware/ff550085)後続の関数呼び出しに使用されるハンドルを取得します。

4.  呼び出す[ **FwpsAcquireWritableLayerDataPointer0** ](https://msdn.microsoft.com/library/windows/hardware/ff550087)を層の書き込み可能なデータ構造体を取得する[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)が呼び出されました。 キャスト、 *writableLayerData* out パラメーターをレイヤーに対応するか、構造体に[ **FWPS\_バインド\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551221)または[**FWPS\_CONNECT\_REQUEST0**](https://msdn.microsoft.com/library/windows/hardware/ff551231)します。

    以降、Windows 8 では、コールアウト ドライバーがローカル サービスにリダイレクトする場合、呼び出す必要がある[ **FwpsRedirectHandleCreate0** ](https://msdn.microsoft.com/library/windows/hardware/hh439681)を埋めるために、 **localRedirectHandle**メンバー、 [ **FWPS\_CONNECT\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551231)ローカル プロキシ化が機能するために構造体。

5.  必要に応じてレイヤーのデータに変更を加えます。

    1.  次の例に示すように、ローカル リダイレクトのコンテキストで元の送信先を保存します。

        ```C++
        FWPS_CONNECT_REQUEST* connectRequest = redirectContext->connectRequest;
        // Replace "..." with your own redirect context size
        connectRequest->localRedirectContextSize = ...;
        // Store original destination IP/Port information in the localRedirectContext member
        connectRequest->localRedirectContext =    ExAllocatePoolWithTag(…);
        ```

    2.  次の例に示すように、リモート アドレスを変更します。

        ```C++
        // Ensure we don't need to worry about crossing any of the TCP/IP stack's zones
        if(INETADDR_ISANY((PSOCKADDR)&(connectRequest->localAddressAndPort)))
        {
           INETADDR_SETLOOPBACK((PSOCKADDR)&(connectRequest->remoteAddressAndPort));
        }
        else
        {
           INETADDR_SET_ADDRESS((PSOCKADDR)&(connectRequest->remoteAddressAndPort),
                                 INETADDR_ADDRESS((PSOCKADDR)&(connectRequest->localAddressAndPort)));
        }
        INETADDR_SET_PORT((PSOCKADDR)&connectRequest->remoteAddressAndPort,
                          RtlUshortByteSwap(params->proxyPort));
        ```

    3.  ローカル プロキシ PID を設定する必要があります、コールアウト ドライバーがローカル サービスにリダイレクトする場合、 **localRedirectTargetPID**のメンバー、 [ **FWPS\_CONNECT\_REQUEST0**](https://msdn.microsoft.com/library/windows/hardware/ff551231)構造体。
    4.  FwpsRedirectHandleCreate0 によって返されるリダイレクト ハンドルを設定する必要があります、コールアウト ドライバーがローカル サービスにリダイレクトする、する場合、 **localRedirectHandle** 、FWPS のメンバー\_CONNECT\_REQUEST0構造体。

6.  呼び出す[ **FwpsApplyModifiedLayerData0** ](https://msdn.microsoft.com/library/windows/hardware/ff551137)データに加えられた変更を適用します。

7.  (これは、ユーザー モードまたはカーネル モードである可能性があります)、プロキシ サービス内の次の例に示すように、リダイレクト レコードとコンテキストをクエリする必要があります。

    ```C++
    BYTE* redirectRecords;
    BYTE redirectContext[CONTEXT_SIZE];
    listenSock = WSASocket(…);
    result = bind(listenSock, …);
    result = listen(listenSock, …);
    clientSock = WSAAccept(listenSock, …);
    // opaque data to be set on proxy connection
    result = WSAIoctl(clientSock,
                      SIO_QUERY_WFP_CONNECTION_REDIRECT_RECORDS,
                      redirectRecords, …);
    // callout allocated data, contains original destination information
    result = WSAIoctl(clientSock,
                      SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT,
                      redirectContext, …);
    // extract original destination IP and port from above context
    ```

8.  (これは、ユーザー モードまたはカーネル モードである可能性があります)、プロキシ サービスで新しい送信ソケットを作成する次の例に示すように、プロキシ接続のソケットにリダイレクト レコードを設定する必要があります。

    ```C++
    proxySock = WSASocket(…);
    result = WSAIoctl(
                 proxySock,
                 SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS,
                 redirectRecords, …);
    ```

9.  呼び出す[ **FwpsReleaseClassifyHandle0** ](https://msdn.microsoft.com/library/windows/hardware/ff551208)手順 2. で取得した分類のハンドルを解放します。

10. 呼び出す[ **FwpsRedirectHandleDestroy0** ](https://msdn.microsoft.com/library/windows/hardware/hh439684)手順 1. で取得されたハンドルを破棄します。

リダイレクトを非同期的に実行するには、コールアウト ドライバーは、次の手順を実行する必要があります。

1.  呼び出す[ **FwpsRedirectHandleCreate0** ](https://msdn.microsoft.com/library/windows/hardware/hh439681) TCP 接続をリダイレクトするために使用できるハンドルを取得します。 (この手順を省略すると Windows 7 以降。)

2.  Windows 8 以降を使用して、接続のリダイレクトの状態を照会する必要があります、 [ **FwpsQueryConnectionRedirectState0** ](https://msdn.microsoft.com/library/windows/hardware/hh439677)コールアウト ドライバー関数。

3.  呼び出す[ **FwpsAcquireClassifyHandle0** ](https://msdn.microsoft.com/library/windows/hardware/ff550085)後続の関数呼び出しに使用されるハンドルを取得します。 この手順と手順 2. および 3. はコールアウト ドライバーの実行[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)コールアウト関数。

4.  呼び出す[ **FwpsPendClassify0** ](https://msdn.microsoft.com/library/windows/hardware/ff551197)次の例に示すように、保留中の状態で、分類を配置します。

    ```C++
    FwpsPendClassify(
            redirectContext->classifyHandle,
            0,
            &redirectContext->classifyOut);
    classifyOut->actionType = FWP_ACTION_BLOCK;
    classifyOut->rights &= ~FWPS_RIGHT_ACTION_WRITE;
    ```

> [!NOTE]
> Windows 7 を対象とする場合は、独立した worker 関数で次の手順を実行する必要があります。 Windows 8 を対象としているか内から非同期のリダイレクトのすべての手順を実行した後で、 *classifyFn*し、手順 5 を無視します。

5.  非同期処理のための別の関数に、分類ハンドルと書き込み可能なレイヤーのデータを送信します。 コールアウト ドライバーの実装ではなく、その関数で残りの手順を実行[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)します。

6.  呼び出す[ **FwpsAcquireWritableLayerDataPointer0** ](https://msdn.microsoft.com/library/windows/hardware/ff550087)を層の書き込み可能なデータ構造体を取得する[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)が呼び出されました。 キャスト、 *writableLayerData* out パラメーターをレイヤーに対応するか、構造体に[ **FWPS\_バインド\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551221)または[**FWPS\_CONNECT\_REQUEST0**](https://msdn.microsoft.com/library/windows/hardware/ff551231)します。

    以降、Windows 8 では、コールアウト ドライバーがローカルにリダイレクトする場合、呼び出す必要がある[ **FwpsRedirectHandleCreate0** ](https://msdn.microsoft.com/library/windows/hardware/hh439681)を埋めるために、 **localRedirectHandle**のメンバー、[ **FWPS\_CONNECT\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551231)プロキシ化作業を行うために構造体。

7.  次の例に示すように、プライベート コンテキスト構造内の吹き出しに固有のコンテキスト情報を格納します。

    ```C++
    redirectContext->classifyHandle = classifyHandle;
    redirectContext->connectRequest = connectRequest;
    redirectContext->classifyOut = *classifyOut; // deep copy
    // store original destination IP, port
    ```

8.  必要に応じてレイヤーのデータを変更をします。

9.  呼び出す[ **FwpsApplyModifiedLayerData0** ](https://msdn.microsoft.com/library/windows/hardware/ff551137)データに加えられた変更を適用します。 設定、 **FWPS_CLASSIFY_FLAG_REAUTHORIZE_IF_MODIFIED_BY_OTHERS**再する別の吹き出しさらにデータを変更することを承認する場合にフラグを設定します。

10. 呼び出す[ **FwpsCompleteClassify0** ](https://msdn.microsoft.com/library/windows/hardware/ff551150)分類操作を次の例に示すように非同期的に実行します。

    ```C++
    FwpsCompleteClassify(
            redirectContext->classifyHandle,
            0,
            &redirectContext->classifyOut);
    classifyOut->actionType = FWP_ACTION_PERMIT;
    classifyOut->rights |= FWPS_RIGHT_ACTION_WRITE;
    ```

11. 呼び出す[ **FwpsReleaseClassifyHandle0** ](https://msdn.microsoft.com/library/windows/hardware/ff551208)手順 1 で取得した分類のハンドルを解放します。

### <a name="handling-connect-redirection-from-multiple-callouts"></a>処理複数のコールアウトからのリダイレクトを接続します。

1 つ以上のコールアウト ドライバーが開始されることは、同じフローのリダイレクトを接続します。 実行する吹き出しのリダイレクトを接続する他の要求に注意してくださいし、適切に応答する必要があります。

**FWPS\_右\_アクション\_書き込み**コールアウトとれたを分類するたびに、フラグを設定する必要があります。 コールアウトをテストする必要があります、 **FWPS\_右\_アクション\_書き込み**吹き出しを返すアクションの権限をチェックするフラグ。 このフラグが設定されていないかどうか、引き出し返すことができますが、 **FWP\_アクション\_ブロック**アクションを拒否するために、 **FWP\_アクション\_許可**アクションを前の引き出しによって返されました。

使用して、コールアウト ドライバーが (のかどうか、コールアウト ドライバーまたは別のコールアウト ドライバーは変更が参照してください) への接続のリダイレクトの状態を照会する必要があります Windows 8 以降では、 [ **FwpsQueryConnectionRedirectState0**](https://msdn.microsoft.com/library/windows/hardware/hh439677)関数。 コールアウト ドライバーで接続がリダイレクトされる場合、または、コールアウト ドライバーによってリダイレクトがいた場合は、コールアウト ドライバーは何を行う必要があります。 それ以外の場合、チェックするようにしても、ローカルのリダイレクトの次の例で示す。

```C++
FwpsAcquireWritableLayerDataPointer(...,(PVOID*)&connectRequest), ...);
if(connectRequest->previousVersion->modifierFilterId != filterId)
{
    if(connectRequest->previousVersion->localRedirectHandle)
    {
        classifyOut->actionType = FWP_ACTION_PERMIT;
        classifyOut->rights &= FWPS_RIGHT_ACTION_WRITE;
        FwpsApplyModifiedLayerData(
                classifyHandle,
                (PVOID)connectRequest,
                FWPS_CLASSIFY_FLAG_REAUTHORIZE_IF_MODIFIED_BY_OTHERS);
    }
}
```

ローカル プロキシに接続する場合は、コールアウト ドライバーしないでにリダイレクトします。

コールアウト ドライバーを使用する接続のリダイレクト接続レイヤーを ALE 認証に登録する必要があります (**FWPS\_レイヤー\_ALE\_AUTH\_CONNECT\_V4**または**FWPS\_レイヤー\_ALE\_AUTH\_CONNECT\_V6**) の次の 2 つのメタデータ値を確認し、場所、 **FWP\_条件\_フラグ\_IS\_接続\_REDIRECTED**フラグを設定します。

-   **FWPS\_メタデータ\_フィールド\_ローカル\_リダイレクト\_ターゲット\_PID**リダイレクトされたフローを担当するプロセスのプロセス識別子が含まれています。

-   **FWPS\_メタデータ\_フィールド\_元\_先**フローの元の送信先のアドレスが含まれています。

[ **FWPS\_CONNECT\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551231)と呼ばれるメンバーが構造に含まれる**localRedirectTargetPID**します。 任意のループバック接続のリダイレクトを有効にする、このフィールドは、リダイレクトされたフローを担当するプロセスの PID を設定する必要があります。 これは、同じデータ エンジン パス ALE 承認レイヤーとしての接続を**FWPS\_メタデータ\_フィールド\_ローカル\_リダイレクト\_ターゲット\_ID**.

プロキシ サービスは Windows 8 以降では、発行する必要があります、 [ **SIO\_クエリ\_WFP\_接続\_リダイレクト\_レコード**](https://msdn.microsoft.com/library/windows/hardware/hh802473)[ **SIO\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/hh802472)を使用して、Ioctl [**WSAIoctl**](https://msdn.microsoft.com/library/windows/desktop/ms741621)、元のプロキシ サービスのエンドポイントに対して。 さらに、 [ **SIO\_設定\_WFP\_接続\_リダイレクト\_レコード**](https://msdn.microsoft.com/library/windows/hardware/hh802474) を使用して、IOCTLを発行する必要があります**WSAIoctl**、新しい (プロキシ) のソケットでします。

## <a name="related-topics"></a>関連トピック


[WFP バージョンに依存しない名前と Windows の特定のバージョンを対象とします。](https://msdn.microsoft.com/library/windows/desktop/gg176678)

 

 






