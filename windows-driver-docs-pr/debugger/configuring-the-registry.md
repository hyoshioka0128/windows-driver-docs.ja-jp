---
title: レジストリの構成
description: レジストリの構成
ms.assetid: 69a1dd39-c4aa-491d-9e28-fd1661ec9a7a
keywords:
- SymProxy、registry
- Proxycfg.exe と SymProxy
- Netsh および SymProxy
ms.date: 03/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5453a38b46b66b1654375ccf69079e32d79f9d3e
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557769"
---
# <a name="configuring-the-registry"></a>レジストリの構成


SymProxy は、このレジストリキーに設定を格納します。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

このレジストリキーは、Web サイトに格納するシンボルの検索場所、ログ記録レベル、および SymProxy がネットワークへの直接接続で動作するかどうかを制御します。 このキーを作成するには、Windows 用デバッグツールで提供されている SymProxy 登録ツール (Symproxy reg) を実行します。 コマンドプロンプトで「 **symproxy .reg** 」と入力するか、Windows エクスプローラーでダブルクリックします。

これにより、"x" というプレフィックスが付いた設定のエントリが追加され、無効になります。 設定を有効にするには、目的の設定の先頭から "x" を削除します。

```reg
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Symbol Server Proxy]
"Available Settings"="Remove the 'x' prefix to use the setting"
"xMissAgeTimeout"=dword:00015180
"xMissAgeCheck"=dword:00000e10
"xMissTimeout"=dword:00000e10
"xNoCache"=dword:00000001
"xNoFilePointers"=dword:00000001
"xNoInternetProxy"=dword:00000001
"xNoLongerIndexedAuthoritive"=dword:00000001
"xNoUncompress"=dword:00000001
"xRequestTimeout"=dword:0000019
"xRetryAppHang"=dword:0000002
"xUriFilter"=dword:00000FF
"xUriTiers"=dword:0000001
```

Symproxy .reg レジストリファイルは、シンボルの仮想ディレクトリ名を前提としており、Microsoft パブリックシンボルサーバーを使用するようにシンボルパスを構成します。

```reg
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Symbol Server Proxy\Web Directories]

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Symbol Server Proxy\Web Directories\Symbols]
"SymbolPath"="https://msdl.microsoft.com/download/symbols"
```

Symproxy .reg のイベントログエントリについては、このトピックの「イベントログ」セクションで説明します。

```reg
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\Microsoft-Windows-SymProxy]
"ProviderGuid"="{0876099c-a903-47ff-af14-52035bb479ef}"
"EventMessageFile"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,\
  00,6f,00,74,00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,\
  5c,00,69,00,6e,00,65,00,74,00,73,00,72,00,76,00,5c,00,53,00,79,00,6d,00,50,\
  00,72,00,6f,00,78,00,79,00,2e,00,64,00,6c,00,6c,00,00,00
"TypesSupported"=dword:00000007
```

このトピックでは、symproxy .reg の web ディレクトリエントリについて説明します。

### <a name="span-idweb_directoriesspanspan-idweb_directoriesspanweb-directories"></a><span id="web_directories"></span><span id="WEB_DIRECTORIES"></span>Web ディレクトリ

シンボルストアとして使用している IIS で生成された仮想ディレクトリごとに、次のレジストリキーの**Web ディレクトリ**サブキーの下にレジストリキーを設定する必要があります。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

**シンボルストアの仮想ディレクトリのレジストリキーを編集するには**

-   SymProxy シンボルストアによって使用されるすべてのシンボルストアを含むように、シンボルの**内容を編集**します。 複数のシンボルストアが使用されている場合は、セミコロンで区切ります。 各値に対して最大10個のストアがサポートされています。 HTTP パスには**https://プレフィックス**を含める必要があり、UNC パスにはプレフィックスを含める必要があり **\\\\** ます。

たとえば、仮想ディレクトリの1つがシンボルと呼ばれており、それがアクセスするシンボルストアが UNC ストア \\ \\ シンボルと HTTP ストアにある場合、 \\ https://msdl.microsoft.com/download/symbols 次のレジストリキーを作成します。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy/Web Directories/Symbols
```

このキーを作成した後、シンボル**パス**をシンボルシンボルに編集し \\ \\ \\ <https://msdl.microsoft.com/download/symbols> ます。 これは、レジストリエディターの次のスクリーンショットで確認できます。

![変更されたシンボルパスを示すレジストリエディターのスクリーンショット](images/symproxy-registry.png)

この例では、SymProxy は最初にシンボルのシンボルを検索 \\ \\ \\ します。 ファイルが見つからない場合は、Microsoft シンボルストアが使用されます。

-   Web ディレクトリの下にある、仮想ディレクトリ名と一致する各キーで、 \_ シンボルパスという名前の REG SZ を作成する必要があります。 値には、SymProxy シンボルストアを設定するために使用されるすべてのアップストリームシンボルストアが含まれます。

-   最大10個のエントリがサポートされています。

-   エントリをセミコロンで区切ります。

-   UNC パスには " \\ " プレフィックスを含める必要があります \\

-   HTTP パスには、"https://" プレフィックスを含める必要があります

-   値は、最もコストが低いものから順に並べ替えてください。

    - 計算では、使用状況のパフォーマンス目標とサーバーとデータの通信コストのバランスを取る必要があります。

    - 一般に、インターネット HTTP サーバーの前にローカルの SMB/HTTP サーバーを配置します。

### <a name="span-idsymproxy_performance_countersspanspan-idsymproxy_performance_countersspanspan-idsymproxy_performance_countersspansymproxy-performance-counters"></a><span id="SymProxy_Performance_Counters"></span><span id="symproxy_performance_counters"></span><span id="SYMPROXY_PERFORMANCE_COUNTERS"></span>SymProxy パフォーマンスカウンター

SymProxy は、SymProxy と呼ばれるプロバイダーを使用してパフォーマンスカウンターを出力できます。

パフォーマンスカウンターのサポートを有効にするには、管理者コマンドウィンドウで symproxy マニフェストファイルを登録します。

```console
C:\> lodctr.exe /m:%WINDIR%\system32\inetsrv\symproxy.man
```

パフォーマンスカウンターのサポートを無効にするには、マニフェストの登録を解除します。

```console
C:\> unlodctr.exe /m:%WINDIR%\system32\inetsrv\symproxy.man
```

### <a name="span-idsymproxy_event_tracing_for_windowsspanspan-idsymproxy_event_tracing_for_windowsspanspan-idsymproxy_event_tracing_for_windowsspansymproxy-event-tracing-for-windows"></a><span id="SymProxy_Event_Tracing_for_Windows"></span><span id="symproxy_event_tracing_for_windows"></span><span id="SYMPROXY_EVENT_TRACING_FOR_WINDOWS"></span>SymProxy Windows イベントトレーシング

SymProxy は、Microsoft-Windows-SymProxy と呼ばれるプロバイダーを使用して ETW イベントを作成できます。

```console
C:\> logman query providers | findstr SymProxy
Microsoft-Windows-SymProxy {0876099C-A903-47FF-AF14-52035BB479EF}
```

ETW のサポートを有効にするには、マニフェストファイルを登録します。

```console
C:\> wevtutil.exe install-manifest %WINDIR%\system32\inetsrv\symproxy.man
```

ETW のサポートを無効にするには、マニフェストファイルの登録を解除します。

```console
C:\> wevtutil.exe uninstall-manifest %WINDIR%\system32\inetsrv\symproxy.man
```

### <a name="span-idevent_logspanspan-idevent_logspanspan-idevent_logspanevent-log"></a><span id="Event_Log"></span><span id="event_log"></span><span id="EVENT_LOG"></span>イベントログ

ETW が構成されている場合、イベントはイベントとしてイベントとして記録されます。このイベント*は、イベント*ログの [*アプリケーションとサービスログ] の [ \\ Microsoft \\ Windows \\ symproxy* ] に記録されます。

イベントログエントリのメッセージを正しく表示するには、symproxy .reg ファイルのイベントログ領域をレジストリに追加する必要があります。

```reg
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\Microsoft-Windows-SymProxy]
"ProviderGuid"="{0876099c-a903-47ff-af14-52035bb479ef}"
"EventMessageFile"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,\
  00,6f,00,74,00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,\
  5c,00,69,00,6e,00,65,00,74,00,73,00,72,00,76,00,5c,00,53,00,79,00,6d,00,50,\
  00,72,00,6f,00,78,00,79,00,2e,00,64,00,6c,00,6c,00,00,00
"TypesSupported"=dword:00000007
```

### <a name="span-idsymproxy_eventsspanspan-idsymproxy_eventsspanspan-idsymproxy_eventsspansymproxy-events"></a><span id="SymProxy_Events"></span><span id="symproxy_events"></span><span id="SYMPROXY_EVENTS"></span>SymProxy イベント

SymProxy は、次のイベントをログに記録します。

| **イベント ID** | **説明**                   | **チャネル** |
|--------------|-----------------------------------|-------------|
| 1            | ISAPI フィルターの開始         | [Admin]       |
| 2            | ISAPI フィルターの停止          | [Admin]       |
| 3            | ISAPI フィルターの構成 | [Admin]       |
| 4            | キャッシュの統計情報を見逃す             | [Admin]       |
| 10           | URL 要求-ローカルキャッシュヒット     | 運用時 |
| 11           | URL 要求-ローカルキャッシュミス    | 運用時 |
| 20           | SymSrv 経由のシンボルのダウンロード        | 運用時 |
| 30           | クリティカルシンボルが見つかりません           | [Admin]       |
| 31           | 重要なイメージが見つかりません            | [Admin]       |
| 40           | SymSrv –パスが見つかりません           | [Admin]       |
| 41           | SymSrv –ファイルが見つかりません           | [Admin]       |
| 42           | SymSrv –アクセスが拒否されました            | [Admin]       |
| 43           | SymSrv –パスが長すぎます            | [Admin]       |
| 49           | SymSrv –エラーコード               | [Admin]       |
| 90           | ロック競合                   | 運用時 |
| 100          | 一般的な重大なメッセージ          | 分析    |
| 101          | 一般的なエラーメッセージ             | 分析    |
| 102          | 一般的な警告メッセージ           | 分析    |
| 103          | 一般情報メッセージ     | 分析    |
| 104          | 一般的な分析メッセージ          | 分析    |
| 105          | 一般的なデバッグメッセージ             | デバッグ       |



### <a name="span-idsymbol_server_proxy_configurationspanspan-idsymbol_server_proxy_configurationspanspan-idsymbol_server_proxy_configurationspansymbol-server-proxy-configuration"></a><span id="Symbol_Server_Proxy_Configuration"></span><span id="symbol_server_proxy_configuration"></span><span id="SYMBOL_SERVER_PROXY_CONFIGURATION"></span>シンボルサーバープロキシの構成

SymProxy は、次のレジストリキー領域に構成設定を格納します。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

この場所から、SymProxy はグローバル設定と上流シンボルストアのシンボルパスを取得します。

このキーを作成するには、前に説明した手順でカスタマイズした symproxy .reg ファイルをマージします。

### <a name="span-idsymbol_server_proxy__keyspanspan-idsymbol_server_proxy__keyspanspan-idsymbol_server_proxy__keyspansymbol-server-proxy-key"></a><span id="Symbol_Server_Proxy__key"></span><span id="symbol_server_proxy__key"></span><span id="SYMBOL_SERVER_PROXY__KEY"></span>シンボルサーバープロキシキー

シンボルサーバープロキシのレジストリキーは、次のグローバル設定 (すべての REG DWORD) をサポートしてい \_ ます。 アプリケーションプールをリサイクルして、設定をライブで適用することができます。 新しい w3wp.exe プロセスが作成され、新しい値が読み取られます。 古い w3wp.exe プロセスに対する保留中の要求がすべて完了すると、古い w3wp.exe プロセスが終了します。 既定では、IIS は1740分 (29 時間) ごとに w3wp.exe プロセスをリサイクルします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">REG_DWORD</td>
<td align="left">説明</td>
</tr>
<tr class="odd">
<td align="left">NoInternetProxy</td>
<td align="left"><p>サービスとして実行している場合、SymSrv.dll は、WinInet ではなく WinHTTP を使用して HTTP 要求を行います。 そのため、サービスがネットワークリソースの外部にアクセスできるように、HTTP プロキシ設定を設定する必要がある場合があります。 これは netsh プログラムを使用して行うことができます。 「netsh.exe winhttp-?」と入力します。 を参照してください。</p>
<p>既定では、SymProxy は、指定された HTTP プロキシを使用します。 HTTP プロキシが構成されていない場合、SymProxy はダミープロキシを使用します。 これにより、イントラネット内の HTTP サイトへのセキュリティで保護されたアクセスが可能になります。 副作用として、SymProxy がセキュリティで保護されていないサイトに直接接続するのを防ぐことができます。</p>
<p>REG_DWORD の作成: "NoInternetProxy" 値は、直接接続を許可する、プロキシを使用せずに動作するように SymProxy を構成します。</p></td>
</tr>
<tr class="even">
<td align="left">NoFilePointers</td>
<td align="left"><p>既定では、存在しないシンボルの場合、SymProxy は、要求されたファイル (ローカルキャッシュ内) の横にあるファイルの ptr ファイルを検索します。 見つかった場合は、ファイルの ptr ファイルによって指定された場所が返されます。 この機能は、ローカルキャッシュが SymStore.exe によって設定されている場合にのみ必要です。</p>
<p>参照をスキップするには、REG_DWORD: "NoFilePointers" の値を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left">NoUncompress</td>
<td align="left"><p>既定では、SymProxy は、ファイルを呼び出し元に返す前に、ダウンロードされたシンボルを圧縮解除します。 これにより、クライアント側の CPU が減少しますが、i/o が増加します。</p>
<p>REG_DWORD: "NoUncompress" 値を作成して、展開をスキップします。</p></td>
</tr>
<tr class="even">
<td align="left">NoCache</td>
<td align="left"><p>既定では、SymProxy はダウンロードしたシンボルを仮想ディレクトリのパスで定義されたローカルファイルシステムにキャッシュします。</p>
<p>REG_DWORD を作成します。 "NoCache" 値を作成してダウンロードをスキップし、代わりにファイルのリモートパスをクライアントに提供します。</p></td>
</tr>
<tr class="odd">
<td align="left">MissTimeout</td>
<td align="left"><p>アップストリームシンボルサーバーを再照会せずに、欠落しているシンボルが見つからないと報告されるタイムアウト期間 (秒単位)。</p>
<p>ミスは UTC ベースの時刻に関連付けられています。 ファイルに対する後続の要求は、すぐに N 秒間拒否されます。</p>
<p>N 秒後にファイルの最初の要求が発生すると、アップストリームのシンボルストアが再照会されます。</p>
<p>成功すると、シンボルファイルが返され、ミスが削除されます。</p>
<p>失敗した場合は、現在の時刻 (UTC) に移動して、新しいタイムアウト期間を開始します。</p>
<p>"ミスキャッシュ" カウンターを使用して <em> 、ミスを監視します。</p>
<p><ul>
    <li>未指定-(既定値) 300 秒/5 分</li>
    <li>0: 機能が無効です。</li>
    <li>N –タイムアウトの継続 N 秒</li>
   </ul>
</td>
</tr>
<tr class="even">
<td align="left">MissAgeCheck</td>
<td align="left"><p>期限チェックの間隔。 ミスキャッシュがスキャンされ、誤検出時間よりも古いレコードが削除されます。</p>
<p>現在の統計情報は、イベント ID 4 を使用してイベントログに保存されます。</p>
<p><ul>
    <li>未指定-(既定値) 3600 秒/1 時間</li>
    <li>0: 機能が無効です。</li>
    <li>N – N 秒間のチェックの間隔</li>
   </ul>
</td>
</tr>
<tr class="odd">
<td align="left"><p>FailureTimeout</p>
<p>FailureCount</p>
<p>FailurePeriod</p>
<p>FailureBlackout アウト</p></td>
<td align="left"><p>ブラックアウト機能は、応答しないアップストリームシンボルストアを termporarly 無効にするために使用されます。 ブラックアウト機能では、4つの REG_DWORD 値を使用して、の動作を定義します。 既定では、この機能は無効になっています。</p>
<p>シンボルパスで定義されている上流シンボルストアごとに、エラーが個別に記録されます。 要求の実行時間が FailureTimeout (ミリ秒) を超えた場合、エラー数が増加します。</p>
<p>シンボルパスは、FailurePeriod 秒の FailureCount に失敗した後に、配信不能としてマークされます。 現時点では、FailureBlackout の秒数が経過するまで、すべての要求は無視されます。 タイムアウト後の最初の呼び出し元は、アップストリームシンボルストアをテストします。 成功すると、タイムアウトが削除され、要求が許可されます。 失敗した場合、時刻は Now + FailureBlackout ダウン秒に設定されます。 その後、アップストリームシンボルストアは再テストされます。</p></td>
</tr>
<tr class="even">
<td align="left">誤 Sagetimeout</td>
<td align="left"><p>説明保留中</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">RequestTimeout</td>
<td align="left"><p>説明保留中</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left">RetryAppHang</td>
<td align="left"><p>説明保留中</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">NoLongerIndexedAuthoritive</td>
<td align="left"><p>説明保留中</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left">UriFilter</td>
<td align="left"><p>説明保留中</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">UriTiers</td>
<td align="left"><p>説明保留中</p>
<p></p></td>
</tr>
</tbody>
</table>



### <a name="span-idaccessing_outside_network_resourcesspanspan-idaccessing_outside_network_resourcesspanaccessing-outside-network-resources"></a><span id="accessing_outside_network_resources"></span><span id="ACCESSING_OUTSIDE_NETWORK_RESOURCES"></span>ネットワークリソース外へのアクセス

SymSrv と Symsrv を組み合わせて使用すると、サービスとして実行され、WinHTTP API を使用して HTTP 接続経由でシンボルにアクセスします。 これは、この目的で WinInet を使用する通常の動作とは異なります。

そのため、このサービスがネットワークリソースの外部にアクセスできるように、HTTP プロキシ設定を設定することが必要になる場合があります。 これらの設定を構成するには、次のいずれかの方法を使用します。

-   Netsh ツール (netsh.exe) を使用します。 手順については、コマンドプロンプトウィンドウで次のように入力します。

    ```console
    netsh winhttp -? 
    ```

SymProxy の既定の動作では、Proxycfg.exe または Netsh のいずれかによって指定された HTTP プロキシが使用されます。 HTTP プロキシが構成されていない場合、SymProxy はダミープロキシを使用して、イントラネット内のセキュリティで保護された HTTP サイトへのアクセスを許可します。 副作用として、この手法は、SymProxy が外部インターネットへの直接接続を処理できないようにします。 SymProxy でインターネットへの直接接続を使用することを許可する場合は、 \_ レジストリの**シンボルサーバープロキシ**キーに**nointernetproxy**という名前の REG DWORD 値を作成します。 **Nointernetproxy**の値を1に設定し、proxycfg.exe によって示される HTTP プロキシが存在しないことを確認します。

