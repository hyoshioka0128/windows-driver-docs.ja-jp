---
title: Microsoft Windows vista MUP の変更点
description: Microsoft Windows vista MUP の変更点
ms.assetid: 8ca2f9bc-14f1-45d3-a397-f3e5459cf8ec
keywords:
- カーネル ネットワーク リダイレクター WDK、MUP
- MUP WDK ネットワーク リダイレクター
- 複数 UNC プロバイダー WDK ネットワーク リダイレクター
- UNC WDK ネットワーク リダイレクター
- カーネル ネットワーク リダイレクター WDK、Windows Vista リダイレクター モデル
- レガシ リダイレクター WDK ファイル システム
- プレフィックス解決の WDK ネットワーク リダイレクター
- プレフィックス キャッシュ WDK ネットワーク リダイレクター
- 二重のフィルタ リング WDK ネットワーク リダイレクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45524f2823bda74db343326487a536f2a4014b12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530656"
---
# <a name="mup-changes-in-microsoft-windows-vista"></a>Microsoft Windows vista MUP の変更点


Windows Vista では、さまざまなネットワーク リダイレクターに影響を与える複数 UNC プロバイダー (MUP) の変更を実装します。

MUP と分散ファイル システム (DFS) クライアントは、個別のバイナリ ファイルがあります。 MUP コンポーネントは mup.sys であり、DFS クライアントが dfsc.sys。 Windows Server 2003、Windows XP、および Windows 2000、MUP カーネル コンポーネント、mup.sys も含まれている DFS クライアント。

新しいリダイレクター モデルは、Windows Vista で定義されます。

-   MUP を呼び出すことによって、I/O マネージャーとファイル システムとして登録[ **IoRegisterFileSystem**](https://msdn.microsoft.com/library/windows/hardware/ff548494)します。

-   ネットワーク リダイレクターに MUP を使用して登録[ **FsRtlRegisterUncProviderEx** ](https://msdn.microsoft.com/library/windows/hardware/ff547184) 、Windows Vista で導入された新しいルーチン。

-   ネットワーク リダイレクターに名前のないデバイス オブジェクトを渡します[ **FsRtlRegisterUncProviderEx**](https://msdn.microsoft.com/library/windows/hardware/ff547184)します。

-   ネットワーク リダイレクターがデバイス名を渡します[ **FsRtlRegisterUncProviderEx**](https://msdn.microsoft.com/library/windows/hardware/ff547184)します。

-   ネットワーク リダイレクターは I/O マネージャーとファイル システムとして登録しません (呼び出しません[ **IoRegisterFileSystem**](https://msdn.microsoft.com/library/windows/hardware/ff548494))。

-   プレフィックスの解決、Ioctl、FSCTLs など、ネットワーク リダイレクターを MUP からすべての呼び出しは、Apc が有効になっているで行われます。 Apc が有効になっていることに加えその他のコンポーネントからすべての呼び出しが予想されます。 呼び出しを使用するときに[ **FsRtlCancellableWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff545738)または[ **FsRtlCancellableWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff545731)、newルーチンは Windows Vista で導入された、これにより、I/O 要求を発行したスレッドが終了した場合に待機時間が長いを中止できます。

-   プレフィックスの解決は IOCTL を使用して、実行\_REDIR\_クエリ\_パス\_EX、Windows Vista で導入された新しい IOCTL します。

-   MUP に登録されているネットワーク リダイレクター デバイス名では、MUP デバイス オブジェクトへのシンボリック リンクになります。

Windows Vista のリダイレクター モデルに準拠している、ネットワーク リダイレクターの MUP シンボリック リンクを作成オブジェクト マネージャーの名前空間への呼び出しでネットワーク リダイレクターで指定されたデバイス名で[ **FsRtlRegisterUncProviderEx**](https://msdn.microsoft.com/library/windows/hardware/ff547184)します。 このシンボリック リンクのターゲットは MUP のデバイス オブジェクト (\\デバイス\\Mup)。

MUP デバイス オブジェクトへのシンボリック リンクされているネットワーク リダイレクターのデバイス名とファイル システムとして MUP の登録の利点は、MUP を介してすべてのリモート ファイル システム I/O 操作といないだけ名前ベースの操作を参照してください。 そのリモート ファイル システム スタック上に存在する必要があるファイル システム フィルター ドライバーは MUP のデバイス オブジェクトを単にアタッチできます。 ファイル システム フィルター ドライバーのプロバイダー デバイス オブジェクトの名前をハードコーディングする必要はありません (\\デバイス\\LanmanRedirector、たとえば) そのドライバーをもはやにします。 これにより、ファイル システム フィルター ドライバーは、1 つの添付ファイルによってすべてのネットワーク リダイレクターに発行されるすべての I/O 操作を監視できます。 DFS (mup.sys) と個々 のネットワーク リダイレクターが個別に接続されている Windows Vista より前に、ファイル システム フィルター ドライバーに表示される重複の I/O 操作も削除されます (\\デバイス\\例については、LanmanRedirector) でI/O 操作を両方に監視する順序。

MUP のデバイス オブジェクトに関連付けられているファイル システム フィルター ドライバーは、特定のネットワーク リダイレクターに送信されるトラフィックをフィルター選択的にできます。 このような状況で、フィルター ドライバー関心のあるネットワーク リダイレクターのデバイス名にマップ プロバイダーの識別子を呼び出して、 [ **FsRtlMupGetProviderIdFromName** ](https://msdn.microsoft.com/library/windows/hardware/ff546971)ルーチン。 フィルター ドライバーを呼び出すことによって取得したプロバイダー識別子を比較することによって、特定のファイル オブジェクトのトラフィックをフィルター処理かどうか決定できます、 [ **FsRtlMupGetProviderInfoFromFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff546981)関心のあるネットワークの取締役会プロバイダー識別子を持つルーチン。

Windows Vista のリダイレクター モデルに準拠しているネットワーク リダイレクター。

-   リモート ファイル システムのスタック上のすべてのファイル オブジェクトは、MUP に解決します。 そのため、 [ **IoGetDeviceAttachmentBaseRef** ](https://msdn.microsoft.com/library/windows/hardware/ff548365) MUP、ファイル オブジェクトを所有するネットワーク リダイレクターいないのデバイス オブジェクトを返します。 ただし、ファイル オブジェクトのコンテンツは、ネットワーク リダイレクターで所有されています。

-   IRP\_MJ\_発行先のネットワーク リダイレクターのデバイスの名前を作成する (\\デバイス\\LanmanRedirector\\server\\を共有) にそのネットワーク リダイレクターの対象となります。MUP プレフィックスの解決を経由せずに、これとまったく同じでは、Windows Server 2003、Windows XP、および Windows 2000 をしました。

(動的または静的にリンクの) Windows Vista RDBSS に基づいていないネットワーク リダイレクターは、「レガシ リダイレクター」と呼ばれます。 これらのレガシ ネットワーク リダイレクターは次のとおりです。

-   ネットワークの MUP を使用して直接登録する Windows Server 2003、Windows XP、および Windows 2000 用に記述されたリダイレクター [ **FsRtlRegisterUncProvider**](https://msdn.microsoft.com/library/windows/hardware/ff547178)します。

-   ネットワークのミニ-Windows Server 2003、Windows XP、および Windows 2000 用に記述するリダイレクター rdbsslib.lib ライブラリを使用した Windows Server 2003、Windows XP、または Windows 2000 用に静的にリンクします。

-   ネットワークの MUP を使用して直接登録する Windows Vista 用に記述されたリダイレクター [ **FsRtlRegisterUncProviderEx**](https://msdn.microsoft.com/library/windows/hardware/ff547184)します。

RDBSS MUP を使用して登録するために、ネットワーク ミニ-リダイレクターに動的に Windows Vista RDBSS (rdbss.sys) に対して自動的にリンクするが、Windows Vista リダイレクターのモデルに準拠[ *FsRtlRegisterUncProviderEx*](https://msdn.microsoft.com/library/windows/hardware/ff547184). RDBSS MUP を使用して登録するために、静的にも自動的にリンク Windows Vista RDBSS (rdbsslib.lib) に対してネットワーク ミニ-リダイレクターが Windows Vista リダイレクター モデルに準拠**FsRtlRegisterUncProviderEx**.

MUP と直接登録する Windows Vista 用に記述されたレガシ ネットワーク リダイレクターは、Windows Vista のリダイレクター モデルに準拠する必要があります。

ネットワークを使用して直接 MUP を登録する Windows Server 2003、Windows XP、および Windows 2000 用に記述されたリダイレクター、 [ **FsRtlRegisterUncProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff547178)と同様に、まったく同じ方法を作業を続けるWindows Server 2003、Windows XP、および Windows 2000。 ネットワークのミニ-リダイレクター Windows Server 2003、Windows XP、および Windows 2000 用に記述された Windows Server 2003、Windows XP、および Windows 2000 がまったく同じ方法で Windows Server 2003 と同じ動作を続行の rdbsslib.lib ライブラリに静的にリンクWindows XP、および Windows 2000 の場合は。 これらのレガシ ネットワーク リダイレクターとミニ リダイレクターが、次の動作があります。

-   ファイル システムの登録を監視するファイル システム フィルター ドライバーに表示されます。

-   それらのデバイス オブジェクトがという名前です。 デバイス名のシンボリック リンクではないとを指していません\\デバイス\\MUP します。

-   ファイル オブジェクトは、ネットワーク リダイレクターの名前付きのデバイス オブジェクトに解決します。

-   プレフィックスの解決操作でのみ MUP が関係しています。 ネットワーク プロバイダーが識別されると、MUP「取得の」状態を返すことによって\_再解析します。 後続のすべての操作は、MUP が通過されます。

この動作は、それ以外の場合なら場合、プロバイダーのデバイス名へのシンボリック リンクが行われる double のフィルタ リングを防ぐために保持されているが\\デバイス\\MUP します。 この 2 つのフィルターが処理されて、次の理由になります。

-   ファイル システム フィルター ドライバーが既にアタッチされている\\デバイス\\MUP します。

-   ファイル システム フィルター ドライバーは、任意の登録ファイル システムにアタッチします。 ネットワーク リダイレクター以降、名前付きのデバイス オブジェクトを使用して自身を登録、ファイル システムとして、ファイル システム フィルター ドライバーは最終的に 2 回、同じ I/O をフィルター処理します。

Windows vista MUP の間の呼び出しが有効にすると、次の影響のある Apc で行われます。

-   保護するために必要な場合、コードから呼び出すと MUP のスレッドの中断に対して特に IOCTL、適切な方法でパスすることが重要\_REDIR\_クエリ\_パス ハンドラー。 スレッドの中断です、可能性のある"unbounded wait"操作長時間続くことができます。

-   (システムのスレッド) ではなくユーザー モード スレッドに常に関連するすべての「I/O の待機の」操作が「キャンセル可能な待機」に使用されるように重要です。 参照してください、 [ **FsRtlCancellableWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff545738)と[ **FsRtlCancellableWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff545731)詳細については、ルーチン。

-   いくつかの重要なロックを保持しているスレッドが中断を取得時に、デッドロックが発生する可能性があります。 ユーザー モード スレッドがデッドロック状態を確認する任意に中断された作業がある場合のテストの実行に重要です。

-   テストを実行することを確認することが重要かどうか「待機の I/O 操作の」は本当にキャンセル可能なとをユーザー モード アプリケーションを終了できますスレッド迅速にする際に「非対応」状態にするのには、アプリケーションが表示されないように前述のスレッドを終了します。

Windows vista MUP によって使用されるタイムアウトとプレフィックスのキャッシュ サイズは、次のレジストリ値によって制御されますようになりました。

-   PrefixCacheSizeInKB

-   PrefixCacheTimeoutInSeconds します。

これらのレジストリ値は、再起動せず、動的に変更することができます。 これらのレジストリ値は、次のレジストリ キーの下です。

```cpp
HKLM\System\CurrentControlSet\Services\Mup\Parameters.
```

システムを再起動しなくても問題が解決要求を個々 のリダイレクターをプレフィックスどの MUP の順序を決定する ProviderOrder レジストリ値を動的に変更することができます。 このレジストリ値は、次のレジストリ キーの下にあります。

```cpp
HKLM\CurrentControlSet\Control\NetworkProvider\Order
```

呼び出すネットワーク リダイレクターを MUP に登録するかどうかに応じて異なる方法でプレフィックスの解決を実行している MUP Windows vista では、 [ **FsRtlRegisterUncProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff547178)または[ **FsRtlRegisterUncProviderEx**](https://msdn.microsoft.com/library/windows/hardware/ff547184)します。 呼び出して MUP を登録する従来のネットワーク リダイレクター **FsRtlRegisterUncProvider**が表示されます、 [ **IOCTL\_REDIR\_クエリ\_パス**](https://msdn.microsoft.com/library/windows/hardware/ff548313)プレフィックス解決の要求。 これは、Windows Server 2003、Windows XP、および Windows 2000 で使用される同じメソッドです。

Windows Vista のリダイレクター モデルに準拠しており、呼び出すことによって MUP を登録するリダイレクターがネットワーク[ **FsRtlRegisterUncProviderEx** ](https://msdn.microsoft.com/library/windows/hardware/ff547184)が表示されます、 [ **IOCTL\_REDIR\_クエリ\_パス\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff548320)プレフィックス解決の要求。 呼び出しは、Windows vista では、ネットワークのミニ リダイレクター rdbsslib.lib と静的にリンクや rdbss.sys を動的にリンクされている**FsRtlRegisterUncProviderEx** RDBSS を通じて間接的にします。

IOCTL の入力と出力バッファー\_REDIR\_クエリ\_パス\_EX が次のようには。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left">パラメーターでご利用いただけます</td>
<td align="left">データ構造の形式</td>
</tr>
<tr class="even">
<td align="left"><p>入力バッファー</p></td>
<td align="left"><p>IrpSp-&gt; Parameters.DeviceIoControl.Type3InputBuffer</p></td>
<td align="left"><p>QUERY_PATH_REQUEST_EX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>出力バッファー</p></td>
<td align="left"><p>IRP-&gt;UserBuffer</p></td>
<td align="left"><p>QUERY_PATH_RESPONSE</p></td>
</tr>
</tbody>
</table>



IOCTL と、データ構造は、ntifs.h で定義されます。 バッファーは、非ページ プールから割り当てられます。

ネットワーク リダイレクターことを確認して、この IOCTL のカーネル モードの送信者を受け入れる必要があるのみ**Irp -&gt;requestormode で**は**kernelmode である**します。

MUP は、クエリを使用して\_パス\_要求\_EX 要求については、データ構造体。

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
<th align="left">構造体のメンバー</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>pSecurityContext</strong></p></td>
<td align="left"><p>セキュリティ コンテキストへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>EaLength</strong></p></td>
<td align="left"><p>拡張属性のバッファーの長さ、(バイト単位)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>pEaBuffer</strong></p></td>
<td align="left"><p>拡張属性バッファーへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>PathName</strong></p></td>
<td align="left"><p>NULL 以外で終わる、フォームの Unicode 文字列&amp;lt; server&gt;&amp;lt; 共有&gt;&amp;lt; パス&gt;します。</p></td>
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
<td align="left"><p>指定された Unicode 文字列のパスから、プロバイダーによって要求されたプレフィックスの長さ、(バイト単位)、 <strong>PathName</strong> QUERY_PATH_REQUEST_EX 構造体のメンバー。</p></td>
</tr>
</tbody>
</table>



注その IOCTL\_REDIR\_クエリ\_パス\_EX メソッドは、\_も IOCTL します。 これは、同じアドレスに入力と出力バッファーが存在しないことを意味します。 UNC プロバイダーでよくある間違いでは、入力バッファーと出力バッファーは同じであり、入力バッファーのポインターを使用して、応答を提供することを前提としています。

UNC プロバイダーが、IOCTL を受信すると\_REDIR\_クエリ\_パス\_の要求例で指定された UNC パスを処理できるかどうかを判断が、 **PathName**クエリのメンバー\_パス\_要求\_EX 構造体。 更新があるため、UNC プロバイダー場合、 **LengthAccepted** 、クエリのメンバー\_パス\_は要求し、状態がIRPの完了のプレフィックスの長さ、(バイト単位)と応答の構造\_成功します。 プロバイダーは、指定した UNC パスを処理できない場合は、IOCTL が失敗する必要があります\_REDIR\_クエリ\_パス\_EX で要求を適切な NTSTATUS エラー コードと、更新する必要があります、 **LengthAccepted** 、クエリのメンバー\_パス\_応答の構造。 プロバイダーは変更しないで、その他のメンバーのいずれかまたは**PathName**いずれかの条件下での文字列。

Windows vista では、ネットワーク ミニ-リダイレクター UNC プロバイダーはこのプレフィックスの要求を受信は正規のツリーに接続した場合と同じサポートを示す RDBSS を使用して作成、ファイルを使用してユーザー モード Createfile の呼び出しに似ています\_作成\_ツリー\_接続フラグを設定します。 RDBSS を送り、 [ **MRxCreateSrvCall** ](https://msdn.microsoft.com/library/windows/hardware/ff549864)要求への呼び出し後にネットワーク ミニ リダイレクターを[ **MRxSrvCallWinnerNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff550824)[ **MRxCreateVNetRoot**](https://msdn.microsoft.com/library/windows/hardware/ff549869)します。 呼び出しとしてこのプレフィックスの要求が送られて[ **MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]**](https://msdn.microsoft.com/library/windows/hardware/ff550715)します。 ネットワークのミニ リダイレクター登録される RDBSS と、キー RDBSS 内部 RDBSS エントリ ポイントをポイントする場所を空けるのネットワークのミニ リダイレクター ドライバー ディスパッチ テーブルがコピーされます。 この IOCTL 受信 RDBSS\_REDIR\_クエリ\_パス\_ネットワーク ミニリダイレクターと呼び出しを内部的に EX **MRxCreateSrvCall**、 **MRxSrvCallWinnerNotify**、および**MRxCreateVNetRoot**します。 元の IOCTL\_REDIR\_クエリ\_パス\_EX IRP が RX に含まれる\_コンテキストに渡され、 **MRxCreateSrvCall**ルーチン。 さらに、次のメンバー、RX で\_に渡されるコンテキスト**MRxCreateSrvCall**が変更されます。

**MajorFunction** IRP にメンバーが設定されている\_MJ\_作成元の IRP が IRP も\_MJ\_デバイス\_コントロール。

**PrefixClaim.SuppliedPathName.Buffer**にメンバーが設定されている、 **PathName.Buffer** 、クエリのメンバー\_パス\_要求\_EX 構造体。

**PrefixClaim.SuppliedPathName.Length**にメンバーが設定されている、 **PathName.Length** 、クエリのメンバー\_パス\_要求\_EX 構造体。

**Create.ThisIsATreeConnectOpen**にメンバーが設定されている、 **TRUE**します。

**Create.ThisIsAPrefixClaim**にメンバーが設定されている、 **TRUE**します。

**Create.NtCreateParameters.SecurityContext**にメンバーが設定されている、 **SecurityContext** 、クエリのメンバー\_パス\_要求\_EX 構造体。

**Create.EaBuffer**にメンバーが設定されている、 **pEaBuffer** 、クエリのメンバー\_パス\_要求\_EX 構造体。

**Create.EaLength**にメンバーが設定されている、 **EaLength** 、クエリのメンバー\_パス\_要求\_EX 構造体。

**Create.Flags**メンバーは、RX が\_コンテキスト\_作成\_フラグ\_UNC\_名ビットが設定されます。

RX でこれらのメンバーを読み取ることができるプレフィックスの要求の詳細を表示する場合、ネットワーク ミニリダイレクター\_に渡されるコンテキスト構造[ **MRxCreateSrvCall**](https://msdn.microsoft.com/library/windows/hardware/ff549864)します。 それ以外の場合、そのサーバー共有に接続して状態を返す試みることができますのみ\_成功した場合、 **MRxCreateSrvCall**呼び出しに成功しました。 RDBSS はミニ リダイレクターにに代わってネットワーク要求のプレフィックスになります。








