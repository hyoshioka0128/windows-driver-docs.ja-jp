---
title: プリンター ドライバーの分離
description: プリンター ドライバーの分離では、印刷スプーラが実行されているプロセスから独立しているプロセスで実行するプリンター ドライバーを有効にすると、Windows プリント サービスの信頼性が向上します。
ms.assetid: b0f11b3f-92f7-41f6-8edb-63b5651f5499
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d60aeadbefa59113df234c245fb03116f98744c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579981"
---
# <a name="printer-driver-isolation"></a>プリンター ドライバーの分離


プリンター ドライバーの分離では、印刷スプーラが実行されているプロセスから独立しているプロセスで実行するプリンター ドライバーを有効にすると、Windows プリント サービスの信頼性が向上します。

プリンター ドライバーの分離のサポートは、Windows 7、Windows Server 2008 R2 以降のオペレーティング システムで実装されます。

Windows 7 と Windows Server 2008 R2 では、受信トレイのプリンター ドライバーはプリンター ドライバーの分離をサポートしてとを分離プロセスで実行できる必要があります。

### <a href="" id="previous-versions-of-windows"></a> Windows の以前のバージョン

Windows の以前のバージョンでプリンター ドライバーを常に、Windows Server 2008 を含む、スプーラーと同じプロセスで実行されました。 スプーラーのプロセスで実行されたプリンター ドライバー コンポーネントには、次のものが含まれています。

-   印刷ドライバーの構成モジュール

-   プリント プロセッサ

-   モジュールの表示

1 つの印刷ドライバー コンポーネントのエラーの考えられる原因が失敗し、印刷サブシステム印刷操作のすべてのユーザーとすべての印刷コンポーネントを停止します。

### <a href="" id="new-versions-of-windows"></a> 新しいバージョンの Windows

Windows 7 および Windows Server 2008 R2 では、管理者は、オプションとして、構成できますプリンター ドライバーを分離プロセス - は、スプーラーのプロセスから別のプロセスで実行します。 ドライバーを分離するには、管理者は、印刷サービスの停止からドライバー コンポーネントで障害を予防できます。

スプーラー機能の詳細については、[スプーラー コンポーネントの関数と構造体](https://msdn.microsoft.com/library/windows/hardware/ff562686)を参照してください。

### <a href="" id="driver-isolation-support-in-inf-files"></a> INF ファイルでのドライバーの分離のサポート

既定では、プリンター ドライバーをインストールする INF ファイルが、ドライバーがドライバーの分離をサポートしていることを表していない場合、プリンター クラスのインストーラーは、スプーラーのプロセスで実行するドライバーを構成します。 ただし、INF ファイルでは、ドライバーがドライバーの分離をサポートしていることを示します、インストーラーは、ドライバーを分離プロセスで実行を構成します。 管理者は、これらの構成設定をオーバーライドし、指定、各ドライバーでは、スプーラーのプロセスまたは分離プロセスで、ドライバーを実行するかどうか。

ドライバーの分離をサポートするプリンター ドライバーをインストールする INF ファイルを使用できる、 **DriverIsolation**ドライバーはプリンター ドライバーの分離をサポートするかどうかを示すキーワードです。 設定**DriverIsolation**= 2 は、ドライバーがドライバーの分離をサポートしていることを示します。 設定**DriverIsolation**= 0 では、ドライバーがドライバーの分離をサポートしていないことを示します。 省略すると、 **DriverIsolation** INF ファイルからのキーワードが設定と同じ効果**DriverIsolation**= 0。

### <a href="" id="spooler-functions-for-driver-isolation-settings"></a> ドライバーの分離設定のスプーラー関数

次の表では、ドライバーの分離設定を構成する管理者が使用できるスプーラー関数を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数名</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135631" data-raw-source="[GetPrinterDataEx](https://go.microsoft.com/fwlink/p/?linkid=135631)">GetPrinterDataEx</a></p></td>
<td><p>プリンターのドライバーの分離設定を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135632" data-raw-source="[SetPrinterDataEx](https://go.microsoft.com/fwlink/p/?linkid=135632)">SetPrinterDataEx</a></p></td>
<td><p>プリンターのドライバーの分離設定を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135633" data-raw-source="[EnumPrinterDataEx](https://go.microsoft.com/fwlink/p/?linkid=135633)">EnumPrinterDataEx</a></p></td>
<td><p>プリンターのドライバーの分離設定を列挙します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135634" data-raw-source="[FindFirstPrinterChangeNotification](https://go.microsoft.com/fwlink/p/?linkid=135634)">FindFirstPrinterChangeNotification</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=135635" data-raw-source="[FindNextPrinterChangeNotification](https://go.microsoft.com/fwlink/p/?linkid=135635)">FindNextPrinterChangeNotification</a></p></td>
<td><p>プリンターのドライバーの分離設定に対する変更の通知を要求します。</p></td>
</tr>
</tbody>
</table>

 

データの形式は次のとおりです。

-   各グループ内のドライバーがで区切られた '\\'
-   個々 のドライバー グループを区切って '\\\\'

最初のグループは、スプーラーのプロセスにドライバーを読み込みます。 後続の各グループは、グループごとの分離プロセスでドライバーを読み込みます。 2 番目のグループは、既定で分離できるその他のドライバーが読み込まれる '共有' のグループと見なされます。

### <a href="" id="configuring-driver-isolation-mode-through-administration"></a> 管理からドライバーの分離モードを構成します。

コンピューターの管理者は、Windows 印刷の管理コンソールを使用して、またはコンピューターにインストールされている各プリンター ドライバーのドライバーの分離設定を構成する Windows スプーラー関数を呼び出すことができます。 管理者は、次の表に示されている設定のいずれかを使用するドライバーを構成します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ドライバーの分離モード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Shared</p></td>
<td><p>その他のプリンター ドライバーでは共有されますが、スプーラーのプロセスとは別のプロセスで、ドライバーを実行します。</p></td>
</tr>
<tr class="even">
<td><p>分離</p></td>
<td><p>他のプリンター ドライバーとは共有されませんが、スプーラーのプロセスとは別のプロセスで、ドライバーを実行します。</p></td>
</tr>
<tr class="odd">
<td><p>なし</p></td>
<td><p>スプーラーのプロセスで、ドライバーを実行します。</p></td>
</tr>
</tbody>
</table>

 

理想的には、プリンター ドライバーは、共有モードで実行できるようにします。 実行を分離プロセスで他のプリンター ドライバーの共有が、スプーラーのプロセスから分離します。 ドライバーは、スプーラーのプロセスから別のプロセスで実行できる場合は、分離モードで実行する必要がありますが、プロセスを他のドライバーで共有が困難です。 たとえば、不適切に設計されたドライバーとの関連ドライバーまたは同じのドライバーの異なるバージョンの競合するファイル名がありますまたはドライバー可能性があります頻繁に障害で実行されているその他のドライバーの操作と競合するメモリ リークが発生同じプロセスです。

トラブルシューティングをサポートするには、ドメイン管理者は、ドメイン内のコンピューターでドライバーの分離機能を無効にできます。 または管理者は分離モードで実行するコンピューターのすべてのプリンター ドライバーを強制できます。 分離モードで各ドライバーは、スプーラーおよびその他のプリンター ドライバーから別のプロセスで実行する必要があります。

ドライバーの分離は、グループ ポリシーによって無効にした場合、分離がオフのすべてのプリンター ドライバーです。 分離が有効になっている場合、個々 のドライバーはモード チェックです。 ドライバーの分離モードの設定にされている場合で実行される共有、分離、または none レジストリ エントリに基づくモード。 ただし場合は、ドライバーには、分離モードの設定はありません。 分離との互換性が、共有モードで実行されます。 グループ ポリシーの上書きが、ドライバーが共有モードまたは none で実行するかどうかを決定、ドライバーが、モードと互換性がない場合モード。

次のグラフには、ドライバーの分離モードを選択するための意思決定のマップが表示されます。

![ドライバーの分離モードを選択するためのフローチャート](images/isolation.png)

### <a name="spooler-functions-allowed-under-driver-isolation"></a>ドライバーの分離レベルで許可されているスプーラー関数

ドライバーの分離レベルでは、特定の関数のみが許可されています。

### <a href="" id="spoolss-dll-functions"></a>Spoolss.dll 関数

次の関数は、spoolss.dll によってエクスポートし、spoolss.lib へのリンクによるスプーラー プラグインを利用します。

**AddMonitorW**

**AppendPrinterNotifyInfoData**

**ClosePrinter**

**DeletePortW**

**DeletePrintProcessorW**

**EndDocPrinter**

**EndPagePrinter**

**EnumFormsW**

**EnumJobsW**

**FlushPrinter**

**GetJobAttributes**

**GetJobAttributesEx**

**GetJobW**

**GetPrinterDataExW**

**GetPrinterDataW**

**GetPrinterDriverDirectoryW**

**GetPrinterDriverW**

**GetPrinterW**

**ImpersonatePrinterClient**

**OpenPrinterW**

**ReadPrinter**

**RouterCreatePrintAsyncNotificationChannel**

**RouterGetPrintClassObject**

**SetJobW**

**SetPrinterDataExW**

**SetPrinterDataW**

**StartDocPrinterW**

**StartPagePrinter**

**WritePrinter**

### <a href="" id="winspool-drv-functions"></a>WinSpool.drv 関数

次の関数は、winspool.drv によってエクスポートし、Winspool.h へのリンクによるスプーラー プラグインを利用します。

**AppendPrinterNotifyInfoData**

**復元するため**

**ImpersonatePrinterClient**

**IsValidDevmode**

**PartialReplyPrinterChangeNotification**

**ReplyPrinterChangeNotification**

**RevertToPrinterSelf**

**RouterAllocBidiMem**

**RouterAllocBidiResponseContainer**

**RouterAllocPrinterNotifyInfo**

**RouterCreatePrintAsyncNotificationChannel**

**RouterFreeBidiMem**

**RouterFreeBidiResponseContainer**

**RouterFreePrinterNotifyInfo**

**RouterGetPrintClassObject**

**RouterRegisterForPrintAsyncNotifications**

**RouterUnregisterForPrintAsyncNotifications**

 

 




