---
title: SAN のソケット オプションと制御コードの処理
description: SAN のソケット オプションと制御コードの処理
ms.assetid: 5c07d0e3-b6d7-4daf-8b3f-80aafd7c7a37
keywords:
- Windows ソケットの直接の WDK SAN ソケット オプション
- SAN ソケット WDK、オプション
- 取得する SAN ソケット オプション
- SAN サービス プロバイダー、WDK のステータス情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad1c3ab12f6229eb16637e4e770484feae08f8d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322282"
---
# <a name="handling-socket-options-and-control-codes-for-a-san"></a>SAN のソケット オプションと制御コードの処理





TCP/IP プロバイダーと組み合わせて、Windows Sockets スイッチを最も処理**WSPGetSockOpt**、 **WSPSetSockOpt**、および**WSPIoctl**アプリケーションによって開始された呼び出し。 これらの要求は、通常、設定およびオプションと、アプリケーションのソケットに関連付けられた操作パラメーターを取得します。 スイッチでは、SAN サービス プロバイダーを除くの説明に従って、次のセクションでこれらの呼び出しは一般に転送しません。

### <a name="retrieving-san-socket-options"></a>取得する SAN ソケット オプション

Windows Sockets スイッチ呼び出し SAN サービス プロバイダーの[ **WSPGetSockOpt** ](https://msdn.microsoft.com/library/windows/hardware/ff566292)関数し、する場合は、そのオプションの現在の値を取得する次のソケット オプションのいずれかを渡す SAN サービスプロバイダーには、そのオプションがサポートされています。

<a href="" id="so-debug"></a>したがって\_デバッグ  
SAN サービス プロバイダーは、このオプションをサポートする必要はありません。 このことをお勧めするですが、アプリケーションの設定、その場合、出力デバッグ情報を指定する必要ありません\_デバッグ オプション。

<a href="" id="so-max-msg-size"></a>したがって\_最大\_MSG\_サイズ  
基になる SAN 転送では、メッセージ指向し、トランスポート スイッチは、SAN サービス プロバイダーの呼び出しで送信できるデータの量を制限する場合、SAN サービス プロバイダーはこのオプションをサポートする必要があります[ **WSPSend**](https://msdn.microsoft.com/library/windows/hardware/ff566316)関数。 スイッチでは、送信要求は、その後は、SAN サービス プロバイダーは、このオプションの値を返しますのサイズを超過する SAN サービス プロバイダーに渡されません。

<a href="" id="so-max-rdma-size"></a>したがって\_最大\_RDMA\_サイズ  
基になる SAN 転送でスイッチを転送できるデータの量を呼び出すいずれかに制限 SAN サービス プロバイダーの場合、SAN サービス プロバイダーはこのオプションをサポートする必要があります[ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304)または[**WSPRdmaWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff566306)関数。 スイッチは、その後 RDMA 転送要求に渡さない SAN サービス プロバイダーは、このオプションの値を返しますのサイズを超過する SAN サービス プロバイダー。

<a href="" id="so-rdma-threshold-size"></a>したがって\_RDMA\_しきい値\_サイズ  
SAN サービス プロバイダーのいずれか、SAN サービス プロバイダーの呼び出しで、スイッチを転送できるデータ量の最小の優先順位を指定するには、このオプションをサポートしている**WSPRdmaRead**または**WSPRdmaWrite**関数。 ただし、スイッチ、実際のしきい値値に設定できます、SAN サービス プロバイダーによって返される値と異なります。 スイッチが、その後に呼び出し、 **WSPRdmaRead**または**WSPRdmaWrite**関数がこのしきい値のサイズを超えるデータ ブロック (RDMA 転送) を転送して、 **WSPSend**または**WSPRecv**このしきい値のサイズより小さいか等しいデータ ブロック (メッセージ指向の転送) を転送する関数。

<a href="" id="so-group-id--so-group-priority"></a>したがって\_グループ\_ID、したがって\_グループ\_優先順位  
SAN サービス プロバイダーは、サービスの品質 (QoS) をサポートしている場合、これらのオプションをサポートする必要があります。 それ以外の場合、スイッチは、これらのオプションを既定値を保持する TCP/IP プロバイダーに転送します。 SAN サービス プロバイダーは、XP1 を設定して、QoS をサポートしていることを示します\_QOS\_でサポートされているビット、 **dwServiceFlags** 、WSAPROTOCOL のメンバー\_情報構造体。

### <a name="setting-san-socket-options"></a>SAN のソケット オプションの設定

Windows Sockets スイッチ呼び出し SAN サービス プロバイダーの[ **WSPSetSockOpt** ](https://msdn.microsoft.com/library/windows/hardware/ff566318)関数を SAN サービス プロバイダーをサポートしている場合、そのオプションの値を設定するのには、次のソケット オプションのいずれかを渡しますオプション:

<a href="" id="so-debug"></a>したがって\_デバッグ  
このソケット オプションの説明は、上記の一覧を参照してください。

<a href="" id="so-group-priority"></a>したがって\_グループ\_優先順位  
このソケット オプションの説明は、上記の一覧を参照してください。

### <a name="accessing-san-socket-information"></a>SAN へのアクセス情報をソケットします。

Windows Sockets スイッチ呼び出し SAN サービス プロバイダーの[ **WSPIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff566296)関数およびパスの場合、その SAN サービス プロバイダーの情報を取得または設定するコード、次のコントロールのいずれか、SANサービス プロバイダーには、そのコントロールのコードがサポートされています。

<a href="" id="sio-get-extension-function-pointer"></a>SIO\_取得\_拡張子\_関数\_ポインター  
SAN サービス プロバイダーがサポートする拡張関数へのポインターを取得します。 拡張関数の詳細については、次を参照してください。 [Windows Sockets SPI Extensions for San](windows-sockets-spi-extensions-for-sans.md)します。 入力バッファー、 **WSPIoctl**呼び出しには、値を持つ、指定された拡張子関数を識別する GUID が含まれています。 SAN サービス プロバイダーが要求された関数のポインターを返します**WSPIoctl**のバッファーを出力します。 次の表には、SAN サービス プロバイダーをサポートする拡張関数の Guid が含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">拡張関数</th>
<th align="left">GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566311" data-raw-source="[&lt;strong&gt;WSPRegisterMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566311)"><strong>WSPRegisterMemory</strong></a></p></td>
<td align="left"><p>{C0B422F5-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566279" data-raw-source="[&lt;strong&gt;WSPDeregisterMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566279)"><strong>WSPDeregisterMemory</strong></a></p></td>
<td align="left"><p>{C0B422F6-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566313" data-raw-source="[&lt;strong&gt;WSPRegisterRdmaMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566313)"><strong>WSPRegisterRdmaMemory</strong></a></p></td>
<td align="left"><p>{C0B422F7-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566281" data-raw-source="[&lt;strong&gt;WSPDeregisterRdmaMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566281)"><strong>WSPDeregisterRdmaMemory</strong></a></p></td>
<td align="left"><p>{C0B422F8-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566306" data-raw-source="[&lt;strong&gt;WSPRdmaWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566306)"><strong>WSPRdmaWrite</strong></a></p></td>
<td align="left"><p>{C0B422F9-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566304" data-raw-source="[&lt;strong&gt;WSPRdmaRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566304)"><strong>WSPRdmaRead</strong></a></p></td>
<td align="left"><p>{C0B422FA-F58C-11d1-AD6C-00C04FA34A2D}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566299" data-raw-source="[&lt;strong&gt;WSPMemoryRegistrationCacheCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566299)"><strong>WSPMemoryRegistrationCacheCallback</strong></a></p></td>
<td align="left"><p>{E5DA4AF8-D824-48CD-A799-6337A98ED2AF}</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="sio-get-qos--sio-get-group-qos--sio-set-qos--sio-set-group-qos"></a>SIO\_取得\_QOS、SIO\_取得\_グループ\_QOS、SIO\_設定\_QOS、SIO\_設定\_グループ\_QOS  
SAN サービス プロバイダーは、QoS をサポートしている場合、これらの制御コードをサポートする必要があります。 それ以外の場合、スイッチは、これらのオプションを既定値を保持する TCP/IP プロバイダーに転送します。 プロバイダーは、XP1 を設定して、QoS をサポートしていることを示します\_QOS\_でサポートされているビット、 **dwServiceFlags** 、WSAPROTOCOL のメンバー\_情報構造体。

<a href="" id="sio-address-list-query"></a>SIO\_アドレス\_一覧\_クエリ  
SAN サービス プロバイダー コントロールがするネットワーク インターフェイス カード (Nic) に割り当てられているローカルの IP アドレスの一覧を取得します。 SAN サービス プロバイダーが、ソケットを使用して\_アドレス\_の一覧を返すように、次のように定義のリスト構造**WSPIoctl**の出力バッファー。

```C++
typedef struct _SOCKET_ADDRESS_LIST {
    INT             iAddressCount; 
    SOCKET_ADDRESS  Address[1]; 
} SOCKET_ADDRESS_LIST, FAR * LPSOCKET_ADDRESS_LIST;
```

この構造体のメンバーには、次の情報が含まれます。

<a href="" id="iaddresscount"></a>**iAddressCount**  
一覧で、アドレスの構造体の数を指定します。

<a href="" id="address"></a>**アドレス**  
IP アドレスの構造体の配列。

スイッチは、特定の SAN サービス プロバイダーを使用して接続するために、または着信接続をリッスンするのにアプリケーションの要求を実行するのにかどうかを決定するのに内部この IOCTL コードを使用します。 スイッチは、TCP/IP プロバイダーに、ローカル IP アドレスの一覧については、実際のアプリケーション要求を転送します。 スイッチでは、すべての SAN サービス プロバイダーのサービスがするアドレス一覧に変更を検出するために TCP/IP プロバイダーも使用します。 TCP/IP が変更を報告した後、スイッチは、すべての SAN サービス プロバイダーのリストを更新するを照会します。

 

 





