---
title: レジストリの構成
description: レジストリの構成
ms.assetid: 69a1dd39-c4aa-491d-9e28-fd1661ec9a7a
keywords:
- SymProxy、レジストリ
- ProxyCfg と SymProxy
- Netsh と SymProxy
ms.date: 03/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: e47fd16f420e3464a6cc1420aab93b94f8e8534a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375585"
---
# <a name="configuring-the-registry"></a>レジストリの構成


SymProxy では、このレジストリ キーでその設定が格納されます。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

このレジストリ キーを制御記号を見つける対象の場所は、Web サイト、ログ出力レベル、および SymProxy がネットワークへの直接接続で動作するかどうかに格納します。 Windows のツールをデバッグで提供される SymProxy 登録ツール (Symproxy.reg) を実行して、このキーを作成できます。 型**symproxy.reg**コマンド プロンプトまたは Windows エクスプ ローラーからそれをダブルクリックします。

これにより、設定を無効にするために、"x"プレフィックスのエントリが追加されます。 設定を有効にするには、目的の設定の前にある"x"を削除します。

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

Symproxy.reg レジストリ ファイルは、シンボルの仮想ディレクトリ名を前提としていて、Microsoft パブリック シンボル サーバーを使用するシンボル パスを構成します。

```reg
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Symbol Server Proxy\Web Directories]

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Symbol Server Proxy\Web Directories\Symbols]
"SymbolPath"="https://msdl.microsoft.com/download/symbols"
```

Symproxy.reg でイベント ログ エントリは、このトピックのイベント ログのセクションでは後者では説明します。

```reg
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\Microsoft-Windows-SymProxy]
"ProviderGuid"="{0876099c-a903-47ff-af14-52035bb479ef}"
"EventMessageFile"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,\
  00,6f,00,74,00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,\
  5c,00,69,00,6e,00,65,00,74,00,73,00,72,00,76,00,5c,00,53,00,79,00,6d,00,50,\
  00,72,00,6f,00,78,00,79,00,2e,00,64,00,6c,00,6c,00,00,00
"TypesSupported"=dword:00000007
```

このトピックでは、symproxy.reg web ディレクトリ エントリがについて説明します。

### <a name="span-idwebdirectoriesspanspan-idwebdirectoriesspanweb-directories"></a><span id="web_directories"></span><span id="WEB_DIRECTORIES"></span>Web ディレクトリ

シンボル ストアとして使用している IIS で生成された各仮想ディレクトリの下のレジストリ キーをセットアップする必要があります、 **Web ディレクトリ**次のレジストリ キーのサブキー。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

**シンボル ストアの仮想ディレクトリのレジストリ キーを編集するには**

-   内容を編集**SymbolPath** SymProxy シンボル ストアで使用されるシンボル ストアのすべてを格納します。 使用されている 1 つ以上のシンボル ストアがある場合は、セミコロンで区切ります。 10 ストアの最大値が値ごとにサポートされています。 HTTP パスを含める必要があります、 **https:// プレフィックス**、UNC パスを含める必要があります、 **\\ \\**プレフィックス。

たとえば、仮想ディレクトリのいずれかと、シンボルが呼び出され、UNC ストアでは、アクセス対象のシンボル ストアが配置されている場合\\\\シンボル\\シンボルと HTTP ストア https://msdl.microsoft.com/download/symbols、次のレジストリの作成キー。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy/Web Directories/Symbols
```

このキーが作成されると、編集、 **SymbolPath**する\\\\シンボル\\シンボル;<https://msdl.microsoft.com/download/symbols>。 これは、レジストリ エディターの次のスクリーン ショットで確認できます。

![変更後の symbolpath を示すレジストリ エディターのスクリーン ショット](images/symproxy-registry.png)

この例で、SymProxy まず検索内のシンボル\\\\シンボル\\シンボル。 ファイルが見つからない場合があります、Microsoft のシンボル ストアが使用されます。

-   レジストリの仮想ディレクトリ名に一致する Web ディレクトリの下のキーの各\_SymbolPath と呼ばれる SZ を作成する必要があります。 値には、SymProxy シンボル ストアの設定に使用されるすべてのアップ ストリームのシンボル ストアが含まれています。

-   最大 10 個の項目がサポートされています。

-   別のエントリはセミコロンでします。

-   UNC パスを含める必要がある、"\\\\"プレフィックス

-   HTTP パスは、"https://"プレフィックスを含める必要があります。

-   最も高価なに最もコストのかからないから値を注文します。

    - サーバーと、計算でのデータ通信コストと使用率パフォーマンスの目標のバランスを取る必要があります。

    - 一般に、インターネット HTTP サーバーの前に、ローカルの SMB または HTTP サーバーを配置します。

### <a name="span-idsymproxyperformancecountersspanspan-idsymproxyperformancecountersspanspan-idsymproxyperformancecountersspansymproxy-performance-counters"></a><span id="SymProxy_Performance_Counters"></span><span id="symproxy_performance_counters"></span><span id="SYMPROXY_PERFORMANCE_COUNTERS"></span>SymProxy パフォーマンス カウンター

SymProxy は、SymProxy と呼ばれるプロバイダー経由でのパフォーマンス カウンターを生成できます。

パフォーマンス カウンターのサポートを有効にするには、コマンド ウィンドウで管理者 symproxy マニフェスト ファイルを登録します。

```console
C:\> lodctr.exe /m:%WINDIR%\system32\inetsrv\symproxy.man
```

パフォーマンス カウンターのサポートを無効にするには、マニフェストの登録を解除します。

```console
C:\> unlodctr.exe /m:%WINDIR%\system32\inetsrv\symproxy.man
```

### <a name="span-idsymproxyeventtracingforwindowsspanspan-idsymproxyeventtracingforwindowsspanspan-idsymproxyeventtracingforwindowsspansymproxy-event-tracing-for-windows"></a><span id="SymProxy_Event_Tracing_for_Windows"></span><span id="symproxy_event_tracing_for_windows"></span><span id="SYMPROXY_EVENT_TRACING_FOR_WINDOWS"></span>SymProxy Event Tracing for Windows

SymProxy は、Microsoft-Windows-SymProxy と呼ばれるプロバイダー経由での ETW イベントを作成できます。

```console
C:\> logman query providers | findstr SymProxy
Microsoft-Windows-SymProxy {0876099C-A903-47FF-AF14-52035BB479EF}
```

ETW のサポートを有効にするには、マニフェスト ファイルを登録します。

```console
C:\> wevtutil.exe install-manifest %WINDIR%\system32\inetsrv\symproxy.man
```

ETW のサポートを無効にするには、マニフェスト ファイルの登録を解除します。

```console
C:\> wevtutil.exe uninstall-manifest %WINDIR%\system32\inetsrv\symproxy.man
```

### <a name="span-ideventlogspanspan-ideventlogspanspan-ideventlogspanevent-log"></a><span id="Event_Log"></span><span id="event_log"></span><span id="EVENT_LOG"></span>イベント ログ

内のイベントとして、イベントが記録された ETW が構成されている場合、*運用、および分析*下チャネル*Applications and Services Logs\\Microsoft\\Windows\\SymProxy*イベント ログにします。

イベント ログ エントリのメッセージを正しく表示するには、symproxy.reg ファイルのイベント ログの領域は、レジストリに追加する必要があります。

```reg
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\Microsoft-Windows-SymProxy]
"ProviderGuid"="{0876099c-a903-47ff-af14-52035bb479ef}"
"EventMessageFile"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,\
  00,6f,00,74,00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,\
  5c,00,69,00,6e,00,65,00,74,00,73,00,72,00,76,00,5c,00,53,00,79,00,6d,00,50,\
  00,72,00,6f,00,78,00,79,00,2e,00,64,00,6c,00,6c,00,00,00
"TypesSupported"=dword:00000007
```

### <a name="span-idsymproxyeventsspanspan-idsymproxyeventsspanspan-idsymproxyeventsspansymproxy-events"></a><span id="SymProxy_Events"></span><span id="symproxy_events"></span><span id="SYMPROXY_EVENTS"></span>SymProxy イベント

SymProxy には、次のイベントが記録されます。

|              |                                   |             |
|--------------|-----------------------------------|-------------|
| **イベント ID** | **説明**                   | **チャネル** |
| 1            | ISAPI フィルターの開始         | 管理       |
| 2            | ISAPI フィルターを停止します。          | 管理       |
| 3            | ISAPI フィルターの構成 | 管理       |
| 4            | キャッシュ ミスの統計             | 管理       |
| 10           | URL の要求]-[ローカル キャッシュ ヒット     | Operational |
| 11           | URL の要求]-[ローカル キャッシュ ミス    | Operational |
| 20           | SymSrv を使用してシンボルのダウンロード        | Operational |
| 30           | 重要なシンボルがありません。           | 管理       |
| 31           | 重要なイメージがありません。            | 管理       |
| 40           | SymSrv – パスが見つかりません           | 管理       |
| 41           | SymSrv – ファイルが見つかりませんでした。           | 管理       |
| 42           | SymSrv – アクセスが拒否されました            | 管理       |
| 43           | SymSrv – パスが長すぎます            | 管理       |
| 49           | SymSrv – エラー コード               | 管理       |
| 90           | ロックの競合                   | Operational |
| 100          | 一般的な重大なメッセージ          | 分析    |
| 101          | 一般的なエラー メッセージ             | 分析    |
| 102          | 一般的な警告メッセージ           | 分析    |
| 103          | 一般的な情報メッセージ     | 分析    |
| 104          | 分析の一般的なメッセージ          | 分析    |
| 105          | 一般的なデバッグ メッセージ             | デバッグ       |



### <a name="span-idsymbolserverproxyconfigurationspanspan-idsymbolserverproxyconfigurationspanspan-idsymbolserverproxyconfigurationspansymbol-server-proxy-configuration"></a><span id="Symbol_Server_Proxy_Configuration"></span><span id="symbol_server_proxy_configuration"></span><span id="SYMBOL_SERVER_PROXY_CONFIGURATION"></span>シンボル サーバー プロキシの構成

SymProxy は、次のレジストリ キーの領域にその構成設定を保存します。

```reg
HKLM/Software/Microsoft/Symbol Server Proxy
```

この場所から、SymProxy はそのグローバル設定とアップ ストリームのシンボル ストアのシンボル パスを取得します。

既に説明したようにカスタマイズした symproxy.reg ファイルにマージすることで、このキーを作成できます。

### <a name="span-idsymbolserverproxykeyspanspan-idsymbolserverproxykeyspanspan-idsymbolserverproxykeyspansymbol-server-proxy-key"></a><span id="Symbol_Server_Proxy__key"></span><span id="symbol_server_proxy__key"></span><span id="SYMBOL_SERVER_PROXY__KEY"></span>シンボル サーバーのプロキシ キー

シンボル サーバーのプロキシのレジストリ キーは、次のグローバル設定をサポートしています (すべての REG\_DWORD)。 設定は、アプリケーション プールのリサイクルをライブで適用できます。 新しい w3wp.exe プロセスが作成され、新しい値が読み取られます。 古い w3wp.exe プロセスに保留中のすべての要求が完了すると、古い w3wp.exe プロセスは終了します。 既定の IIS は 1,740 分 (29 時間) ごと w3wp.exe プロセスをリサイクルします。

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
<td align="left"><p>サービスとしての実行時に SymSrv.dll を使用して WinHTTP WinInet ではなく HTTP 要求を行います。 その結果、ネットワーク リソースの外部サービスがアクセスできるように HTTP プロキシ設定を設定する必要があります。 Netsh プログラムを使用してこれが実行できます。 型"netsh.exe winhttp のでしょうか。" 手順についてはします。</p>
<p>既定では、SymProxy は、指定された HTTP プロキシを使用します。 HTTP プロキシが構成されていない場合、SymProxy はダミーのプロキシを使用します。 これにより、HTTP サイト、イントラネット内に安全にアクセスできます。 、副作用としては、SymProxy これにより保護されていないサイトに直接接続する防ぎます。</p>
<p>REG_DWORD を作成する:"NoInternetProxy"値が、プロキシは、直接接続することがないと動作を SymProxy を構成します。</p></td>
</tr>
<tr class="even">
<td align="left">NoFilePointers</td>
<td align="left"><p>既定では、存在しないのシンボル (ローカル キャッシュ) 内の要求されたファイルの横にある file.ptr ファイル SymProxy を検索します。 見つかったが返されます file.ptr ファイルで指定された場所。 この機能は、のみ SymStore.exe でローカル キャッシュを設定しているときに必要です。</p>
<p>REG_DWORD を作成します。 ルックアップをスキップする"NoFilePointers"の値。</p></td>
</tr>
<tr class="odd">
<td align="left">NoUncompress</td>
<td align="left"><p>既定では、SymProxy は、ファイルを呼び出し元に返す前にダウンロードしたシンボルを展開します。 これで、クライアントでは、CPU を削減しますが I/O が増加します。</p>
<p>REG_DWORD を作成します。 圧縮解除をスキップする"NoUncompress"の値。</p></td>
</tr>
<tr class="even">
<td align="left">NoCache</td>
<td align="left"><p>既定では、SymProxy は仮想ディレクトリのパスで定義されている、ローカル ファイル システムにダウンロードしたシンボルをキャッシュします。</p>
<p>作成、REG_DWORD:"含む NoCache"の値は、ダウンロードをスキップする代わりに、クライアントにリモート ファイルのパスを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left">MissTimeout</td>
<td align="left"><p>タイムアウト期間を秒単位のシンボルがないが、アップ ストリームのシンボル サーバーを再クエリを使用しない不足しているとして報告されます。</p>
<p>何も見つからなかったは、ベース UTC 時間に関連付けられます。 ファイルの後続の要求は、N 秒のすぐに拒否されます。</p>
<p>再クエリすると、アップ ストリームのシンボルを N 秒後に、ファイルの最初の要求を格納します。</p>
<p>成功した場合、シンボル ファイルが返され、ミスを削除します。</p>
<p>失敗した場合は、ミスは、新しいタイムアウト期間を開始する、現在の時刻 (UTC) で前方移動します。</p>
<p>使用して、"Miss キャッシュ<em>"、ミスを監視するカウンター。</p>
<p>• が指定されていない - (既定値) 300 秒/5 分</p>
<p>• 0 – 機能を無効になっています</p>
<p>• N – タイムアウト N 秒を継続します。</p></td>
</tr>
<tr class="even">
<td align="left">MissAgeCheck</td>
<td align="left"><p>ミスの有効期間の間の期間を確認します。 キャッシュ ミスがスキャンされ、MissAgeTimeout 秒経過したレコードが削除されます。</p>
<p>現在の統計情報は、イベント ID 4 を使用して、イベント ログに保存されます。</p>
<p>• が指定されていない - (既定値) 3600 秒/1 時間</p>
<p>• 0 – 機能を無効になっています</p>
<p>• N – N 秒のチェック間隔</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FailureTimeout</p>
<p>FailureCount</p>
<p>FailurePeriod</p>
<p>FailureBlackout</p></td>
<td align="left"><p>ブラック アウト機能は、応答性の高いいる termporarly 無効にするアップ ストリームのシンボル ストアに使用されます。 ブラック アウト機能は、動作を定義するのに 4 つの REG_DWORD 値を使用します。 既定では、この機能は無効になります。</p>
<p>シンボル パスで定義されているアップ ストリームのシンボル ストアごとに、エラーは個別に記録されます。 FailureTimeout (ミリ秒) よりも、要求がかかる場合は、エラーの数が増加します。</p>
<p>シンボル パスは、FailureCount FailurePeriod (秒) が失敗した後、配信不能としてマークされます。 この時点で FailureBlackout 秒が経過するまで、すべての要求は無視されます。 タイムアウトの後の最初の呼び出し元は、アップ ストリームのシンボル ストアをテストします。 成功した場合は、タイムアウトが削除され、要求が許可されます。 失敗した場合、時刻は、今すぐ + FailureBlackout 秒に設定されます。 その後は、アップ ストリームのシンボル ストアはもう一度テストします。</p></td>
</tr>
<tr class="even">
<td align="left">MissAgeTimeout</td>
<td align="left"><p>保留中の説明</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">RequestTimeout</td>
<td align="left"><p>保留中の説明</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left">RetryAppHang</td>
<td align="left"><p>保留中の説明</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">NoLongerIndexedAuthoritive</td>
<td align="left"><p>保留中の説明</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left">UriFilter</td>
<td align="left"><p>保留中の説明</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left">UriTiers</td>
<td align="left"><p>保留中の説明</p>
<p></p></td>
</tr>
</tbody>
</table>



### <a name="span-idaccessingoutsidenetworkresourcesspanspan-idaccessingoutsidenetworkresourcesspanaccessing-outside-network-resources"></a><span id="accessing_outside_network_resources"></span><span id="ACCESSING_OUTSIDE_NETWORK_RESOURCES"></span>外部のネットワーク リソースにアクセスします。

SymSrv を SymProxy と組み合わせて使用すると、ときにサービスとして実行し、WinHTTP API を使用して、HTTP 接続経由でのシンボルにアクセスします。 これは、WinInet を使用して、この目的のための通常の動作とは異なります。

そのため、このサービスが外部ネットワーク リソースにアクセスできるように HTTP プロキシ設定を設定する必要があります。 これらの設定を構成するのにには、次のメソッドのいずれかを使用します。

-   Netsh ツール (netsh.exe) を使用します。 手順については、コマンド プロンプト ウィンドウで、次を入力します。

    ```console
    netsh winhttp -? 
    ```

SymProxy の既定の動作では、どのような HTTP プロキシが ProxyCfg または Netsh のいずれかで指定されたを使用します。 HTTP プロキシが構成されていない場合、SymProxy はダミーのプロキシを使用して、イントラネット内の HTTP サイトのセキュリティ保護にアクセスできるようにします。 、副作用としては、この手法は、SymProxy を外部のインターネットに直接接続を使用できないようにします。 インターネットへの直接接続で動作する SymProxy を許可する場合は、作成、REG\_という名前の DWORD 値**NoInternetProxy**で、**シンボル サーバーのプロキシ**レジストリのキー。 値を設定**NoInternetProxy** 1 ProxyCfg によって示される HTTP プロキシがないことを確認します。

