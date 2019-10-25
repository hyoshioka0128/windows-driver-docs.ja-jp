---
title: バインドまたは接続リダイレクトの使用
description: バインドまたは接続リダイレクトの使用
ms.assetid: 6b27a9ad-53e9-4e80-bf03-79665f8a82a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af6a46226d2c18d024b3db3e660ddb3db6dde612
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842993"
---
# <a name="using-bind-or-connect-redirection"></a>バインドまたは接続リダイレクトの使用


Windows Filtering Platform (WFP) の接続/バインドリダイレクト機能を使用すると、アプリケーションレイヤー適用 (ALE) コールアウトドライバーは、接続を検査し、必要に応じてリダイレクトすることができます。

この機能は、Windows 7 以降で使用できます。

**  、** [WFP ドライバーサンプル](https://go.microsoft.com/fwlink/p/?LinkId=618934)の\_Proxycallouts 関数には、接続とバインドのリダイレクトを示すコードが含まれています。

 

WFP 接続リダイレクトの吹き出しは、アプリケーションが元の宛先ではなくプロキシサービスに接続するように、アプリケーションの接続要求をリダイレクトします。 プロキシサービスには2つのソケットがあります。1つはリダイレクトされた元の接続用で、もう1つは新しいプロキシ送信接続用です。

WFP リダイレクトレコードは、WFP が FWPM\_レイヤーで送信プロキシ接続に対して設定する必要がある不透明なデータのバッファーで、 **\_ALE\_AUTH\_CONNECT\_リダイレクト\_V4**と**FWPM\_レイヤー\_ALE\_AUTH\_接続\_** 、リダイレクトされた接続と元の接続が論理的に関連付けられるように、V6 レイヤーを\_リダイレクトします。

バインドリダイレクトは可能なため、接続リダイレクトでローカルアドレスとポートの変更をサポートする必要はありません。 Connect リダイレクトの一部としてローカルアドレスとポートを変更することはサポートされていません。

### <a name="layers-used-for-redirection"></a>リダイレクトに使用されるレイヤー

リダイレクトは、"リダイレクトレイヤー" と呼ばれる次のレイヤーのコールアウトドライバーによって実行できます。

-   FWPM\_レイヤー\_ALE\_バインド\_リダイレクト\_V4 (FWPS\_LAYER\_ALE\_バインド\_リダイレクト\_V4)

-   FWPM\_レイヤー\_ALE\_バインド\_リダイレクト\_V6 (FWPS\_LAYER\_ALE\_BIND\_リダイレクト\_V6)

-   FWPM\_レイヤー\_ALE\_接続\_リダイレクト\_V4 (FWPS\_LAYER\_ALE\_CONNECT\_リダイレクト\_V4)

-   FWPM\_レイヤー\_ALE\_接続\_リダイレクト\_V6 (FWPS\_LAYER\_ALE\_CONNECT\_REDIRECT\_V6)

リダイレクトが実行されるレイヤーによって、変更の影響が決まります。 接続レイヤーでの変更は、接続されているフローのみに影響します。 バインドレイヤーでの変更は、そのソケットを使用しているすべての接続に影響します。

リダイレクトレイヤーは、Windows 7 以降のバージョンの Windows でのみ使用できます。 これらのレイヤーでの分類をサポートするコールアウトドライバーは、古い[**FwpsCalloutRegister0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister0)関数ではなく、 [**FwpsCalloutRegister1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister1)以降を使用して登録する必要があります。

> [!IMPORTANT]
> のリダイレクトは、すべての種類のネットワークトラフィックで使用できるわけではありません。 次の一覧に、リダイレクトがサポートされているパケットの種類を示します。
> - TCP
> - UDP
> - ヘッダーインクルードオプションのない Raw UDPv4
> - 未加工の ICMP

### <a name="performing-redirection"></a>リダイレクトの実行

接続をリダイレクトするには、コールアウトドライバーが TCP 4 タプル情報の書き込み可能なコピーを取得し、必要に応じて変更を行い、変更を適用する必要があります。 書き込み可能なレイヤーデータを取得し、エンジンを介して適用するために、一連の新しい関数が用意されています。 コールアウトドライバーには、分類関数でインライン化するか、別[の関数で](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)非同期的に変更するオプションがあります。

リダイレクトを実装するコールアウトドライバーは、分類のコールアウト関数として[*classifyFn0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)の代わりに[*classifyFn1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn1)以降を使用する必要があります。 *ClassifyFn1*以降を使用するには、以前の[**FwpsCalloutRegister0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister0)ではなく[**FwpsCalloutRegister1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister1)以降を呼び出して、コールアウトを登録する必要があります。

インラインでリダイレクトを実行するには、コールアウトドライバーが、 [classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)の実装で次の手順を実行する必要があります。

1.  [**FwpsRedirectHandleCreate0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)を呼び出して、TCP 接続をリダイレクトするために使用できるハンドルを取得します。 このハンドルは、すべてのリダイレクトにキャッシュして使用する必要があります。 (Windows 7 およびそれ以前のバージョンでは、この手順は省略されています)。

2.  Windows 8 以降では、コールアウトドライバーの[**FwpsQueryConnectionRedirectState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0)関数を使用して、接続のリダイレクト状態を照会する必要があります。 これは、無限のリダイレクトを防ぐために行う必要があります。

3.  [**FwpsAcquireClassifyHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquireclassifyhandle0)を呼び出して、後続の関数呼び出しに使用されるハンドルを取得します。

4.  [**FwpsAcquireWritableLayerDataPointer0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquirewritablelayerdatapointer0)を呼び出して、 [classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)が呼び出されたレイヤーの書き込み可能なデータ構造体を取得します。 *Writablelayerdata* out パラメーターを、レイヤーに対応する構造体 ( [**FWPS\_BIND\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_bind_request0)または[**FWPS\_CONNECT\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)) にキャストします。

    Windows 8 以降では、コールアウトドライバーがローカルサービスにリダイレクトしている場合は、 [**FwpsRedirectHandleCreate0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)を呼び出して、 [**FWPS\_CONNECT\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)構造体の**localRedirectHandle**メンバーに入力する必要があります。ローカルのプロキシ処理を行うための順序。

5.  必要に応じてレイヤーデータに変更を加えます。

    1.  次の例に示すように、元の場所をローカルのリダイレクトコンテキストに保存します。

        ```C++
        FWPS_CONNECT_REQUEST* connectRequest = redirectContext->connectRequest;
        // Replace "..." with your own redirect context size
        connectRequest->localRedirectContextSize = ...;
        // Store original destination IP/Port information in the localRedirectContext member
        connectRequest->localRedirectContext =    ExAllocatePoolWithTag(…);
        ```

    2.  次の例に示すように、リモートアドレスを変更します。

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

    3.  コールアウトドライバーがローカルサービスにリダイレクトしている場合は、 [**Fwps\_CONNECT\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)構造体の**Localredirecttargetpid**メンバーにローカルプロキシ PID を設定する必要があります。
    4.  コールアウトドライバーがローカルサービスにリダイレクトしている場合は、FWPS\_CONNECT\_REQUEST0 構造体の**localRedirectHandle**メンバーの FwpsRedirectHandleCreate0 によって返されるリダイレクトハンドルを設定する必要があります。

6.  [**FwpsApplyModifiedLayerData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsapplymodifiedlayerdata0)を呼び出して、データに加えられた変更を適用します。

7.  プロキシサービス (ユーザーモードまたはカーネルモード) では、次の例に示すように、リダイレクトレコードとコンテキストを照会する必要があります。

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

8.  プロキシサービス (ユーザーモードまたはカーネルモードの場合もあります) では、次の例に示すように、プロキシ接続ソケットにリダイレクトレコードを設定して、新しい送信ソケットを作成する必要があります。

    ```C++
    proxySock = WSASocket(…);
    result = WSAIoctl(
                 proxySock,
                 SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS,
                 redirectRecords, …);
    ```

9.  [**FwpsReleaseClassifyHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreleaseclassifyhandle0)を呼び出して、手順2で取得した分類ハンドルを解放します。

10. [**FwpsRedirectHandleDestroy0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandledestroy0)を呼び出して、手順 1. で取得したハンドルを破棄します。

リダイレクトを非同期で実行するには、コールアウトドライバーが次の手順を実行する必要があります。

1.  [**FwpsRedirectHandleCreate0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)を呼び出して、TCP 接続をリダイレクトするために使用できるハンドルを取得します。 (Windows 7 およびそれ以前のバージョンでは、この手順は省略されています)。

2.  Windows 8 以降では、コールアウトドライバーの[**FwpsQueryConnectionRedirectState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0)関数を使用して、接続のリダイレクト状態を照会する必要があります。

3.  [**FwpsAcquireClassifyHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquireclassifyhandle0)を呼び出して、後続の関数呼び出しに使用されるハンドルを取得します。 この手順と手順 2. および 3. は、コールアウトドライバーの[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)関数で実行されます。

4.  次の例に示すように、 [**FwpsPendClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0)を呼び出して、分類を保留中の状態にします。

    ```C++
    FwpsPendClassify(
            redirectContext->classifyHandle,
            0,
            &redirectContext->classifyOut);
    classifyOut->actionType = FWP_ACTION_BLOCK;
    classifyOut->rights &= ~FWPS_RIGHT_ACTION_WRITE;
    ```

> [!NOTE]
> Windows 7 を対象としている場合は、別のワーカー関数で次の手順を実行する必要があります。 Windows 8 以降を対象としている場合は、 *classid*からの非同期リダイレクトのすべての手順を実行して、手順 5. を無視することができます。

5.  非同期処理のために、分類ハンドルと書き込み可能なレイヤーデータを別の関数に送信します。 残りの手順は、コールアウトドライバーの[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)の実装ではなく、その関数で実行されます。

6.  [**FwpsAcquireWritableLayerDataPointer0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquirewritablelayerdatapointer0)を呼び出して、 [classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)が呼び出されたレイヤーの書き込み可能なデータ構造体を取得します。 *Writablelayerdata* out パラメーターを、レイヤーに対応する構造体 ( [**FWPS\_BIND\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_bind_request0)または[**FWPS\_CONNECT\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)) にキャストします。

    Windows 8 以降では、コールアウトドライバーがローカルにリダイレクトしている場合は、 [**FwpsRedirectHandleCreate0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)を呼び出して[**FWPS\_CONNECT\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)構造体の**localRedirectHandle**メンバーに入力し、プロキシ処理。

7.  次の例に示すように、コールアウト固有のコンテキスト情報をプライベートコンテキスト構造に格納します。

    ```C++
    redirectContext->classifyHandle = classifyHandle;
    redirectContext->connectRequest = connectRequest;
    redirectContext->classifyOut = *classifyOut; // deep copy
    // store original destination IP, port
    ```

8.  必要に応じてレイヤーデータに変更を加えます。

9.  [**FwpsApplyModifiedLayerData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsapplymodifiedlayerdata0)を呼び出して、データに加えられた変更を適用します。 別のコールアウトがデータをさらに変更した場合に再承認する場合は、 **FWPS_CLASSIFY_FLAG_REAUTHORIZE_IF_MODIFIED_BY_OTHERS**フラグを設定します。

10. 次の例に示すように、 [**FwpsCompleteClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteclassify0)を呼び出して、分類操作を非同期的に完了します。

    ```C++
    FwpsCompleteClassify(
            redirectContext->classifyHandle,
            0,
            &redirectContext->classifyOut);
    classifyOut->actionType = FWP_ACTION_PERMIT;
    classifyOut->rights |= FWPS_RIGHT_ACTION_WRITE;
    ```

11. [**FwpsReleaseClassifyHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreleaseclassifyhandle0)を呼び出して、手順 1. で取得した分類ハンドルを解放します。

### <a name="handling-connect-redirection-from-multiple-callouts"></a>複数のコールアウトからの接続リダイレクトの処理

複数のコールアウトドライバーが同じフローに対して接続リダイレクトを開始する可能性があります。 接続リダイレクトを実行するコールアウトは、他の要求を認識し、適切に応答する必要があります。

コールアウトが分類を pends たびに**Fwps\_RIGHT\_ACTION\_WRITE**フラグを設定する必要があります。 コールアウトは**Fwps\_RIGHT\_action\_WRITE**フラグをテストして、コールアウトがアクションを返す権限を確認する必要があります。 このフラグが設定されていない場合でも、コールアウトは、前のコールアウトによって返された**許可操作\_許可**アクションを\_拒否するために、 **\_アクション\_ブロック**アクションを返すことができます。

Windows 8 以降では、 [**FwpsQueryConnectionRedirectState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0)関数を使用して、コールアウトドライバーが接続のリダイレクト状態を照会する必要があります (コールアウトドライバーまたは他のコールアウトドライバーによって変更されたかどうかを確認します)。 接続がコールアウトドライバーによってリダイレクトされた場合、または以前にコールアウトドライバーによってリダイレクトされた場合、コールアウトドライバーは何も実行しません。 それ以外の場合は、次の例に示すように、ローカルのリダイレクトも確認する必要があります。

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

ローカルプロキシへの接続の場合、コールアウトドライバーはリダイレクトを試行しません。

接続リダイレクトを使用するコールアウトドライバーは、ALE 承認接続層 (**Fwps\_レイヤー\_ale\_認証\_connect\_V4**または**FWPS\_layer\_ale\_AUTH\_に登録する必要があります\_V6**) に接続し、次の2つのメタデータ値を確認します。 **\_条件\_フラグ\_が\_接続\_リダイレクト**フラグが設定されていることを確認します。

-   **Fwps\_メタデータ\_フィールド\_ローカル\_リダイレクト\_ターゲット\_PID**には、リダイレクトされたフローを担当するプロセスのプロセス id が含まれています。

-   **Fwps\_メタデータ\_フィールド\_元の\_の宛先**には、フローの元の送信先のアドレスが含まれます。

[**Fwps\_CONNECT\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)構造体には、 **Localredirecttargetpid**というメンバーが含まれています。 ループバック接続のリダイレクトを有効にするには、このフィールドに、リダイレクトされたフローの役割を果たすプロセスの PID を設定する必要があります。 これは、エンジンが ALE 承認接続レイヤーで**Fwps\_メタデータ\_フィールド\_渡すデータと同じです。ローカル\_リダイレクト\_ターゲット\_ID**です。

Windows 8 以降では、プロキシサービスは[**SIO\_クエリ\_wfp\_接続**](https://docs.microsoft.com/windows-hardware/drivers/network/sio-query-wfp-connection-redirect-records)を発行する必要があります\_リダイレクト\_レコードと[**SIO\_クエリ\_wfp\_接続\_リダイレクト @no__t_13**](https://docs.microsoft.com/windows-hardware/drivers/network/sio-query-wfp-connection-redirect-context)プロキシサービスの元のエンドポイントに対して、 [**wsaioctl**](https://docs.microsoft.com/windows/desktop/api/winsock2/nf-winsock2-wsaioctl)を使用する _ コンテキスト ioctl。 また、 [**SIO\_\_WFP\_接続\_リダイレクト\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/sio-set-wfp-connection-redirect-records) 、新しい (プロキシ) ソケットで**wsaioctl**を使用して ioctl を発行する必要があります。

## <a name="related-topics"></a>関連トピック


[WFP のバージョンに依存しない名前と特定のバージョンの Windows を対象とする](https://docs.microsoft.com/windows/desktop/FWP/wfp-version-independent-names-and-targeting-specific-versions-of-windows)

 

 






