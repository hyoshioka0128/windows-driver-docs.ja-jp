---
title: UNC 名前付けと MUP のサポート
description: UNC 名前付けと MUP のサポート
ms.assetid: 07c4a498-10c7-41b2-aaeb-73cab946f392
keywords:
- カーネルネットワークリダイレクター WDK、UNC 名前付け
- カーネルネットワークリダイレクター WDK、MUP
- MUP WDK ネットワークリダイレクター
- 複数の UNC プロバイダー WDK ネットワークリダイレクター
- UNC WDK ネットワークリダイレクター
- WDK ファイルシステムの名前
- プレフィックス解決 WDK ネットワークリダイレクター
- プレフィックスキャッシュ WDK ネットワークリダイレクター
- シリアルプレフィックス解決 WDK ネットワークリダイレクター
- 並列プレフィックス解決 WDK ネットワークリダイレクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c17f495247d2b1d7ba8a24430ed65aa02fec246
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840960"
---
# <a name="support-for-unc-naming-and-mup"></a>UNC 名前付けと MUP のサポート


マルチ UNC プロバイダー (MUP) は、リモートファイルシステムを処理できるネットワークリダイレクター (UNC プロバイダー) に汎用名前付け規則 (UNC) 名を使用して、すべてのリモートファイルシステムアクセスを channeling するカーネルモードのコンポーネントです。要求. MUP は、コマンドラインから実行できる次の例に示すように、アプリケーションで UNC パスを使用する場合に関係します。

```cpp
notepad \\server\public\readme.txt
```

MUP は、マップされたドライブ文字 (たとえば、"NET USE" コマンド) を作成する操作中には関与しません。 この操作は、複数のプロバイダールーター (MPR) と、ネットワークリダイレクターのユーザーモード WNet プロバイダー DLL によって処理されます。 ただし、ユーザーモードの WNet プロバイダー DLL は、この操作中にカーネルモードのネットワークリダイレクタードライバーと直接通信できます。

Microsoft Windows Server 2003、Windows XP、および Windows 2000 では、分散ファイルシステム (DFS) ドライブを表していないマップされたドライブで実行されたリモートファイル操作は、MUP を経由しません。 これらの操作は、ドライブ文字のマッピングを処理したネットワークプロバイダーに直接送られます。

Windows Vista リダイレクターモデルに準拠するネットワークリダイレクターの場合は、マップされたネットワークドライブが使用されている場合でも、MUP が関係します。 マップされたドライブで実行されるファイル操作は、MUP 経由でネットワークリダイレクターに送られます。 この場合、MUP は、関係するネットワークリダイレクターに操作を渡すだけです。

MUP は、mup.sys バイナリに含まれてい*ます。* これには、windows Server 2003、windows XP、および windows 2000 の Microsoft DFS クライアントも含まれています。

通常、カーネルネットワークリダイレクターは、リモートリソースへの接続の確立 (たとえば、リモートリソースへのドライブ文字のマッピング) をサポートするために、ユーザーモードの WNet プロバイダー DLL も備えています。 MPR は、WNet プロバイダーに対するクエリに基づいてネットワーク接続を確立するユーザーモードの DLL です。 MPR を呼び出すと、次のいずれかの結果が得られます。

コマンドプロンプトから発行された "net use x: \\\\server\\share" コマンド。

Windows エクスプローラーから確立されたネットワークドライブ文字接続

WNet 関数を直接呼び出します。

ネットワークリダイレクターは、UNC 名を処理するために、MUP に登録する必要があります。 MUP に登録されている複数の UNC プロバイダーを使用できます。 これらの UNC プロバイダーは、次の1つまたは複数にすることができます。

-   RDBSS に基づくネットワークミニリダイレクター

-   RDBSS に基づいていない従来のリダイレクター

MUP は、名前ベースの操作で UNC パスを処理できるプロバイダーを決定します。通常は、IRP\_MJ\_CREATE 要求です。 これは "プレフィックス解決" と呼ばれます。 Windows Vista より前の場合、プレフィックス解決操作は次の2つの目的で機能します。

-   プレフィックス解決が発生した名前ベースの操作は、プレフィックスを要求するプロバイダーにルーティングされます。 成功した場合、MUP は、後続のハンドルベースの操作 (IRP\_MJ\_READ および IRP\_MJ\_書き込みなど) が、MUP を完全にバイパスする同じプロバイダーにアクセスすることを保証します。

-   プロバイダーと要求されたプレフィックスは、MUP によって管理されるプレフィックスキャッシュに入力されます。 その後の名前ベースの操作では、このプレフィックスキャッシュを使用して、プロバイダーがプレフィックスの解決を試行する前に既にプレフィックスを要求しているかどうかを判断します。 このプレフィックスキャッシュ内の各エントリは、キャッシュに追加されると、タイムアウト (TTL) が適用されます。 このタイムアウトが経過した後、エントリがスローされます。この時点で、MUP は、後続の名前ベースの操作で、このプレフィックスに対してもう一度プレフィックスの解決を実行します。

MUP に登録されているネットワークリダイレクターに対して、 [**IOCTL\_REDIR\_クエリ\_パス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ni-ntifs-ioctl_redir_query_path)要求を発行して、プレフィックスの解決を実行します。 IOCTL\_REDIR\_クエリ\_パスの入力バッファーと出力バッファーは次のとおりです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">パラメーターはで使用できます。</th>
<th align="left">データ構造の形式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>入力バッファー</strong></p></td>
<td align="left"><p>IrpSp-&gt; Parameters. DeviceIoControl. Type3InputBuffer</p></td>
<td align="left"><p>QUERY_PATH_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>出力バッファー</strong></p></td>
<td align="left"><p>IRP-&gt;UserBuffer</p></td>
<td align="left"><p>QUERY_PATH_RESPONSE</p></td>
</tr>
</tbody>
</table>



IOCTL とデータ構造は、 *ntifs*で定義されています。 バッファーは、非ページプールから割り当てられます。

ネットワークリダイレクターは、IRP 構造体の**RequesterMode**メンバーが**kernelmode で**であることを確認することで、この IOCTL のカーネルモードの送信を許可する必要があります。

MUP では、クエリ\_パス\_要求のデータ構造を使用して要求情報を参照します。

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
<th align="left">構造体メンバー</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>PathNameLength</strong></p></td>
<td align="left"><p><strong>Filepathname</strong>メンバーに格納されている Unicode 文字列の長さ (バイト単位)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SecurityContext</strong></p></td>
<td align="left"><p>セキュリティコンテキストへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FilePathName</strong></p></td>
<td align="left"><p>&lt;server&gt;&lt;&gt;&lt;パス&gt;の形式の NULL で終わる NULL 以外の Unicode 文字列。 文字列の長さ (バイト単位) は、 <strong>PathNameLength</strong>メンバーによって指定されます。</p></td>
</tr>
</tbody>
</table>



UNC プロバイダーでは、クエリ\_パス\_応答データ構造を使用して応答情報を提供する必要があります。

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
<th align="left">構造体メンバー</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>許容される長さ</strong></p></td>
<td align="left"><p>QUERY_PATH_REQUEST 構造体の<strong>Filepathname</strong>メンバーで指定された Unicode 文字列パスからプロバイダーによって要求されたプレフィックスの長さ (バイト単位)。</p></td>
</tr>
</tbody>
</table>



IOCTL\_REDIR\_クエリ\_パスは、IOCTL ではない\_メソッドであることに注意してください。 これは、入力バッファーと出力バッファーが同じアドレスにない可能性があることを意味します。 UNC プロバイダーでよくある間違いは、入力バッファーと出力バッファーが同じであると想定し、入力バッファーポインターを使用して応答を提供することです。

UNC プロバイダーが IOCTL\_REDIR\_QUERY\_PATH 要求を受信すると、クエリの**Filepathname**メンバーに指定されている unc パスを処理できるかどうかを判断する必要があります\_パス\_要求構造です。 その場合は、\_\_クエリの**許容**される長さのメンバーを、要求されたプレフィックスの長さ (バイト単位) で更新し、状態\_成功を持つ IRP を完了する必要があります。 プロバイダーは、指定された UNC パスを処理できない場合、IOCTL\_REDIR\_クエリ\_パス要求を適切な NTSTATUS エラーコードで失敗させる必要があります。また、クエリ\_パスの許容される**長さ**のメンバーを更新することはできません\_応答構造体。 プロバイダーは、他のメンバー、または任意の条件下で**Filepathname**文字列を変更することはできません。

\\サーバー\\共有プレフィックス名 \\が、UNC 名を使用する IRP\_MJ\_作成またはその他の Irp に応答して認識されない場合は、次のいずれかの方法で返すことをお勧めします。:

<span id="STATUS_BAD_NETWORK_PATH"></span><span id="status_bad_network_path"></span>状態\_無効\_ネットワーク\_パス  
ネットワークパスが見つかりません。 コンピューター名 (\\\\サーバーなど) が無効であるか、ネットワークリダイレクターがコンピューター名を解決できません (名前解決メカニズムが使用可能な場合)。

<span id="STATUS_BAD_NETWORK_NAME"></span><span id="status_bad_network_name"></span>状態\_無効\_ネットワーク\_名  
指定された共有名がリモートサーバーで見つかりません。 コンピューター名 (\\\\サーバーなど) は有効ですが、指定された共有名がリモートサーバーで見つかりません。

<span id="STATUS_INSUFFICIENT_RESOURCES"></span><span id="status_insufficient_resources"></span>状態\_\_リソースが不足しています  
バッファーにメモリを割り当てるために使用できるリソースが不足しています。

<span id="STATUS_INVALID_DEVICE_REQUEST"></span><span id="status_invalid_device_request"></span>デバイス\_要求\_状態\_無効です  
IOCTL\_REDIR\_クエリ\_パス要求は、MUP からのものである必要があります。 IRP のリクエスターモードは常に**kernelmode で**にする必要があります。 このエラーコードは、呼び出し元のスレッドのリクエスターモードが**kernelmode で**れなかった場合に返されます。

<span id="STATUS_INVALID_PARAMETER"></span><span id="status_invalid_parameter"></span>状態\_無効\_パラメーター  
クエリ\_パス\_要求構造の**PathNameLength**メンバーが、unicode 文字列で許容される最大長 (UNICODE\_文字列\_最大\_バイト) を超えています。

<span id="STATUS_LOGON_FAILURE_or_STATUS_ACCESS_DENIED"></span><span id="status_logon_failure_or_status_access_denied"></span><span id="STATUS_LOGON_FAILURE_OR_STATUS_ACCESS_DENIED"></span>ステータス\_ログオン\_失敗または状態\_アクセス\_拒否されました  
無効または正しくない資格情報が原因でプレフィックス解決操作が失敗した場合、プロバイダーはリモートサーバーから返された正確なエラーコードを返す必要があります。これらのエラーコードを状態に変換することはできません\_無効\_ネットワーク\_の名前または状態\_正しくない\_ネットワーク\_パスです。 ステータス\_ログオン\_の失敗や状態などのエラーコードは、適切な資格情報を使用する必要があることを示すフィードバックメカニズムとして機能\_アクセス\_拒否されます。 これらのエラーコードは、ユーザーに資格情報の入力を自動的に求める場合にも使用されます。 これらのエラーコードがないと、コンピューターにアクセスできないことをユーザーが想定している可能性があります。

ネットワークリダイレクターがプレフィックスを解決できない場合は、前述の推奨される NTSTATUS コードの一覧とは、意図したセマンティクスに厳密に一致する NTSTATUS コードを返す必要があります。 ネットワークリダイレクターでは、実際に発生したエラーを返すことはできません (状態\_接続\_拒否されています。たとえば、NTSTATUS コードが上記の一覧にない場合)。

プロバイダーによって要求されたプレフィックスの長さは、個々の UNC プロバイダーによって異なります。 ほとんどのプロバイダーは通常、\\\\&lt;servername&gt;\\&lt;sharename &gt; フォームのパスの一部 \\\\&lt;servername&gt;\\&lt;sharename を要求します。&lt;パス&gt;を&gt;\\。 たとえば、\\server\\public\\dir1\\dir2 というパス \\\\server\\public\\に指定されている場合、プロバイダーが\\server\\public の \\を要求した場合、そのプレフィックスに対する名前ベースのすべての操作は serverプレフィックスはプレフィックスキャッシュに既に存在しているため、public (\\server\\public\\file1 など) は、プレフィックスを解決せずに、そのプロバイダーに自動的にルーティングされます。 ただし、プレフィックス \\server\\マーケティング\\プレゼンテーションを含むパスは、プレフィックスの解決を行います。

ネットワークリダイレクターがサーバー名 (\\\\サーバーなど) を要求した場合、このサーバー上の共有に対するすべての要求は、このネットワークリダイレクターに送られます。 この動作は、同じサーバー上で別のネットワークリダイレクターによってアクセスされる可能性がない場合にのみ許容されます。 たとえば、UNC パスの \\\\サーバーを要求しているネットワークリダイレクターは、他のネットワークリダイレクターによるこのサーバー上の他の共有へのアクセスを禁止します (WebDAV は \\\\server\\web にアクセスします)。

[**FsrtlregisterRDBSS プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncprovider)を呼び出すことによって、REDIR プロバイダーとして登録されている従来のネットワークリダイレクターは、のクエリ\_パス要求で IOCTL\_\_を受け取ります。

UNC プロバイダーとしてのサポートを示すネットワークミニリダイレクターは、このプレフィックス要求を、IRP\_MJ\_CREATE 呼び出しとして受信します。 この作成要求は、ファイル\_作成\_ツリー\_接続フラグが設定されたユーザーモードの**Createfile**呼び出しに似ています。 ネットワークミニリダイレクターは、 [**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](https://msdn.microsoft.com/library/windows/hardware/ff550715)の呼び出しとしてプレフィックス要求を受け取りません。 プレフィックス要求の場合、RDBSS は[**MRxCreateSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)要求をネットワークミニリダイレクターに送信し、その後に[**MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)と[**MRxCreateVNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root)を呼び出します。 ネットワークミニリダイレクターが RDBSS に登録すると、ネットワークミニリダイレクターのドライバーディスパッチテーブルが RDBSS によってコピーされ、内部 RDBSS エントリポイントをポイントします。 RDBSS は、この IOCTL\_REDIR\_クエリ\_パスをネットワークミニリダイレクターの内部で受信し、 **MRxCreateSrvCall**、 **MRxSrvCallWinnerNotify**、および**MRxCreateVNetRoot**を呼び出します。 元の IOCTL\_REDIR\_クエリ\_パス IRP は、 **MRxCreateSrvCall**ルーチンに渡される RX\_CONTEXT 構造に含まれます。 また、 **MRxCreateSrvCall**に渡される RX\_コンテキストの次のメンバーが変更されます:

元の IRP が IRP\_MJ\_デバイス\_コントロールでも、 **MajorFunction**メンバーは IRP\_MJ\_CREATE に設定されます。

**SuppliedPathName**メンバーは、クエリ\_パス\_要求構造の**filepathname**メンバーに設定されます。

**SuppliedPathName**メンバーは、クエリ\_パス\_要求構造の**PathNameLength**メンバーに設定されます。

**SecurityContext**メンバーは、クエリ\_パス\_要求構造の**SecurityContext**メンバーに設定されます。

**ThisIsATreeConnectOpen**メンバーは**TRUE**に設定されます。

**Create. Flags**メンバーには、RX\_コンテキスト\_作成\_フラグ\_UNC\_名前ビットセットがあります。

ネットワークミニリダイレクターがプレフィックス要求の詳細を表示する必要がある場合は、 **MRxCreateSrvCall**に渡される RX\_コンテキストでこれらのメンバーを読み取ることができます。 それ以外の場合は、サーバー共有への接続を試行するだけで、 **MRxCreateSrvCall**の呼び出しが成功した場合には状態\_SUCCESS を返すことができます。 RDBSS は、ネットワークミニリダイレクターに代わってプレフィックス要求を行います。

ネットワークミニリダイレクターがこの IOCTL を直接受信できるケースが1つあります。 ネットワークミニリダイレクターは、RDBSS を初期化して登録する前に、ドライバーディスパッチテーブルのコピーを保存できます。 [**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)を呼び出して RDBSS に登録すると、ネットワークミニリダイレクターは、RDBSS によってインストールされた新しいドライバーディスパッチテーブルのエントリポイントのコピーを保存し、元のドライバーディスパッチテーブルを復元できます。 復元されたドライバーディスパッチテーブルを変更する必要があります。これにより、受信した IRP がネットワークミニリダイレクターに関連するものであることを確認した後、その呼び出しは RDBSS ドライバーのディスパッチエントリポイントに転送されるようになります。 ドライバーが RDBSS を初期化して**RxRegisterMinrdr**を呼び出すと、RDBSS はネットワークミニリダイレクターのドライバーディスパッチテーブルをコピーします。 Rdbsslib にリンクするネットワークミニリダイレクターは、 [**RxDriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry)を**driverentry**ルーチンから呼び出して RDBSS スタティックライブラリを初期化し、そのドライバーを復元する前に、元のドライバーディスパッチテーブルを保存する必要があり*ます。* **RxRegisterMinrdr**を呼び出した後のディスパッチテーブル。 これは、RDBSS が**RxDriverEntry**ルーチンと**RxRegisterMinrdr**ルーチンの両方でネットワークミニリダイレクターディスパッチテーブルを介してコピーされるためです。

プレフィックスの解決中にプロバイダーが照会される順序は、次のキーの下に格納されている REG\_SZ ProviderOrder レジストリ値によって制御されます。

```cpp
HKLM\System\CurrentControlSet\Control\NetworkProvider\Order
```

ProviderOrder レジストリ値内の個々のプロバイダー名は、先頭または末尾の空白を除いてコンマで区切られます。

たとえば、次の値に文字列を含めることができます。

```cpp
RDPNP,LanmanWorkstation,WebClient
```

UNC パスが指定されている場合、\\&lt;サーバー&gt;\\&lt;共有&gt;\\&lt;&gt;\\\\、\\@no__t_ サーバーでプレフィックス解決要求を発行します。たとえば、12_ share または \\\\server など) が、MUP プレフィックスキャッシュに見つかりません。 MUP は、プロバイダーがプレフィックスを要求する (またはすべてのプロバイダーがクエリされた) まで、プレフィックス解決要求を各プロバイダーに送信します。

1.  TS クライアント (RDPNP)

2.  SMB リダイレクター (LanmanWorkstation)

3.  WebDAV リダイレクター (WebClient)

ProviderOrder レジストリ値を変更すると、Windows Server 2003、Windows XP、および Windows 2000 の MUP で再起動が有効になります。

MUP では、一覧に示されている各プロバイダー名を使用して、次のレジストリキーでプロバイダーのレジストリキーを検索します。

```cpp
HKLM\System\CurrentControlSet\Services\<ProviderName>
```

次に、NetworkProvider サブキーの DeviceName 値を読み取って、プロバイダーが登録するデバイス名を見つけます。 プロバイダーによって実際に登録されると、MUP は、に渡されたデバイス名と既知のプロバイダーのデバイス名のリストを照合し、プレフィックスの解決のためにプロバイダーを順序付きリストに配置します。 この一覧に表示されるプロバイダーの順序は、前に説明した ProviderOrder レジストリ値に指定されている順序に基づいています。

このプロバイダーの順序は、複数のプロバイダールーター (MPR) にも適用されることに注意してください。これは、WNet プロバイダーに対するクエリに基づいてネットワーク接続を確立するユーザーモード DLL です。

Windows Server 2003 Service Pack 1 および Windows XP Service Pack 2 より前の場合、MUP 動作では、ProviderOrder レジストリ値で指定された順序ですべてのプロバイダーに対して "並列" でプレフィックス解決要求を発行し、すべてのプロバイダーを待機していました。を実行して、プレフィックス解決操作を完了します。 したがって、最初のプロバイダーがプリフィックスを要求した場合でも、その他のすべてのプロバイダーがプレフィックス解決操作を完了するまで、MUP は待機します。 複数のプロバイダーがプレフィックス要求で応答する場合、MUP は ProviderOrder レジストリ値に指定されている順序に基づいてプロバイダーを選択します。

Windows XP Service Pack 2 以降、および Windows Server 2003 Service Pack 1 以降では、この動作は少し変更されました。 MUP は、プレフィックス解決要求を直列に発行し、最初のプロバイダーがプレフィックスを要求するとすぐに停止します。 したがって、上記の例では、RDPNP がプレフィックスを要求した場合、MUP は SMB または WebDAV のリダイレクターを呼び出しません。

この動作が変更された主な理由は、"シリアルプレフィックスの解像度" スキームによって、ProviderOrder 値の優先順位が低いネットワークリダイレクターのケースにより、ProviderOrder 値。 たとえば、ファイアウォールが設定されたリモートサーバーで、特定の種類の TCP/IP パケット (HTTP へのアクセスなど) をブロックし、他のユーザー (SMB アクセスなど) を許可するように構成されているとします。 この場合、SMB ネットワークリダイレクターが ProviderOrder 値の最初のプロバイダーとして構成されていて、そのプレフィックスを迅速に要求しても、WebDAV リダイレクターは、への TCP 接続を待機することにより、プレフィックスの解決の完了を大幅に遅延する可能性があります。タイムアウト.








