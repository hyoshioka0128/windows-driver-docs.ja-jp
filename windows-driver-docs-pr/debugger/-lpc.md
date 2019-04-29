---
title: lpc
description: Lpc 拡張機能では、ターゲット システムですべてのローカル プロシージャ呼び出し (LPC) ポートとメッセージに関する情報が表示されます。
ms.assetid: d474aeca-fb12-424a-b57e-360215d0305c
keywords:
- LPC (ローカル/軽量プロシージャ コール)
- Windows デバッグ lpc
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lpc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e7d92d68ccd103c89f747baf87557e837778c39
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336160"
---
# <a name="lpc"></a>!lpc


**重要な**   alpc で Lpc がエミュレートされるようになりましたを使用して、! alpc 拡張子代わりにします。

 
**! Lpc**拡張機能は、ターゲット システムですべてのローカル プロシージャ呼び出し (LPC) のポートおよびメッセージに関する情報を表示します。

```dbgcmd
!lpc message MessageID 
!lpc port Port 
!lpc scan Port 
!lpc thread Thread 
!lpc PoolSearch 
!lpc
```

## <a name="span-idddklpcdbgspanspan-idddklpcdbgspanparameters"></a><span id="ddk__lpc_dbg"></span><span id="DDK__LPC_DBG"></span>パラメーター


<span id="_______message______"></span><span id="_______MESSAGE______"></span> **message**   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)存在する場合は、キュー、および、このメッセージを待っているスレッドでメッセージを含むサーバーのポートなど、メッセージに関する情報が表示されます。

<span id="_______MessageID______"></span><span id="_______messageid______"></span><span id="_______MESSAGEID______"></span> *メッセージ Id*   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)表示されるメッセージのメッセージ ID を指定します。 このパラメーターの値は 0、またはこのパラメーターを省略した場合、 **! lpc メッセージ**コマンド メッセージの一覧を表示します。 (Windows 2000 Service Pack 1 (SP1) で概要を含む LPC ゾーン内のすべてのメッセージ。 Service Pack 2 (SP2)、Windows XP では、以降のバージョンの Windows と Windows 2000 では、概要には、カーネル プールのすべてのメッセージが含まれています。 Paged-out メッセージは含まれません)。

<span id="_______port______"></span><span id="_______PORT______"></span> **ポート**   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)ポート、そのセマフォの状態、そのキューのメッセージ、ランダウンのキュー、そのハンドルの数、その参照、および関連ポート内のスレッドの名前などのポート情報を表示します。

<span id="_______scan______"></span><span id="_______SCAN______"></span> **scan**   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)指定したポートとそれに接続されているすべてのポートについての概要情報が表示されます。

<span id="_______Port______"></span><span id="_______port______"></span><span id="_______PORT______"></span> *ポート*   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)表示されるポートの 16 進数のアドレスを指定します。 場合、 **! lpc ポート**コマンドを使用すると、および*ポート*は 0 です。 または、省略すると、すべての LPC ポートの概要一覧が表示されます。 場合、 **! lpc スキャン**コマンドを使用すると、*ポート*実際のポートのアドレスを指定する必要があります。

<span id="_______thread______"></span><span id="_______THREAD______"></span> **thread**   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)ランダウンのポート、キュー内の指定したスレッドが含まれているすべてのポートのポート情報を表示します。

<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
(Windows Server 2003、Windows XP、および Windows 2000 のみ)スレッドの 16 進数のアドレスを指定します。 0 または省略するの場合は、 **! lpc スレッド**コマンド LPC のすべての操作を実行しているすべてのスレッドの一覧を表示します。

<span id="_______PoolSearch______"></span><span id="_______poolsearch______"></span><span id="_______POOLSEARCH______"></span> **PoolSearch**   
(Windows Server 2003 および Windows XP の場合のみ)決定かどうか、 **! lpc メッセージ**コマンド カーネル プール内のメッセージを検索します。 毎回 **! lpc PoolSearch**が使用すると、この設定を切り替えますオンまたはオフ (初期設定では、カーネルのプールを検索できません)。 これにのみ影響 **! lpc メッセージ**以外の値を指定するコマンド*MessageID*します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p>
<p><strong>Windows Server 2003</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Lpc については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

Windows Vista および Windows の以降のバージョンでは、この拡張機能はサポートされていません。

Windows Server 2003、Windows XP、および Windows 2000 を使用してで **! lpc**引数なしで、デバッガー コマンド ウィンドウでこの拡張機能のヘルプを表示します。

メッセージに応答を待機中としてマークされているスレッドがある場合は、使用、 **! lpc メッセージ**遅延メッセージの ID を持つコマンド。 このコマンドは、それを含んでいる、ポート、指定したメッセージを表示し、すべてのスレッドに関連します。

場合は、メッセージが見つからないし、があります (「ゾーンのセグメントをアクセスできません」) などのエラーを読み取られたいいえ、サーバーは、メッセージを受け取りました。

この場合、サーバーのポートは、通常ありますを使用して、 **! lpc スレッド**コマンド。 応答を待機しているスレッドは、サーバー通信のキューにリンクされています。 このコマンドは、指定したスレッドが含まれているすべてのポートに表示されます。 使用してポート アドレスを確認した後、 **! lpc ポート**コマンド。 各スレッドに関する詳細な情報を使用して取得できます、 **! lpc スレッド**コマンドを各スレッドのアドレスを使用します。

Windows XP システムからこの拡張機能からの出力のいくつかの例を次に示します。

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

前の例では、アドレス e14ae238 でポートにメッセージがありません。つまり、すべてのメッセージが検出された、新しいメッセージが到着しません。

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

前の例では、0xe14ae238 でポートには、キューに登録されているが、サーバーによって取得されていないメッセージ、します。

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

その他の Windows XP の例では、この拡張機能で使用できるその他のオプションに関するものです。

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

 

 





