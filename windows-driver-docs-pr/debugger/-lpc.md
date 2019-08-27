---
title: lpc
description: Lpc 拡張機能には、ターゲットシステムのすべてのローカルプロシージャコール (LPC) ポートとメッセージに関する情報が表示されます。
ms.assetid: d474aeca-fb12-424a-b57e-360215d0305c
keywords:
- LPC (ローカル/軽量プロシージャ呼び出し)
- lpc Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lpc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b18ea2c3accfe8a76a5bb81ad026adf779f5f5a1
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025204"
---
# <a name="lpc"></a>!lpc


**重要な**   Lpc が alpc でエミュレートされるようになりました。代わりに、! alpc 拡張機能を使用してください。

 
**! Lpc**拡張機能では、ターゲットシステムのすべてのローカルプロシージャコール (lpc) ポートとメッセージに関する情報が表示されます。

```dbgcmd
!lpc message MessageID 
!lpc port Port 
!lpc scan Port 
!lpc thread Thread 
!lpc PoolSearch 
!lpc
```

## <a name="span-idddk__lpc_dbgspanspan-idddk__lpc_dbgspanparameters"></a><span id="ddk__lpc_dbg"></span><span id="DDK__LPC_DBG"></span>パラメータ


<span id="_______message______"></span><span id="_______MESSAGE______"></span>**メッセージ**   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)キュー内のメッセージを含むサーバーポートや、このメッセージを待機しているスレッド (存在する場合) など、メッセージに関する情報を表示します。

<span id="_______MessageID______"></span><span id="_______messageid______"></span><span id="_______MESSAGEID______"></span>*MessageID*   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)表示するメッセージのメッセージ ID を指定します。 このパラメーターの値が0の場合、またはこのパラメーターを省略した場合、 **! lpc message**コマンドを実行すると、メッセージの概要リストが表示されます。 (Windows 2000 Service Pack 1 (SP1) の概要には、LPC ゾーン内のすべてのメッセージが含まれています。 Windows 2000 Service Pack 2 (SP2)、Windows XP、およびそれ以降のバージョンの Windows では、概要にカーネルプール内のすべてのメッセージが含まれています。 ページアウトされたメッセージは含まれません。)

<span id="_______port______"></span><span id="_______PORT______"></span>**ポート**   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)ポートの名前、そのセマフォの状態、キュー内のメッセージ、ランダウンキュー内のスレッド、ハンドル数、その参照、関連ポートなど、ポート情報が表示されます。

<span id="_______scan______"></span><span id="_______SCAN______"></span>**スキャン**   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)指定したポートとそれに接続されているすべてのポートに関する概要情報が表示されます。

<span id="_______Port______"></span><span id="_______port______"></span><span id="_______PORT______"></span>*ポート*   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)表示するポートの16進数のアドレスを指定します。 **! Lpc port**コマンドが使用され、 *port*が0であるか省略されている場合は、すべての lpc ポートの概要リストが表示されます。 **! Lpc scan**コマンドが使用されている場合、*ポート*は実際のポートのアドレスを指定する必要があります。

<span id="_______thread______"></span><span id="_______THREAD______"></span>**スレッド**   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)ランダウンポートキュー内の指定されたスレッドを含むすべてのポートのポート情報を表示します。

<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*スレッド*   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)スレッドの16進数のアドレスを指定します。 このが0または省略された場合、 **! lpc thread**コマンドを実行すると、すべての lpc 操作を実行しているすべてのスレッドの概要リストが表示されます。

<span id="_______PoolSearch______"></span><span id="_______poolsearch______"></span><span id="_______POOLSEARCH______"></span>**Poolsearch**   
(Windows Server 2003 および Windows XP のみ) **! Lpc message**コマンドでカーネルプール内のメッセージを検索するかどうかを決定します。 各時間を使用して、 **Lpc PoolSearch**が使用されます。この設定は、オンまたはオフにします (初期設定では、カーネルプールを検索しません)。 これは、 *MessageID*に0以外の値を指定する **! lpc メッセージ**コマンドにのみ影響します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p>
<p><strong>Windows Server 2003</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

LPCs の詳細については、Windows Driver Kit (WDK) のドキュメントおよび*Microsoft windows の内部*(Mark Russinovich と David ソロモン) を参照してください。

<a name="remarks"></a>コメント
-------

この拡張機能は、Windows Vista 以降のバージョンの Windows ではサポートされていません。

Windows Server 2003、Windows XP、および Windows 2000 では、 **! lpc**を引数なしで使用すると、デバッガーコマンドウィンドウでこの拡張機能のヘルプが表示されます。

メッセージへの応答を待機しているとマークされているスレッドがある場合は、 **! lpc message**コマンドに遅延メッセージの ID を指定します。 このコマンドは、指定されたメッセージ、それを含むポート、およびすべての関連スレッドを表示します。

メッセージが見つからず、読み取りエラー ("ゾーンセグメントにアクセスできません" など) がない場合、サーバーはメッセージを受信しました。

この場合、サーバーポートは通常、 **! lpc thread**コマンドを使用して検出できます。 応答を待機しているスレッドは、サーバーの通信キューにリンクされます。 このコマンドは、指定されたスレッドを含むすべてのポートを表示します。 ポートアドレスを確認したら、 **! lpc port**コマンドを使用します。 各スレッドに関するより具体的な情報を取得するには、 **! lpc thread**コマンドに各スレッドのアドレスを指定します。

Windows XP システムからのこの拡張機能からの出力の例をいくつか次に示します。

この例では、すべてのポート LPC ポートが表示されます。

```dbgcmd
kd> !lpc port
Scanning 225 objects
       1  Port: 0xe1405650 Connection: 0xe1405650  Communication: 0x00000000  'SeRmCommandPort' 
       1  Port: 0xe141ef50 Connection: 0xe141ef50  Communication: 0x00000000  'SmApiPort' 
       1  Port: 0xe13c5740 Connection: 0xe13c5740  Communication: 0x00000000  'ApiPort' 
       1  Port: 0xe13d9550 Connection: 0xe13d9550  Communication: 0x00000000  'SbApiPort' 
       3  Port: 0xe13d8830 Connection: 0xe141ef50  Communication: 0xe13d8910  ' 
80000004  Port: 0xe13d8910 Connection: 0xe141ef50  Communication: 0xe13d8830  ' 
       3  Port: 0xe13d8750 Connection: 0xe13d9550  Communication: 0xe13a4030  ' 
       .....
```

前の例では、アドレス e14ae238 のポートにはメッセージがありません。つまり、すべてのメッセージが取得され、新しいメッセージは届いていません。

```dbgcmd
kd> !lpc port e14ae238

Server connection port e14ae238  Name: ApiPort
 Handles: 1   References: 107
    Server process  : 84aa0140 (csrss.exe)
    Queue semaphore : 84a96da8
 Semaphore state 0 (0x0)
    The message queue is empty
    The LpcDataInfoChainHead queue is empty
```

前の例では、0xe14ae238 のポートにキューに登録されたメッセージがありますが、サーバーによってまだ選択されていません。

```dbgcmd
kd> !lpc port 0xe14ae238

Server connection port e14ae238  Name: ApiPort
 Handles: 1   References: 108
    Server process  : 84aa0140 (csrss.exe)
    Queue semaphore : 84a96da8
 Semaphore state 0 (0x0)
        Messages in queue:
 0000 e20d9b80 - Busy  Id=0002249c  From: 0584.0680  Context=00000021  [e14ae248 . e14ae248]
 Length=0098007c  Type=00000001 (LPC_REQUEST)
                   Data: 00000000 0002021e 00000584 00000680 002f0001 00000007
    The message queue contains 1 messages
    The LpcDataInfoChainHead queue is empty
```

残りの Windows XP の例では、この拡張機能で使用できるその他のオプションについて考慮しています。

```dbgcmd
kd> !lpc message 222be
Searching message 222be in threads ...
Client thread 842a4db0 waiting a reply from 222be
Searching thread 842a4db0 in port rundown queues ...

Server communication port 0xe114a3c0
    Handles: 1   References: 1
    The LpcDataInfoChainHead queue is empty
        Connected port: 0xe1e7b948      Server connection port: 0xe14ae238

Client communication port 0xe1e7b948
    Handles: 1   References: 3
    The LpcDataInfoChainHead queue is empty

Server connection port e14ae238  Name: ApiPort
 Handles: 1   References: 107
    Server process  : 84aa0140 (csrss.exe)
    Queue semaphore : 84a96da8
 Semaphore state 0 (0x0)
    The message queue is empty
    The LpcDataInfoChainHead queue is empty
Done.
```

```dbgcmd
kd> !lpc thread 842a4db0
Searching thread 842a4db0 in port rundown queues ...

Server communication port 0xe114a3c0
    Handles: 1   References: 1
    The LpcDataInfoChainHead queue is empty
        Connected port: 0xe1e7b948      Server connection port: 0xe14ae238

Client communication port 0xe1e7b948
    Handles: 1   References: 3
    The LpcDataInfoChainHead queue is empty

Server connection port e14ae238  Name: ApiPort
 Handles: 1   References: 107
    Server process  : 84aa0140 (csrss.exe)
    Queue semaphore : 84a96da8
 Semaphore state 0 (0x0)
    The message queue is empty
    The LpcDataInfoChainHead queue is empty
```

```dbgcmd
kd> !lpc scan e13d8830
Scanning 225 objects
       3  Port: 0xe13d8830 Connection: 0xe141ef50  Communication: 0xe13d8910  ' 
80000004  Port: 0xe13d8910 Connection: 0xe141ef50  Communication: 0xe13d8830  ' 
Scanning 3 objects
```

 

 





