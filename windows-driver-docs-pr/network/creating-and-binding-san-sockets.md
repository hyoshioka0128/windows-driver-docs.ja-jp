---
title: 作成して SAN のソケットをバインドします。
description: 作成して SAN のソケットをバインドします。
ms.assetid: 0589bd82-40d3-42df-926c-93093fb0617f
keywords:
- SAN 接続のセットアップ WDK、ソケットの作成とバインド
- SAN ソケット WDK San
- コンパニオン ソケット WDK San
- WDK の San を呼び出すコンパニオン ソケットの失敗
- バインドのコンパニオン ソケット
- TCP/IP ソケット WDK San
- SAN サービス プロバイダーの決定、WDK
- raw ソケット WDK San
- SAN は、WDK をソケットを作成します。
- SAN ソケット WDK、バインド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a536797eb2f860c395d5a2997f344eda8f5de4f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552376"
---
# <a name="creating-and-binding-san-sockets"></a>作成して SAN のソケットをバインドします。





Windows Sockets スイッチが、TCP/IP スタックではなく SAN 接続を介してデータをルーティングできると判断した場合は、作成、バインド、およびデータを転送できますソケットのオプションを設定する適切な SAN サービス プロバイダーを要求します。

SAN サービス プロバイダーによって作成されたソケットは、*コンパニオン*TCP/IP サービスのプロバイダーの作成からか、データを転送中に、アプリケーションの要求でソケットにします。 *コンパニオン ソケット*作成サービス プロバイダーが、SAN サービス プロバイダーの場合、TCP/IP サービス プロバイダーによって作成されたソケットは、これらのオプションをサポートしているのと同じオプションを持つ、SAN でします。

コンパニオン ソケットでは、TCP/IP サービス プロバイダーによって作成されたソケットと同じ IP アドレスと TCP ポートもあります。 SAN のデータは、TCP/IP サービス プロバイダーによって作成されたソケットではなく SAN サービス プロバイダーによって作成されたコンパニオン ソケットを介して転送されます。 SAN のソケットでは、アプリケーションに表示されません。 アプリケーションの観点から、データ転送用に作成することを要求したソケットでのデータが転送されます。

**注**  スイッチが常に TCP/IP サービス プロバイダーを使用して経由でデータを転送*raw ソケット*します。 スイッチしたがってことはありません要求 SAN サービス プロバイダー raw ソケットを作成します。

 

次の図は、コンパニオン ソケットを作成する Windows Sockets のスイッチの概要を示します。 次のセクションで、シーケンスは、さらに詳しくコンパニオン ソケットの作成について説明します。

![windows ソケットのスイッチの図の概要ガイド 』 のソケットを作成します](images/apiflow2.png)

### <a name="initiating-creation-of-a-tcpip-socket"></a>TCP/IP ソケットの作成を開始します。

1.  スイッチの受信後、Windows ソケットを**WSPSocket**呼び出しが、スイッチ、アプリケーションによって開始された呼び出し TCP/IP プロバイダーの**WSPSocket** TCP/IP プロバイダーの作成に要求する関数をソケット。

2.  Windows Sockets スイッチは、アプリケーションに作成されたソケットの記述子を返し、ソケットに関連付けられているプライベート データ構造でこの記述子を格納します。

    アプリケーションの観点からは、TCP/IP プロバイダーによって作成されたソケットは、スイッチが TCP/IP サービス プロバイダーを使用または SAN サービス プロバイダー データを転送するかどうか、データ転送のために使用するソケットをします。

### <a name="binding-a-tcpip-socket"></a>TCP/IP ソケットをバインドします。

1.  スイッチを受け取る、 **WSPBind**ワイルドカードの IP アドレス (0.0.0.0) または特定のネットワーク インターフェイス コント ローラー (NIC) には、ソケットをバインドするアプリケーションが要求した場合に呼び出します。 ワイルドカードの IP アドレスにバインドされているソケットは、すべての Nic からの受信接続要求をリッスンできます。

    **注**  以降 Windows Vista では、ワイルドカードの IP アドレス 0.0.0.0 ご利用いただけません。
    また、Windows Vista で始まる場合、 **IPAutoconfigurationEnabled**レジストリ キーが値を 0 に設定、IP アドレスの自動割り当てを無効にすると、および IP アドレスが割り当てられていません。 ここで、 **ipconfig**コマンド ライン ツールでは、IP アドレスは表示されません。 キーが 0 以外の値に設定されている場合は、IP アドレスが自動的に割り当てられます。 このキーはレジストリに次のパスにすることはできます。

    **HKEY\_ローカル\_マシン\\システム\\現在のコントロール セット\\サービス\\Tcpip\\パラメーター\\IPAutoconfigurationEnabled**

    **HKEY\_ローカル\_マシン\\システム\\現在のコントロール セット\\サービス\\Tcpip\\パラメーター\\インターフェイス\\*GUID*\\IPAutoconfigurationEnabled**

     

2.  スイッチは、TCP/IP のプロバイダーを呼び出すことによって TCP/IP サービス プロバイダーには、この呼び出しを転送**WSPBind**関数。

### <a name="service-provider-determination"></a>サービス プロバイダーの決定

1.  アプリケーションが開始した後、ソケットでのデータ転送に SAN サービス プロバイダーを使用するかどうかを決定するスイッチを**WSPListen**または**WSPConnect** 」の説明に従って、スイッチに呼び出す[SAN 接続を設定する](setting-up-a-san-connection.md)します。

2.  データ転送に SAN サービス プロバイダーを使用できないことを決定するスイッチ、スイッチは、TCP/IP サービス プロバイダー経由のデータ転送をルーティングします。

3.  スイッチが SAN サービス プロバイダーを呼び出す場合は、スイッチは、アプリケーションのソケットのサービスを提供する SAN サービス プロバイダーを選択、 [ **WSPSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566319)コンパニオン ソケットを作成する関数。

### <a name="initiating-creation-of-a-companion-socket"></a>コンパニオン ソケットの作成を開始します。

1.  SAN サービス プロバイダーの**WSPSocket**関数は、コンパニオン ソケットに関する情報が格納する内部データ構造を初期化します。

2.  SAN サービス プロバイダーの**WSPSocket**関数は次に呼び出す必要があります、 **WPUCreateSocketHandle**スイッチからソケット記述子を取得する関数。

3.  SAN サービス プロバイダーのコンパニオン ソケットの場合は、その内部データ構造でスイッチのソケット記述子を格納する必要があるし、を完了するコンパニオン ソケットの独自の記述子を返す必要があります、 **WSPSocket**呼び出します。 SAN サービス プロバイダーによって返されるソケット記述子には、プライベート データ構造体へのポインターなど、意味のある値を指定できます。

4.  ソケットでの操作を実行するには、スイッチは、SAN サービス プロバイダーによって SAN サービス プロバイダーの適切な関数に返されたソケット記述子を提供します。 同様に、SAN サービス プロバイダーは、スイッチから取得されたソケット記述子を指定する必要があります、 **WPUCreateSocketHandle** SAN サービス プロバイダーが、呼び出しを次のいずれかの場合します。

    **WPUQuerySocketHandleContext**

    **WPUCloseSocketHandle**

    **WPUCompleteOverlappedRequest**

### <a name="binding-a-companion-socket"></a>コンパニオン ソケットをバインドします。

1.  SAN サービス プロバイダーの場合、 **WSPSocket**関数が正常に完了すると、スイッチは、SAN サービス プロバイダーのすぐに呼び出し[ **WSPBind** ](https://msdn.microsoft.com/library/windows/hardware/ff566268)関数を割り当てるにはローカル IP アドレスと TCP ポート ソケットにします。

2.  スイッチは、SAN のソケット TCP/IP プロバイダーによって作成されたソケットに割り当てたのと同じ IP アドレスと TCP ポートを割り当てます。 SAN サービス プロバイダーは、ネイティブ形式にこの TCP/IP アドレスを変換する必要があります。

3.  スイッチを SAN サービス プロバイダーの完全修飾の IP アドレスと TCP ポート (つまり、0 以外の値) を提供する**WSPBind**関数のすべての Nic からの着信接続をリッスンするアプリケーションが要求されない限り、します。 SAN サービス プロバイダーのワイルドカードの IP アドレスを提供するスイッチ後のケースで**WSPBind**関数。

### <a name="setting-options-for-a-companion-socket"></a>コンパニオン ソケット オプションの設定

-   アプリケーションが、ソケット オプションを指定した場合、スイッチは、これらのオプションを格納します。 SAN のソケットを作成した後、スイッチが SAN サービス プロバイダーを呼び出す[ **WSPSetSockOpt** ](https://msdn.microsoft.com/library/windows/hardware/ff566318)をすぐにこれらのオプションを設定するアプリケーションによって指定されたサポートされている各オプションの関数SAN ソケット。

### <a name="failing-a-companion-socket-call"></a>コンパニオン ソケットの呼び出しの失敗

-   SAN サービス プロバイダーでは、前の呼び出しのいずれかが失敗した場合、 **WSPSocket**、 **WSPBind**、または**WSPSetSockOpt**関数、スイッチの呼び出し、SAN サービス プロバイダー [**WSPCloseSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566273) SAN ソケットを破棄します。 スイッチは、TCP/IP プロバイダーを使用して、アプリケーションのソケットをサービス提供を継続します。 スイッチ、SAN サービス プロバイダーを使用して接続を確立した後、スイッチできませんプロバイダーを使用して TCP/IP アプリケーションのソケットをサービスに注意してください。 この場合、スイッチは、アプリケーションに、適切なエラーを返します。

### <a name="connecting-the-companion-socket"></a>コンパニオン ソケットを接続します。

-   スイッチがいずれかを呼び出し、スイッチがコンパニオン ソケットを設定後、 **WSPListen**または**WSPConnect** SAN に SAN サービス プロバイダーの原因となった操作を実行するプロバイダーのサービスの機能当初、ソケットを設定します。 たとえば、アプリケーションが最初に要求の受信接続をリッスンするように、スイッチは SAN サービス プロバイダーを呼び出す[ **WSPListen** ](https://msdn.microsoft.com/library/windows/hardware/ff566297)関数。

 

 





