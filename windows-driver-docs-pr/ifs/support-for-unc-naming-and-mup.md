---
title: UNC 名前付けと MUP のサポート
description: UNC 名前付けと MUP のサポート
ms.assetid: 07c4a498-10c7-41b2-aaeb-73cab946f392
keywords:
- カーネル ネットワーク リダイレクター WDK、UNC 名
- カーネル ネットワーク リダイレクター WDK、MUP
- MUP WDK ネットワーク リダイレクター
- 複数 UNC プロバイダー WDK ネットワーク リダイレクター
- UNC WDK ネットワーク リダイレクター
- WDK の名前のファイル システム
- プレフィックス解決の WDK ネットワーク リダイレクター
- プレフィックス キャッシュ WDK ネットワーク リダイレクター
- シリアル プレフィックス解決の WDK ネットワーク リダイレクター
- 並列プレフィックス解決の WDK ネットワーク リダイレクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d471ede1543438093cad0cb61592d8c9b502d8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570124"
---
# <a name="support-for-unc-naming-and-mup"></a>UNC 名前付けと MUP のサポート


複数 UNC プロバイダー (MUP) は、チャネル接続のすべてのリモート ファイル システムでは、リモート ファイル システムを処理できるネットワーク リダイレクター (UNC プロバイダー) への汎用名前付け規則 (UNC) 名を使用してアクセスする責任を負いますカーネル モード コンポーネント要求します。 コマンドラインから実行する次の例に示すように、UNC パスが、アプリケーションで使用されるときに MUP が含まれます。

```cpp
notepad \\server\public\readme.txt
```

MUP がマップされたドライブ文字 ("NET 使用"コマンドなど) を作成する操作中に関与しません。 この操作は、ネットワーク リダイレクターのプロバイダーの複数のルーター (MPR) とユーザー モード WNet プロバイダー DLL によって処理されます。 ただし、ユーザー モード WNet プロバイダー DLL は、この操作中に、カーネル モードのネットワーク リダイレクター ドライバーと直接通信することができます。

Microsoft Windows Server 2003、Windows XP、および Windows 2000 では、分散ファイル システム (DFS) ドライブを表していないあるマップされたドライブに対して実行されるリモート ファイルの操作は MUP を経由しません。 これらの操作は、ドライブ文字のマッピングを処理するネットワーク プロバイダーに直接移動します。

Windows Vista リダイレクター モデルに準拠するネットワーク リダイレクター、マップ済みネットワーク ドライブを使用する場合でも、MUP が関係します。 マップされたドライブで実行されるファイルの操作は、MUP ネットワーク リダイレクターを経由します。 ここで MUP 単に渡すこと操作ネットワーク リダイレクターに関連する注意してください。

MUP の一部である、 *mup.sys*バイナリは、Windows Server 2003、Windows XP、および Windows 2000 で Microsoft DFS クライアントも含まれています。

カーネルのネットワーク リダイレクターが通常ユーザー モード WNet プロバイダー (ドライブ文字にマップ、リモート リソースなど)、リモート リソースへの接続の確立をサポートするために DLL があることもできます。 MPR は、ユーザー モード DLL WNet プロバイダーへのクエリに基づくネットワーク接続を確立します。 MPR の呼び出し結果から、次のいずれかになります。

A"net を使用して、x: \\ \\server\\共有"コマンドがコマンド プロンプトから実行します。

Windows エクスプ ローラーから確立されているネットワーク ドライブ文字を接続

WNet 関数への直接の呼び出し。

ネットワーク リダイレクターは、UNC 名を処理する MUP を登録する必要があります。 複数 UNC プロバイダーが MUP に登録されていることができます。 これらの UNC プロバイダーには、次の 1 つ以上ができます。

-   RDBSS に基づいてネットワーク ミニ リダイレクター

-   RDBSS に基づいていないレガシ リダイレクター

MUP を決定するプロバイダーは IRP では通常に名前ベースの操作の UNC パスを処理できる\_MJ\_要求の作成。 これを「プレフィックスの解決策」と呼びます Windows Vista では、前に、プレフィックスの解決操作には 2 つの目的があります。

-   プレフィックスの解決では、名前に基づく操作は、プレフィックスを要求プロバイダーにルーティングされます。 かどうかは成功すると、MUP により、後続ハンドル ベースの操作 (IRP\_MJ\_読み取りおよび IRP\_MJ\_を記述) MUP を完全にバイパス同じプロバイダーに移動します。

-   プロバイダーと主張した場合、プレフィックスは、MUP によって保持されるプレフィックスのキャッシュに入力されます。 残りの名前ベースの操作は、MUP は、決定かどうか、プロバイダーは既に要求プレフィックスのプレフィックスの解決を実行するのに前にこのプレフィックス キャッシュを使用します。 このプレフィックスのキャッシュ内の各エントリは、("TTL"と呼ばれます)、タイムアウトの対象とキャッシュに追加されます。 このタイムアウトの期限が切れた後に、エントリを破棄は、どの時点で MUP しますプレフィックス解決もう一度その後の名前に基づく操作では、このプレフィックスの。

プレフィックスの解決を発行して実行して MUP、 [ **IOCTL\_REDIR\_クエリ\_パス**](https://msdn.microsoft.com/library/windows/hardware/ff548313) MUP に登録されているネットワーク リダイレクターを要求します。 IOCTL の入力と出力バッファー\_REDIR\_クエリ\_パスは、次のとおり。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">パラメーターでご利用いただけます</th>
<th align="left">データ構造の形式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>入力バッファー</strong></p></td>
<td align="left"><p>IrpSp-&gt; Parameters.DeviceIoControl.Type3InputBuffer</p></td>
<td align="left"><p>QUERY_PATH_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>出力バッファー</strong></p></td>
<td align="left"><p>IRP-&gt;UserBuffer</p></td>
<td align="left"><p>QUERY_PATH_RESPONSE</p></td>
</tr>
</tbody>
</table>



IOCTL とデータ構造で定義されます*ntifs.h*します。 バッファーは、非ページ プールから割り当てられます。

ネットワーク リダイレクター: ことを確認して、この IOCTL の送信者をカーネル モードのみを許可する必要があります、 **RequesterMode** IRP 構造体のメンバーは**kernelmode である**します。

MUP は、クエリを使用して\_パス\_要求については、要求データの構造体。

```cpp
typedef struct _QUERY_PATH_REQUEST {
    ULONG                PathNameLength;
    PIO_SECURITY_CONTEXT SecurityContext;
    WCHAR                FilePathName[1];
} QUERY_PATH_REQUEST, *PQUERY_PATH_REQUEST;
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>PathNameLength</strong></p></td>
<td align="left"><p>含まれる Unicode 文字列の長さをバイト単位で、 <strong>FilePathName</strong>メンバー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SecurityContext</strong></p></td>
<td align="left"><p>セキュリティ コンテキストへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FilePathName</strong></p></td>
<td align="left"><p>NULL 以外で終わる、フォームの Unicode 文字列&amp;lt; server&gt;&amp;lt; 共有&gt;&amp;lt; パス&gt;します。 (バイト単位)、文字列の長さがで指定された、 <strong>PathNameLength</strong>メンバー。</p></td>
</tr>
</tbody>
</table>



UNC プロバイダーは、クエリを使用する必要があります\_パス\_応答情報の応答データの構造体。

```cpp
typedef struct _QUERY_PATH_RESPONSE {
    ULONG  LengthAccepted;
} QUERY_PATH_RESPONSE, *PQUERY_PATH_RESPONSE;
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>LengthAccepted</strong></p></td>
<td align="left"><p>指定された Unicode 文字列のパスから、プロバイダーによって要求されたプレフィックスの長さ、(バイト単位)、 <strong>FilePathName</strong> QUERY_PATH_REQUEST 構造体のメンバー。</p></td>
</tr>
</tbody>
</table>



注その IOCTL\_REDIR\_クエリ\_パスは、メソッド\_も IOCTL します。 これは、同じアドレスに入力と出力バッファーが存在しないことを意味します。 UNC プロバイダーでよくある間違いでは、入力バッファーと出力バッファーは同じであり、入力バッファーのポインターを使用して、応答を提供することを前提としています。

UNC プロバイダーが、IOCTL を受信すると\_REDIR\_クエリ\_パスが要求で指定された UNC パスを処理できるかどうかを判断する必要がある、 **FilePathName**クエリのメンバー\_パス\_要求の構造。 更新する必要があるため場合、 **LengthAccepted** 、クエリのメンバー\_パス\_(バイト単位) は要求し、ステータスの IRP の完了にプレフィックスの長さと応答の構造\_成功しました。 プロバイダーは、指定した UNC パスを処理できない場合は、IOCTL が失敗する必要があります\_REDIR\_クエリ\_パスで NTSTATUS の適切なエラー コードの要求、更新する必要があります、 **LengthAccepted**クエリのメンバー\_パス\_応答の構造。 プロバイダーは変更しないで、その他のメンバーのいずれかまたは**FilePathName**いずれかの条件下での文字列。

場合、 \\ \\server\\IRP への応答で共有プレフィックス名が認識されない\_MJ\_作成、またはその他の Irp UNC 名では、返されることをお勧めの NTSTATUS コードを使用しているが、次のいずれか。

<span id="STATUS_BAD_NETWORK_PATH"></span><span id="status_bad_network_path"></span>ステータス\_不良\_ネットワーク\_パス  
ネットワーク パスが見つかりません。 コンピューター名 (\\\\サーバーなど) が無効ですか、ネットワーク リダイレクター (を使用してどのような名前解決メカニズムが使用可能な) コンピューター名を解決できません。

<span id="STATUS_BAD_NETWORK_NAME"></span><span id="status_bad_network_name"></span>ステータス\_不良\_ネットワーク\_名  
指定した共有名は、リモート サーバーで見つかりません。 コンピューター名 (\\\\サーバーなど) が有効ですが、指定した共有名がリモート サーバー上に見つかりません。

<span id="STATUS_INSUFFICIENT_RESOURCES"></span><span id="status_insufficient_resources"></span>ステータス\_不十分\_リソース  
バッファーのメモリを割り当てることができるリソースの不足が発生しました。

<span id="STATUS_INVALID_DEVICE_REQUEST"></span><span id="status_invalid_device_request"></span>ステータス\_無効な\_デバイス\_要求  
IOCTL\_REDIR\_クエリ\_パスの要求が MUP から取得する必要がありますのみと IRP の要求元のモードでは常に**kernelmode である**します。 呼び出し元のスレッドの要求元のモードがない場合、このエラー コードが返される**kernelmode である**します。

<span id="STATUS_INVALID_PARAMETER"></span><span id="status_invalid_parameter"></span>ステータス\_無効な\_パラメーター  
**PathNameLength** 、クエリでメンバー\_パス\_構造が許容される最大の長 UNICODE を超える要求\_文字列\_最大\_Unicode のバイト数文字列。

<span id="STATUS_LOGON_FAILURE_or_STATUS_ACCESS_DENIED"></span><span id="status_logon_failure_or_status_access_denied"></span><span id="STATUS_LOGON_FAILURE_OR_STATUS_ACCESS_DENIED"></span>ステータス\_ログオン\_エラーまたは状態\_アクセス\_が拒否されました  
無効なまたは正しくない資格情報のためのプレフィックスの解決操作に失敗した場合、プロバイダーは、リモート サーバーによって返される正確なエラー コードを返す必要があります。これらのエラー コードは、状態に変換できないする必要があります\_不良\_ネットワーク\_名前または状態\_不適切な\_ネットワーク\_パス。 エラー コードなどの状態\_ログオン\_障害と状態\_アクセス\_適切な資格情報を使用するという要件を示す、ユーザーにフィードバック メカニズムとしてが拒否されました。 これらのエラー コードは、資格情報を自動的にユーザー入力を求めるは、状況にも使用されます。 これらのエラー コードがないユーザーは可能性があります、マシンがアクセスできないことをとします。

ネットワーク リダイレクターがプレフィックスを解決できない場合に推奨される NTSTATUS コードの上記のリストから目的のセマンティクスに近い NTSTATUS コードを返す必要があります。 ネットワーク リダイレクターは戻り実際のエラーが発生しました (ステータス\_接続\_拒否されると、たとえば) MUP NTSTATUS コードは上記の一覧にない場合に直接します。

プロバイダーが要求したプレフィックスの長さは、個々 の UNC プロバイダーに依存します。 ほとんどのプロバイダーは通常、要求、 \\ \\ &lt;servername&gt;\\&lt;sharename&gt;形式のパスの一部\\ \\ &lt;servername&gt;\\&lt;sharename&gt;\\&lt;パス&gt;します。 たとえば、プロバイダーが要求\\\\サーバー\\、パスが指定されたパブリック\\\\サーバー\\パブリック\\dir1\\ディレクトリ 2 のすべての名前に基づく操作、プレフィックス\\ \\server\\パブリック (\\server\\パブリック\\例については、ファイル 1) 以降の任意のプレフィックス解決なしに自動的にそのプロバイダーにルーティングされます、プレフィックスは、既にプレフィックス キャッシュされています。 ただし、プレフィックスを持つパス\\サーバー\\マーケティング\\プレゼンテーションがプレフィックス解決経由します。

ネットワーク リダイレクター サーバー名を要求する場合 (\\\\サーバーなど)、このサーバー上の共有に対するすべての要求はこのネットワーク リダイレクターに移動します。 この動作は、許容されるは、別のネットワーク リダイレクターでアクセスされている同じサーバー上の別の共有の可能性がない場合のみ。 たとえば、ネットワーク リダイレクターと主張して\\ \\UNC パスのサーバーがこのサーバー上の他の共有には、その他のネットワーク リダイレクターによるアクセスを防ぐため (へのアクセスを WebDAV \\\\サーバー\\web、).

レガシ ネットワーク リダイレクター (RDBSS を使用するのには基づいていない) を呼び出して MUP の UNC プロバイダーとして登録する[ **FsRtlRegisterUncProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff547178) IOCTL 受け取ります\_REDIR\_クエリ\_パス要求。

A ネットワーク UNC プロバイダーはこのプレフィックスの要求を受信は IRP の場合と同様のサポートを示すミニ リダイレクター\_MJ\_作成の呼び出し。 この要求の作成はユーザー モードに似ています**Createfile**ファイルを使用して呼び出す\_作成\_ツリー\_接続フラグを設定します。 ネットワークのミニ リダイレクターの呼び出しとプレフィックスの要求を受信しません[ **MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]**](https://msdn.microsoft.com/library/windows/hardware/ff550715)します。 RDBSS プレフィックスのクレームの送信、 [ **MRxCreateSrvCall** ](https://msdn.microsoft.com/library/windows/hardware/ff549864)要求への呼び出し後にネットワーク ミニリダイレクター [ **MRxSrvCallWinnerNotify**](https://msdn.microsoft.com/library/windows/hardware/ff550824)と[ **MRxCreateVNetRoot**](https://msdn.microsoft.com/library/windows/hardware/ff549869)します。 ネットワークのミニ リダイレクター登録される RDBSS と、キー RDBSS 内部 RDBSS エントリ ポイントをポイントする場所を空けるのネットワークのミニ リダイレクター ドライバー ディスパッチ テーブルがコピーされます。 この IOCTL 受信 RDBSS\_REDIR\_クエリ\_ネットワーク ミニリダイレクターと呼び出しの内部パス**MRxCreateSrvCall**、 **MRxSrvCallWinnerNotify**、および**MRxCreateVNetRoot**します。 元の IOCTL\_REDIR\_クエリ\_RX に含まれるパス IRP\_に渡されるコンテキストの構造、 **MRxCreateSrvCall**ルーチン。 さらに、次のメンバー、RX で\_に渡されるコンテキスト**MRxCreateSrvCall**が変更されます。

**MajorFunction** IRP にメンバーが設定されている\_MJ\_作成元の IRP が IRP も\_MJ\_デバイス\_コントロール。

**PrefixClaim.SuppliedPathName.Buffer**にメンバーが設定されている、 **FilePathName** 、クエリのメンバー\_パス\_要求の構造。

**PrefixClaim.SuppliedPathName.Length**にメンバーが設定されている、 **PathNameLength** 、クエリのメンバー\_パス\_要求の構造。

**Create.NtCreateParameters.SecurityContext**にメンバーが設定されている、 **SecurityContext** 、クエリのメンバー\_パス\_要求の構造。

**Create.ThisIsATreeConnectOpen**に設定されているメンバー **TRUE**します。

**Create.Flags**メンバーには、RX\_コンテキスト\_作成\_フラグ\_UNC\_名ビットが設定されます。

RX でこれらのメンバーを読み取ることができるプレフィックスの要求の詳細を表示する場合、ネットワーク ミニリダイレクター\_に渡されるコンテキスト**MRxCreateSrvCall**します。 それ以外の場合、サーバー共有に接続して状態を返す試みることができますのみ\_成功した場合、 **MRxCreateSrvCall**呼び出しに成功しました。 RDBSS はミニ リダイレクターにに代わってネットワーク要求のプレフィックスになります。

ネットワークのミニ リダイレクターがでしたこの IOCTL を直接受信する 1 つのケースがあります。 ネットワークのミニ リダイレクターは、の初期化と RDBSS を登録する前にそのドライバー ディスパッチ テーブルのコピーを保存する可能性があります。 呼び出した後[ **RxRegisterMinirdr** ](https://msdn.microsoft.com/library/windows/hardware/ff554693) RDBSS に登録するネットワーク ミニリダイレクターでした、新しいドライバー ディスパッチ テーブル エントリ ポイント RDBSS によってインストールのコピーを保存し、その元のドライバーを復元ディスパッチ テーブルです。 復元されたドライバーのディスパッチ テーブルは、ネットワークのミニ リダイレクターに関心のあるものの受信の IRP をオンにした後、呼び出しは RDBSS ドライバーのディスパッチのエントリ ポイントに転送されるように変更する必要があります。 ドライバーは、RDBSS と呼び出しを初期化します。 ときに、ネットワークのミニ リダイレクターのドライバーのディスパッチ テーブルを介して RDBSS がコピーされます**RxRegisterMinrdr**します。 A ネットワークに対してリンク ミニ リダイレクター *rdbsslib.lib*呼び出す前に元のドライバー ディスパッチ テーブルを保存する必要があります[ **RxDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554404)そのから**DriverEntry** RDBSS スタティック ライブラリを初期化し、そのドライバー ディスパッチ テーブルを呼び出した後に復元するルーチン**RxRegisterMinrdr**します。 これは、両方のネットワークのミニ リダイレクター ディスパッチ テーブル上の RDBSS をコピーするため、 **RxDriverEntry**と**RxRegisterMinrdr**ルーチン。

プレフィックスの解決時に、プロバイダーを照会する順序は、REG によって制御されます\_SZ ProviderOrder レジストリ値が次のキーに格納されます。

```cpp
HKLM\System\CurrentControlSet\Control\NetworkProvider\Order
```

ProviderOrder のレジストリ値の個々 のプロバイダー名は、先頭または末尾の空白なしのコンマで区切られます。

たとえば、この値は、文字列を含む可能性があります。

```cpp
RDPNP,LanmanWorkstation,WebClient
```

UNC パスが指定された\\ \\&lt;サーバー&gt;\\&lt;共有&gt;\\&lt;パス&gt;MUP が場合、プレフィックス解決の要求を発行しますプレフィックス (\\\\server\\共有または\\\\サーバーなど) が MUP プレフィックスのキャッシュに見つかりません。 プロバイダーは、プレフィックスを要求するまで MUP に次の順序で各プロバイダーにプレフィックス解決の要求が送信します (またはすべてのプロバイダーのクエリが実行されています)。

1.  ターミナル サービス クライアント (RDPNP)

2.  SMB リダイレクター (LanmanWorkstation)

3.  WebDAV リダイレクター (WebClient)

ProviderOrder レジストリ値が変更には、Windows Server 2003、Windows XP、および Windows 2000 MUP に反映するために再起動が必要です。

MUP では、次のレジストリ キーの下で、プロバイダーのレジストリ キーを検索するには、各プロバイダー名を使用します。

```cpp
HKLM\System\CurrentControlSet\Services\<ProviderName>
```

MUP は、プロバイダーを登録するデバイス名を検索する NetworkProvider サブキーの下でデバイス名の値を読み取ります。 プロバイダーが登録では実際には、MUP が渡される既知のプロバイダーのデバイス名の一覧のデバイス名と一致し、プレフィックス解決のため、プロバイダーを順序付きリストに配置します。 この一覧でプロバイダーの順序は、前に説明した ProviderOrder レジストリ値で指定された順序に基づきます。

このプロバイダーの順序もによって、複数プロバイダーのルーター (MPR)、ユーザー モード DLL WNet プロバイダーへのクエリに基づくネットワーク接続を確立するを受け入れられることに注意してください。

Windows Server 2003 Service Pack 1 と Windows XP Service Pack 2 では、前に、MUP の動作が ProviderOrder のレジストリ値で指定された順序で"並列"内のすべてのプロバイダーにプレフィックス解決要求を発行し、すべてのプロバイダーの待機をされましたプレフィックス解決操作を完了します。 したがって、最初のプロバイダーが、プレフィックスを要求した場合でも MUP はまだプレフィックスの解決操作を完了するその他のすべてのプロバイダーで待機します。 複数のプロバイダーは、プレフィックスの要求で応答、MUP ProviderOrder レジストリ値で指定された順序に基づいてプロバイダーを選択します。

Windows XP Service Pack 2 でし、後でと Windows Server 2003 Service Pack 1 以降で、この動作が若干変更されました。 MUP では、プレフィックス解決の要求を逐次的に発行し、最初のプロバイダーは、プレフィックスを要求するとすぐを停止します。 したがって、上記の例では、RDPNP 要求プレフィックス、MUP は呼び出しません SMB または WebDAV リダイレクター。

この動作が変更された主な理由は、「シリアル プレフィックス解決」スキームをによって禁止されているネットワーク リダイレクターのケース ProviderOrder 値の優先順位の低いで優先順位の高いネットワーク リダイレクターのパフォーマンスの問題が発生しますProviderOrder 値。 たとえば、他のユーザー (たとえば SMB アクセス) を許可するが、TCP/IP パケット (へのアクセス、HTTP など) の特定の種類をブロックするように構成の場所でのファイアウォールでのリモート サーバーがあるとします。 この場合、いて SMB ネットワーク リダイレクターで ProviderOrder 値の最初のプロバイダーとして構成されている、迅速に、プレフィックスを要求して、WebDAV リダイレクターが大幅を遅らせることがプレフィックス解決の完了への TCP 接続を待機してタイムアウトになりました。








