---
title: プリンター ドライバーの分離
description: プリンタードライバーを分離すると、印刷スプーラが実行されているプロセスとは別のプロセスでプリンタードライバーを実行できるようになるため、Windows プリントサービスの信頼性が向上します。
ms.assetid: b0f11b3f-92f7-41f6-8edb-63b5651f5499
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54dda102a57d0abcd308d881f10d18f6ce336d63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840437"
---
# <a name="printer-driver-isolation"></a>プリンター ドライバーの分離


プリンタードライバーを分離すると、印刷スプーラが実行されているプロセスとは別のプロセスでプリンタードライバーを実行できるようになるため、Windows プリントサービスの信頼性が向上します。

プリンタードライバーの分離のサポートは、Windows 7、Windows Server 2008 R2、およびそれ以降のオペレーティングシステムで実装されています。

Windows 7 および Windows Server 2008 R2 では、受信トレイプリンタードライバーは、プリンタードライバーの分離をサポートし、分離されたプロセスで実行できる必要があります。

### <a href="" id="previous-versions-of-windows"></a>以前のバージョンの Windows

Windows Server 2008 を含め、以前のバージョンの Windows では、プリンタードライバーは常にスプーラと同じプロセスで実行されていました。 スプーラプロセスで実行されたプリンタドライバコンポーネントには、次のものが含まれます。

-   印刷ドライバーの構成モジュール

-   プリントプロセッサ

-   レンダリングモジュール

印刷ドライバーコンポーネントが1つでも失敗すると、印刷サブシステムが失敗し、すべてのユーザーとすべての印刷コンポーネントで印刷操作が停止する可能性があります。

### <a href="" id="new-versions-of-windows"></a>新しいバージョンの Windows

Windows 7 と Windows Server 2008 R2 では、管理者はオプションとして、プリンタードライバーを分離プロセスで実行するように構成することができます。これは、スプーラプロセスとは別のプロセスです。 ドライバーを分離することにより、管理者はドライバーコンポーネントのエラーによって印刷サービスが停止するのを防ぐことができます。

スプーラ関数の詳細については、「[スプーラコンポーネントの関数と構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)」を参照してください。

### <a href="" id="driver-isolation-support-in-inf-files"></a>INF ファイルでのドライバーの分離のサポート

既定では、プリンタードライバーをインストールする INF ファイルにドライバーがドライバーの分離をサポートしていることが示されていない場合、プリンタークラスインストーラーによってドライバーがスプーラプロセスで実行されるように構成されます。 ただし、ドライバーがドライバーの分離をサポートしていることが INF ファイルによって示されている場合、インストーラーは、分離されたプロセスで実行されるようにドライバーを構成します。 管理者は、これらの構成設定を上書きして、各ドライバーのドライバーをスプーラプロセスで実行するか、分離プロセスで実行するかを指定できます。

ドライバーの分離をサポートするために、プリンタードライバーをインストールする INF ファイルで**Driverisolation**キーワードを使用して、ドライバーがプリンタードライバーの分離をサポートしているかどうかを示すことができます。 **Driverisolation**= 2 を設定すると、ドライバーがドライバーの分離をサポートしていることを示します。 **Driverisolation**= 0 を設定すると、ドライバーがドライバーの分離をサポートしていないことを示します。 INF ファイルから**driverisolation**キーワードを省略すると、 **driverisolation**= 0 を設定した場合と同じ効果があります。

### <a href="" id="spooler-functions-for-driver-isolation-settings"></a>ドライバー分離設定のスプーラ関数

次の表は、管理者がドライバーの分離設定を構成するために使用できるスプーラ関数を示しています。

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
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135631" data-raw-source="[GetPrinterDataEx](https://go.microsoft.com/fwlink/p/?linkid=135631)">Getプリンター Dataex</a></p></td>
<td><p>プリンターのドライバー分離設定を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135632" data-raw-source="[SetPrinterDataEx](https://go.microsoft.com/fwlink/p/?linkid=135632)">Setプリンター Dataex</a></p></td>
<td><p>プリンターのドライバー分離設定を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135633" data-raw-source="[EnumPrinterDataEx](https://go.microsoft.com/fwlink/p/?linkid=135633)">Enumプリンター Dataex</a></p></td>
<td><p>プリンタのドライバ分離設定を列挙します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=135634" data-raw-source="[FindFirstPrinterChangeNotification](https://go.microsoft.com/fwlink/p/?linkid=135634)">FindFirstPrinterChangeNotification</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=135635" data-raw-source="[FindNextPrinterChangeNotification](https://go.microsoft.com/fwlink/p/?linkid=135635)">FindNextPrinterChangeNotification</a></p></td>
<td><p>プリンタのドライバ分離設定に対する変更の通知を要求します。</p></td>
</tr>
</tbody>
</table>

 

データの形式は次のとおりです。

-   各グループのドライバーは '\\' で区切られます
-   各ドライバーグループは '\\\\' で区切られています

最初のグループは、ドライバーをスプーラプロセスに読み込みます。 後続の各グループは、各グループの分離されたプロセスのドライバーを読み込みます。 2つ目のグループは、既定で他の分離対応ドライバーが読み込まれる "共有" グループと見なされます。

### <a href="" id="configuring-driver-isolation-mode-through-administration"></a>管理によるドライバー分離モードの構成

コンピューター管理者は、Windows 印刷管理コンソールを使用することも、Windows スプーラ機能を呼び出して、コンピューターにインストールされている各プリンタードライバーのドライバー分離設定を構成することもできます。 管理者は、次の表に示す設定のいずれかを使用するようにドライバーを構成します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ドライバー分離モード</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>共有</p></td>
<td><p>他のプリンタードライバーと共有されているがスプーラプロセスとは別のプロセスで、ドライバーを実行します。</p></td>
</tr>
<tr class="even">
<td><p>分離</p></td>
<td><p>スプーラプロセスとは別のプロセスでドライバを実行し、他のプリンタドライバとは共有しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p>なし</p></td>
<td><p>スプーラプロセスでドライバを実行します。</p></td>
</tr>
</tbody>
</table>

 

プリンタードライバーは、共有モードで実行できるのが理想的です。 つまり、他のプリンタードライバーと共有される分離プロセスで実行されますが、スプーラプロセスとは異なります。 ドライバーは、スプーラプロセスとは別のプロセスで実行できるが、プロセスを他のドライバーと共有するのが困難な場合は、分離モードで実行する必要があります。 たとえば、適切に設計されていないドライバーは、関連するドライバーや同じドライバーの異なるバージョンのファイル名と競合している可能性があります。または、ドライバーが頻繁に障害を発生させるか、またはで実行される他のドライバーの操作を妨げるメモリリークが発生する可能性があります。同じプロセス。

トラブルシューティングをサポートするために、ドメイン管理者はドメイン内のコンピューターでドライバー分離機能を無効にすることができます。また、管理者は、コンピューター上のすべてのプリンタードライバーを強制的に分離モードで実行することもできます。 分離モードでは、各ドライバーはスプーラと他のプリンタードライバーとは別のプロセスで実行する必要があります。

ドライバーの分離がグループポリシーによって無効にされている場合、すべてのプリンタードライバーで分離が無効になります。 分離が有効になっている場合、個々のドライバーはモードでチェックされます。 ドライバーが分離モードを設定している場合は、レジストリエントリに基づいて、共有、分離、またはなしモードで実行されます。 ただし、分離モードが設定されておらず、分離と互換性があるドライバーは、共有モードで実行されます。 ドライバーがモードと互換性がない場合は、グループポリシーの上書きによって、ドライバーが共有モードと none モードのどちらで実行されるかが決まります。

次の表は、ドライバーの分離モードを選択するためのデシジョンマップを示しています。

![ドライバーの分離モードを選択するためのフローチャート](images/isolation.png)

### <a name="spooler-functions-allowed-under-driver-isolation"></a>ドライバーの分離下で許可されるスプーラ関数

ドライバーの分離では、特定の関数のみが許可されます。

### <a href="" id="spoolss-dll-functions"></a>Spoolss 関数

次の関数は、spoolss によってエクスポートされ、spoolss にリンクすることでスプーラプラグインで使用できます。

**AddMonitorW**

**Appendプリンター Notifyinfodata**

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

**Getプリンター Dataw**

**Getプリンター Driverdirectoryw**

**Getプリンター Driverw**

**Getプリンター w**

**ImpersonatePrinterClient**

**Openプリンター w**

**ReadPrinter**

**RouterCreatePrintAsyncNotificationChannel**

**RouterGetPrintClassObject**

**SetJobW**

**SetPrinterDataExW**

**Setプリンター Dataw**

**Startdocプリンター w**

**StartPagePrinter**

**WritePrinter**

### <a href="" id="winspool-drv-functions"></a>WinSpool. drv 関数

次の関数は winspool によってエクスポートされ、Winspool にリンクすることでスプーラプラグインで使用できます。

**Appendプリンター Notifyinfodata**

**ExtDeviceMode**

**ImpersonatePrinterClient**

**IsValidDevmode**

**PartialReplyPrinterChangeNotification**

**ReplyPrinterChangeNotification**

**RevertToPrinterSelf**

**RouterAllocBidiMem**

**RouterAllocBidiResponseContainer**

**Routerallocプリンター Notifyinfo**

**RouterCreatePrintAsyncNotificationChannel**

**RouterFreeBidiMem**

**RouterFreeBidiResponseContainer**

**Routerfreeプリンター Notifyinfo**

**RouterGetPrintClassObject**

**RouterRegisterForPrintAsyncNotifications**

**RouterUnregisterForPrintAsyncNotifications**

 

 




