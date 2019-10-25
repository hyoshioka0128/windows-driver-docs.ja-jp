---
title: Microsoft Windows Vista における MUP の変更点
description: Microsoft Windows Vista における MUP の変更点
ms.assetid: 8ca2f9bc-14f1-45d3-a397-f3e5459cf8ec
keywords:
- カーネルネットワークリダイレクター WDK、MUP
- MUP WDK ネットワークリダイレクター
- 複数の UNC プロバイダー WDK ネットワークリダイレクター
- UNC WDK ネットワークリダイレクター
- カーネルネットワークリダイレクター WDK、Windows Vista リダイレクターモデル
- 従来のリダイレクター WDK ファイルシステム
- プレフィックス解決 WDK ネットワークリダイレクター
- プレフィックスキャッシュ WDK ネットワークリダイレクター
- WDK ネットワークリダイレクターのダブルフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b00c81dc2705d811708d1c183bcfb04a29ca18a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841058"
---
# <a name="mup-changes-in-microsoft-windows-vista"></a>Microsoft Windows Vista における MUP の変更点


Windows Vista では、ネットワークリダイレクターに影響を与える可能性がある複数の UNC プロバイダー (MUP) に対して多数の変更が実装されています。

MUP と分散ファイルシステム (DFS) クライアントは別々のバイナリファイルにあります。 MUP コンポーネントは mup.sys にあり、DFS クライアントは dfsc にあります。 Windows Server 2003、Windows XP、および Windows 2000 では、MUP カーネルコンポーネントである mup.sys にも、DFS クライアントが含まれていました。

Windows Vista では、新しいリダイレクターモデルが定義されています。

-   MUP は、 [**IoRegisterFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfilesystem)を呼び出すことによって、i/o マネージャーを使用してファイルシステムとして登録します。

-   ネットワークリダイレクターは、Windows Vista で導入された新しいルーチンである[**Fsrtlregisteruncproviderex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)を使用して、MUP に登録します。

-   ネットワークリダイレクターは、名前のないデバイスオブジェクトを[**Fsrtlregisterfinalex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)に渡します。

-   ネットワークリダイレクターは、デバイス名を[**Fsrtlregisteruncproviderex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)に渡します。

-   ネットワークリダイレクターは、i/o マネージャーを使用してファイルシステムとして登録しません ( [**IoRegisterFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfilesystem)を呼び出すことはありません)。

-   MUP からネットワークリダイレクターへのすべての呼び出し (プレフィックス解決、Ioctl、FSCTLs を含む) は、Apc が有効になっています。 他のコンポーネントから MUP へのすべての呼び出しは、Apc が有効になっていると想定されます。 [**FsRtlCancellableWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff545738)または[**FsRtlCancellableWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff545731)で呼び出しを使用し、Windows Vista で導入された新しいルーチンがある場合、i/o 要求を発行したスレッドが末尾.

-   プレフィックスの解決は、Windows Vista で導入された新しい IOCTL である、IOCTL\_REDIR\_クエリ\_パス\_EX を使用して実行されます。

-   MUP に登録されているネットワークリダイレクターのデバイス名は、MUP デバイスオブジェクトへのシンボリックリンクになります。

Windows Vista リダイレクターモデルに準拠するネットワークリダイレクターの場合、MUP では、オブジェクトマネージャーの名前空間にシンボリックリンクを作成します。これには、 [**Fsrtlregisterの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)呼び出しでネットワークリダイレクターによって指定されたデバイス名が使用されます。 このシンボリックリンクのターゲットは、MUP デバイスオブジェクト (\\デバイス\\Mup) です。

MUP をファイルシステムとして登録し、ネットワークリダイレクターのデバイス名を、MUP デバイスオブジェクトにシンボリックリンクとして登録する利点は、名前ベースの操作だけでなく、すべてのリモートファイルシステム i/o 操作が、MUP を経由することです。 したがって、リモートファイルシステムスタックに存在する必要があるファイルシステムフィルタードライバーは、単に MUP デバイスオブジェクトにアタッチできます。 ファイルシステムフィルタードライバーは、プロバイダーのデバイスオブジェクト名 (\\デバイス\\LanmanRedirector など) をドライバーにハードコーディングする必要はありません。 これにより、ファイルシステムフィルタードライバーは、すべてのネットワークリダイレクターに発行されたすべての i/o 操作を1つの添付ファイルで監視できます。 これにより、Windows Vista より前のファイルシステムフィルタードライバーによって検出された重複 i/o 操作が回避されます。これは、DFS (mup.sys) と個々のネットワークリダイレクター (\\デバイス\\LanmanRedirector など) に個別に接続されています。i/o 操作を両方に対して監視します。

MUP デバイスオブジェクトに接続されているファイルシステムフィルタードライバーは、特定のネットワークリダイレクターに送信されるトラフィックを選択的にフィルター処理できます。 この場合、フィルタードライバーは、 [**FsRtlMupGetProviderIdFromName**](https://msdn.microsoft.com/library/windows/hardware/ff546971)ルーチンを呼び出すことによって、目的のネットワークリダイレクターのデバイス名をプロバイダー識別子にマップします。 フィルタードライバーは、特定のファイルオブジェクトのトラフィックをフィルター処理するかどうかを判断できます。そのためには、 [**FsRtlMupGetProviderInfoFromFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff546981)ルーチンの呼び出しによって取得されたプロバイダー識別子を、のプロバイダー識別子と比較します。対象のネットワークディレクター。

Windows Vista リダイレクターモデルに準拠するネットワークリダイレクターの場合:

-   リモートファイルシステムスタック上のすべてのファイルオブジェクトが、MUP に解決されます。 そのため、 [**IoGetDeviceAttachmentBaseRef**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetdeviceattachmentbaseref)は、ファイルオブジェクトを所有するネットワークリダイレクターではなく、MUP のデバイスオブジェクトを返します。 ただし、ファイルオブジェクトの内容はネットワークリダイレクターによって所有されています。

-   ネットワークリダイレクター (\\デバイス\\LanmanRedirector\\server\\share など) のデバイス名に対して発行された IRP\_MJ\_の作成は、MUP プレフィックスを経由せずに、そのネットワークリダイレクターを対象とします。解決方法は、Windows Server 2003、Windows XP、および Windows 2000 の場合とまったく同じです。

Windows Vista RDBSS (動的または静的にリンク) に基づいていないネットワークリダイレクターは、"従来のリダイレクター" と呼ばれます。 これらのレガシネットワークリダイレクターには次のものが含まれます。

-   Windows Server 2003、Windows XP、および Windows 2000 用に記述されたネットワークリダイレクターは、 [**Fsrtlregisteruncprovider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncprovider)を使用して、MUP に直接登録します。

-   Windows server 2003、windows XP、または Windows 2000 の rdbsslib ライブラリと静的にリンクする Windows Server 2003、Windows XP、および Windows 2000 用に作成されたネットワークミニリダイレクター。

-   [**Fsrtlregisterの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)登録を使用して、MUP に直接登録する Windows Vista 用に記述されたネットワークリダイレクター。

Windows Vista RDBSS (RDBSS) に動的にリンクするネットワークミニリダイレクターは、Windows Vista リダイレクターモデルに自動的に準拠します。これは、RDBSS が[*Fsrtlregister Providerex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)を使用して MUP に登録するためです。 Windows Vista RDBSS (rdbsslib) に対して静的にリンクされるネットワークミニリダイレクターは、Windows Vista リダイレクターモデルにも自動的に準拠します。これは、RDBSS が**Fsrtlregister Providerex**を使用して MUP に登録するためです。

Windows Vista 用に作成された従来のネットワークリダイレクターは、MUP に直接登録する必要があります Windows Vista リダイレクターモデルに準拠している必要があります。

Windows Server 2003、Windows XP、および Windows 2000 用に記述されたネットワークリダイレクターは、 [**Fsrtlregisterプロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncprovider)を使用して直接 MUP に登録すると、windows server 2003、windows xp、および windows 2000 で行ったのとまったく同じ方法で動作します。 Windows server 2003、windows XP、および Windows 2000 の rdbsslib ライブラリと静的にリンクする Windows Server 2003、Windows XP、および windows 2000 用に作成されたネットワークミニリダイレクターは、Windows Server 2003 とまったく同じように動作します。Windows XP および Windows 2000。 これらのレガシネットワークリダイレクターとミニリダイレクターは、次の動作を示しています。

-   ファイルシステムの登録を監視するファイルシステムフィルタードライバーに表示されます。

-   デバイスオブジェクトにはという名前が付けられます。 デバイス名はシンボリックリンクではなく、\\デバイス\\MUP を指していません。

-   ファイルオブジェクトは、ネットワークリダイレクターの名前付きデバイスオブジェクトに解決されます。

-   MUP は、プレフィックス解決操作にのみ関係します。 ネットワークプロバイダーが特定されると、状態\_再解析を返すことによって、MUP "がその方法を利用できなくなります。 後続のすべての操作は、MUP を通過しません。

この動作は、プロバイダーのデバイス名が \\デバイス\\MUP にシンボリックリンクされている場合に発生する可能性がある、ダブルフィルター処理を防ぐために保持されています。 この2つのフィルター処理は、次の理由で発生します。

-   ファイルシステムフィルタードライバーは、既に \\デバイス\\MUP にアタッチされています。

-   ファイルシステムフィルタードライバーは、登録している任意のファイルシステムにアタッチします。 名前付きデバイスオブジェクトを使用するネットワークリダイレクターは自身をファイルシステムとして登録するため、ファイルシステムフィルタードライバーは、同じ i/o を2回フィルター処理することになります。

Windows Vista での MUP との呼び出しは、Apc が有効になっているため、次のような影響があります。

-   必要に応じて、必要に応じて、適切な方法によってスレッドの中断に対して MUP から呼び出されるコードパスを保護することが重要です。特に、IOCTL\_REDIR\_クエリ\_パスハンドラーによって実行されます。 スレッドの中断は、長時間に及ぶ可能性がある "無制限の待機" 操作であることに注意してください。

-   (システムスレッドではなく) ユーザーモードスレッドに関係する "wait for i/o" 操作では、常に "キャンセル可能な wait" が使用されるようにすることが重要です。 詳細については、 [**FsRtlCancellableWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff545738)ルーチンと[**FsRtlCancellableWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff545731)ルーチンを参照してください。

-   何らかの重要なロックを保持しているスレッドが中断されると、デッドロックが発生する可能性があります。 ユーザーモードのスレッドが存在する場合は、デッドロック状態をチェックするために中断されないように、テストを実行することが重要です。

-   テストを実行して、"i/o 操作の待機" が本当にキャンセル可能なかどうかを確認し、ユーザーモードアプリケーションがスレッドをすぐに終了できるようにすることが重要です。これにより、アプリケーションは、スレッドを終了します。

Windows Vista の MUP で使用されるプレフィックスキャッシュサイズとタイムアウトは、次のレジストリ値によって制御されるようになりました。

-   PrefixCacheSizeInKB

-   PrefixCacheTimeoutInSeconds.

これらのレジストリ値は、再起動せずに動的に変更できます。 これらのレジストリ値は、次のレジストリキーの下にあります。

```cpp
HKLM\System\CurrentControlSet\Services\Mup\Parameters.
```

プロバイダーが個々のリダイレクターにプレフィックス解決要求を発行する順序を決定する ProviderOrder レジストリ値は、システムを再起動しなくても動的に変更できます。 このレジストリ値は、次のレジストリキーの下にあります。

```cpp
HKLM\CurrentControlSet\Control\NetworkProvider\Order
```

Windows Vista では、MUP は、ネットワークリダイレクターが MUP に登録されているかどうかによって、 [**Fsrtlregisteruncprovider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncprovider)または[**fsrtlregisterを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)呼び出すことによって、プレフィックスの解決方法が異なります。 **FsrtlregisterREDIR プロバイダー**を呼び出すことによって MUP に登録するレガシネットワークのリダイレクターは、プレフィックス解決のために\_パス要求に対して、 [**IOCTL\_\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ni-ntifs-ioctl_redir_query_path)を受け取ります。 これは、Windows Server 2003、Windows XP、および Windows 2000 で使用される方法と同じです。

Windows Vista リダイレクターモデルに準拠し、 [**FsrtlregisterREDIR Providerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlregisteruncproviderex)を呼び出すことによって MUP に登録されたネットワークリダイレクターは[ **\_、\_クエリ\_\_パス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ni-ntifs-ioctl_redir_query_path_ex)を使用して、プレフィックスに対する EX 要求を送信します。解決. Windows Vista では、ネットワークミニリダイレクターは rdbsslib に静的にリンクされているか、rdbss で動的にリンクされているため、RDBSS を通じて間接的に**Fsrtlregister**を呼び出します。

IOCTL\_REDIR\_クエリ\_パス\_EX の入力バッファーと出力バッファーは、次のようになります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left">パラメーターはで使用できます。</td>
<td align="left">データ構造の形式</td>
</tr>
<tr class="even">
<td align="left"><p>入力バッファー</p></td>
<td align="left"><p>IrpSp-&gt; Parameters. DeviceIoControl. Type3InputBuffer</p></td>
<td align="left"><p>QUERY_PATH_REQUEST_EX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>出力バッファー</p></td>
<td align="left"><p>IRP-&gt;UserBuffer</p></td>
<td align="left"><p>QUERY_PATH_RESPONSE</p></td>
</tr>
</tbody>
</table>



IOCTL とデータ構造は、ntifs で定義されています。 バッファーは、非ページプールから割り当てられます。

ネットワークリダイレクターは、 **Irp&gt;irp->requestormode**が**kernelmode で**であることを確認することによって、この IOCTL のカーネルモードの送信者のみに優先する必要があります。

MUP では、クエリの\_パス\_要求情報に\_EX データ構造を使用します。

```cpp
typedef struct _QUERY_PATH_REQUEST_EX {
  PIO_SECURITY_CONTEXT  pSecurityContext;
 ULONG  EaLength;
 PVOID  pEaBuffer;
  UNICODE_STRING  PathName;
} QUERY_PATH_REQUEST_EX, *PQUERY_PATH_REQUEST_EX;
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
<td align="left"><p><strong>pSecurityContext</strong></p></td>
<td align="left"><p>セキュリティコンテキストへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>EaLength</strong></p></td>
<td align="left"><p>拡張属性バッファーの長さ (バイト単位)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>pEaBuffer</strong></p></td>
<td align="left"><p>拡張属性バッファーへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>パス名</strong></p></td>
<td align="left"><p>&lt;server&gt;&lt;&gt;&lt;パス&gt;の形式の NULL で終わる NULL 以外の Unicode 文字列。</p></td>
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
<td align="left"><p>QUERY_PATH_REQUEST_EX 構造体の<strong>PathName</strong>メンバーに指定された Unicode 文字列パスからプロバイダーによって要求されたプレフィックスの長さ (バイト単位)。</p></td>
</tr>
</tbody>
</table>



IOCTL\_REDIR\_クエリ\_パス\_EX は、IOCTL ではないメソッド\_メソッドであることに注意してください。 これは、入力バッファーと出力バッファーが同じアドレスにない可能性があることを意味します。 UNC プロバイダーでよくある間違いは、入力バッファーと出力バッファーが同じであると想定し、入力バッファーポインターを使用して応答を提供することです。

UNC プロバイダーが\_\_クエリ\_PATH\_EX 要求の IOCTL を受け取ると、クエリの**PathName**メンバーに指定されている unc パスを処理できるかどうかを判断する必要があります\_パス\_要求\_exデータ. その場合、UNC プロバイダーは、\_\_クエリの**許容**される長さのメンバーを、要求されたプレフィックスの長さ (バイト単位) で更新する必要があります。これにより、状態\_SUCCESS で IRP を完了します。 プロバイダーは、指定された UNC パスを処理できない場合、IOCTL\_REDIR\_QUERY\_PATH\_EX 要求を適切な NTSTATUS エラーコードで失敗させる必要があります。また、クエリの許容される**長さ**のメンバーを更新することはできません\_パス\_応答構造体。 プロバイダーは、任意の条件下で、他のメンバーまたは**パス名**文字列を変更することはできません。

Windows Vista では、UNC プロバイダーとしてのサポートを示す RDBSS の使用に基づくネットワークミニリダイレクターは、このプレフィックス要求を、ファイル\_作成\_ツリーを使用したユーザーモードの Createfile 呼び出しと同様に、通常のツリー接続作成として受信し\_接続フラグを設定します。 RDBSS は、 [**MRxCreateSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)要求をネットワークミニリダイレクターに送信し、その後に[**MRxSrvCallWinnerNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_srvcall_winner_notify)と[**MRxCreateVNetRoot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_v_net_root)を呼び出します。 このプレフィックス要求は、 [**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](https://msdn.microsoft.com/library/windows/hardware/ff550715)への呼び出しとして受信されません。 ネットワークミニリダイレクターが RDBSS に登録すると、ネットワークミニリダイレクターのドライバーディスパッチテーブルが RDBSS によってコピーされ、内部 RDBSS エントリポイントをポイントします。 RDBSS は、この IOCTL\_REDIR\_クエリ\_パス\_EX をネットワークミニリダイレクターの内部で受信し、 **MRxCreateSrvCall**、 **MRxSrvCallWinnerNotify**、および**MRxCreateVNetRoot**を呼び出します。 元の IOCTL\_REDIR\_クエリ\_パス\_EX IRP は、 **MRxCreateSrvCall**ルーチンに渡される RX\_コンテキストに含まれます。 また、 **MRxCreateSrvCall**に渡される RX\_コンテキストの次のメンバーが変更されます:

元の IRP が IRP\_MJ\_デバイス\_コントロールでも、 **MajorFunction**メンバーは IRP\_MJ\_CREATE に設定されます。

**SuppliedPathName**メンバーは、クエリ\_PATH\_REQUEST\_EX 構造体の PrefixClaim**のメンバーに**設定されます。

SuppliedPathName メンバー**は、クエリ**\_PATH\_REQUEST\_EX 構造体の**PrefixClaim**メンバーに設定されます。

**ThisIsATreeConnectOpen**メンバーは**TRUE**に設定されます。

**ThisIsAPrefixClaim**メンバーは**TRUE**に設定されます。

**SecurityContext**メンバーは、クエリ\_PATH\_REQUEST\_EX 構造体の**SecurityContext**メンバーに設定されます。

**EaBuffer**メンバーは、クエリ\_PATH\_REQUEST\_EX 構造体の**pEaBuffer**メンバーに設定されます。

**EaLength**メンバーは、クエリ\_PATH\_REQUEST\_EX 構造体の**EaLength**メンバーに設定されます。

**Create. Flags**メンバーには、RX\_コンテキスト\_作成\_フラグ\_UNC\_名前ビットセットが設定されます。

ネットワークミニリダイレクターがプレフィックス要求の詳細を表示する必要がある場合は、 [**MRxCreateSrvCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_create_srvcall)に渡される RX\_コンテキスト構造でこれらのメンバーを読み取ることができます。 それ以外の場合は、サーバー共有への接続を試行するだけで、 **MRxCreateSrvCall**の呼び出しが成功した場合には状態\_SUCCESS を返すことができます。 RDBSS は、ネットワークミニリダイレクターに代わってプレフィックス要求を行います。








