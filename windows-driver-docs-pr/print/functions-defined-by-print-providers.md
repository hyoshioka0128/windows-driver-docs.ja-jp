---
title: 印刷プロバイダーによって定義されている関数
description: 印刷プロバイダーによって定義されている関数
ms.assetid: 4fae4b69-ed4b-47b6-b6e8-41733aed51a5
keywords:
- プロバイダー WDK、関数を印刷します。
- 関数の WDK 印刷プロバイダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ec343fd5db0345044216287d0d559aa4c32d43f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363444"
---
# <a name="functions-defined-by-print-providers"></a>印刷プロバイダーによって定義されている関数





**警告**  以降 Windows 10 では、サード パーティの印刷プロバイダーをサポートする Api は非推奨とされます。 Microsoft には、サード パーティの印刷プロバイダーに他の投資はお勧めしません。 さらに、Windows 8 および v4 印刷ドライバー モデルが使用可能な新しい製品では、サード パーティの印刷プロバイダーが作成や v4 印刷ドライバーを使用するキューを管理します。

 

このトピックでは、すべての印刷のプロバイダーが提供できる機能を一覧表示します。 これらの関数のほとんどは、Microsoft Windows SDK ドキュメントで説明します。 関数は、Windows Driver Kit (WDK) で説明されている、関数名は、関連付けられている参照ページへのリンクを提供します。

すべての印刷プロバイダーは、上記のすべての関数のポインターを提供する必要があります。 ただし、ほとんどのベンダーから提供された印刷プロバイダーは、関数で定義されている操作の多くをサポートする必要はありません「部分的なプロバイダー」です。 関数ポインターの多くは、そのため、 **NULL**します。 部分的な印刷プロバイダーの詳細については、次を参照してください。[ネットワーク印刷のプロバイダーを記述](writing-a-network-print-provider.md)します。

サポートする必要がある関数は次の関数のリストで、"Required"ラベル付けされます。

すべての印刷プロバイダーは、初期化関数をエクスポートする必要があります[ **InitializePrintProvidor**](https://msdn.microsoft.com/library/windows/hardware/ff551614)します。 その他のすべての関数へのポインターを指定する必要があります、 [ **PRINTPROVIDOR** ](https://msdn.microsoft.com/library/windows/hardware/ff560993)構造体。 (これら 2 つの名前は、スペルが間違っているが、ヘッダー ファイル、Winsplp.h で表示される名前との一貫性に注意してください)。

関数は、グループに分割し、次のセクションに表示されます。

初期化関数

印刷キューの管理機能

プリンター ドライバーの管理機能

印刷ジョブの作成機能

印刷ジョブのスケジュールの機能

フォームの管理機能

印刷の管理機能のプロセッサ

印刷管理機能の監視

ポートの管理機能

レジストリの管理機能

その他の関数

### <a href="" id="ddk-initialization-function-gg"></a>初期化関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551614" data-raw-source="[&lt;strong&gt;InitializePrintProvidor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551614)"><strong>InitializePrintProvidor</strong> </a> (必須)</p></td>
<td><p>印刷のプロバイダーを初期化し、指定された関数へのポインターを返します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-print-queue-management-functions-gg"></a>印刷キューの管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddPrinter</strong></p></td>
<td><p>印刷のプロバイダーで管理されている一覧に印刷キューを追加し、印刷キューをプリント プロセッサを関連付けます。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPrinterConnection</strong></p></td>
<td><p>指定した印刷キューへの接続を作成します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClosePrinter</strong> (必須)</p></td>
<td><p>指定した印刷キューへの呼び出し元のアクセスを無効にします。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeletePrinter</strong></p></td>
<td><p>印刷プロバイダーによって管理されている一覧から印刷キューを削除します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeletePrinterConnection</strong></p></td>
<td><p>指定した印刷キューへの接続を削除します。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumPrinters</strong> (必須)</p></td>
<td><p>印刷のプロバイダーによって現在管理されている印刷キューの一覧を列挙します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FindClosePrinterChangeNotification</strong></p></td>
<td><p>有効にしていたプリンターの変更通知を無効にします。 <strong>FindFirstPrinterChangeNotification</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>FindFirstPrinterChangeNotification</strong></p></td>
<td><p>指定したプリンター イベントを待機する、呼び出し元が使用できる待機オブジェクト ハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetPrinter</strong> (必須)</p></td>
<td><p>指定した印刷キューの現在パラメーター値を返します。</p></td>
</tr>
<tr class="even">
<td><p><strong>ようになりました</strong>(必須)</p></td>
<td><p>指定した印刷キューへの呼び出し元のアクセスを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561930" data-raw-source="[&lt;strong&gt;RefreshPrinterChangeNotification&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561930)"><strong>RefreshPrinterChangeNotification</strong></a></p></td>
<td><p>クライアントが呼び出す場合、ルーターによって呼び出されます<strong>FindNextPrinterChangeNotification</strong> (Microsoft Windows SDK のドキュメントを参照してください)、PRINTER_NOTIFY_OPTIONS_REFRESH でフラグを設定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>ResetPrinter</strong></p></td>
<td><p>印刷キューのデータ型を変更または<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SetPrinter</strong> (必須)</p></td>
<td><p>指定した印刷キューのパラメーターを設定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>WaitForPrinterChange</strong></p></td>
<td><p>使われていません。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-printer-driver-management-functions-gg"></a>プリンター ドライバーの管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddPrinterDriver</strong></p></td>
<td><p>指定したサーバーには、指定したプリンターのドライバー ファイルを追加します。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPrinterDriverEx</strong></p></td>
<td><p>同じ<strong>AddPrinterDriver</strong>、追加のパラメーターを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeletePrinterDriver</strong></p></td>
<td><p>指定したサーバー上の指定したプリンターのドライバー ファイルへのアクセスを削除します。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeletePrinterDriverEx</strong></p></td>
<td><p>同じ<strong>DeletePrinterDriver</strong>、追加のパラメーターを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumPrinterDrivers</strong></p></td>
<td><p>呼び出すことによって指定されたサーバーに追加されたプリンター ドライバーの一覧を返します<strong>AddPrinterDriver</strong>または<strong>AddPrinterDriverEx</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetPrinterDriver</strong></p></td>
<td><p>呼び出し元に渡すことができますし、プリンター ドライバーに関する情報を返します<strong>AddPrinterDriver</strong>します。 (返される情報は、INF ファイルから通常取得)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetPrinterDriverEx</strong></p></td>
<td><p>同じ<strong>GetPrinterDriver</strong>、追加のパラメーターを使用します。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetPrinterDriverDirectory</strong></p></td>
<td><p>ドライバーのディレクトリ サーバーのプリンターの名前を返します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-print-job-creation-functions-gg"></a>印刷ジョブの作成機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<strong>AbortPrinter</strong> (必須)</td>
<td><p>指定した印刷キューから現在のジョブを削除しようとします。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>AddJob</strong> (必須)</td>
<td><p>ジョブの識別子とスプール ファイルのパスを返します。 呼び出し元を使用して<a href="https://msdn.microsoft.com/library/windows/desktop/aa363858" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363858)"> <strong>CreateFile</strong> </a>と<strong>WriteFile</strong>スプール ファイルにデータを送信します。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>EndDocPrinter</strong> (必須)</td>
<td><p>ジョブの完了操作を実行します。</p></td>
</tr>
<tr class="even">
<td><p><strong>EndPagePrinter</strong></p></td>
<td><p>ページの完了操作を実行します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ReadPrinter</strong></p></td>
<td><p>双方向プリンターからステータス情報を取得します。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>ScheduleJob</strong> (必須)</td>
<td><p>指定したジョブをスケジュールできることをプロバイダーに通知します。 ジョブがによって以前返されるジョブの識別子で指定された<strong>AddJob</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>StartDocPrinter</strong> (必須)</td>
<td><p>印刷ジョブをスプールする印刷プロバイダーを準備します。</p></td>
</tr>
<tr class="even">
<td><p><strong>StartPagePrinter</strong></p></td>
<td><p>印刷ジョブ ページの受信に印刷プロバイダーを準備します。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>WritePrinter</strong> (必須)</td>
<td><p>印刷ジョブのデータ ストリームの一部を受け取ります。</p></td>
</tr>
</tbody>
</table>

 

**注**   、 **AddJob**.**ScheduleJob**シーケンスは、代わりに、 **StartDocPrinter**.**EndDocPrinter**シーケンス。

 

### <a href="" id="ddk-print-job-scheduling-functions-gg"></a>印刷ジョブのスケジュールの機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<strong>EnumJobs</strong> (必須)</td>
<td><p>スケジュールされた印刷ジョブの一覧を返します。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>GetJob</strong> (必須)</td>
<td><p>ジョブのパラメーターを返します。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>SetJob</strong> (必須)</td>
<td><p>キャンセル、一時停止、再開すると、または、印刷ジョブを再開またはジョブのパラメーターを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-forms-management-functions-gg"></a>フォームの管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddForm</strong></p></td>
<td><p>利用可能なプリンターの一覧を指定されたフォームを追加します。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeleteForm</strong></p></td>
<td><p>利用可能なプリンターの一覧から、指定した形式を削除します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumForms</strong></p></td>
<td><p>指定したプリンターで使用できるフォームの一覧を返します。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetForm</strong></p></td>
<td><p>指定されたフォームの特性を返します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SetForm</strong></p></td>
<td><p>指定されたフォームの特性を変更します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-print-processor-management-functions-gg"></a>印刷の管理機能のプロセッサ

関数の説明**AddPrintProcessor**

指定されたサーバーでプリント プロセッサをインストールし、それを呼び出すことができる、印刷プロバイダーの一覧に追加します。

**DeletePrintProcessor**

印刷のプロバイダーを呼び出すことができるものの一覧から、プリント プロセッサを削除します。

**EnumPrintProcessorDataTypes**

印刷のプロバイダーによって呼び出すことができるプリント プロセッサによってサポートされるデータ型の一覧を返します。

**EnumPrintProcessors**

印刷のプロバイダーを呼び出すことができるプリント プロセッサの一覧を返します。

**GetPrintProcessorDirectory**

プリント プロセッサ ファイルの保存されているディレクトリのパスを返します。

 

### <a href="" id="ddk-print-monitor-management-functions-gg"></a>印刷管理機能の監視

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddMonitor</strong></p></td>
<td><p>印刷のプロバイダーを呼び出すことができるものの一覧には、印刷のモニターを追加します。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeleteMonitor</strong></p></td>
<td><p>印刷のプロバイダーを呼び出すことができるものの一覧から、印刷のモニターを削除します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumMonitors</strong></p></td>
<td><p>印刷のプロバイダーを呼び出すことができる印刷のモニターの一覧を返します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-port-management-functions-gg"></a>ポートの管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AddPort</strong></p></td>
<td><p>通常、指定したポート モニターを呼び出すことによって利用可能なリストに、プリンター ポートを追加します。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545026" data-raw-source="[&lt;strong&gt;AddPortUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545026)"> <strong>AddPortUI</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPortEx</strong></p></td>
<td><p>同じ<strong>AddPort</strong>、追加のパラメーターを使用します。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>ConfigurePort</strong> (必須)</td>
<td><p>呼び出して、指定したポート モニターの通常、プリンター ポートを構成します<a href="https://msdn.microsoft.com/library/windows/hardware/ff546290" data-raw-source="[&lt;strong&gt;ConfigurePortUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546290)"> <strong>ConfigurePortUI</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>DeletePort</strong> (必須)</td>
<td><p>通常、指定したポート モニターを呼び出すことによって利用可能な一覧からプリンター ポートを削除します。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547432" data-raw-source="[&lt;strong&gt;DeletePortUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547432)"> <strong>DeletePortUI</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>EnumPorts</strong> (必須)</td>
<td><p>利用可能なポートの一覧を返します。</p></td>
</tr>
<tr class="even">
<td><p><strong>SetPort</strong></p></td>
<td><p>指定されたプリンター ポートのパラメーターを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-registry-management-functions-gg"></a>レジストリの管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DeletePrinterData</strong></p></td>
<td><p>指定したプリンターの下の指定された値名に現在割り当てられている値を削除します<strong>PrinterDriverData</strong>キー。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeletePrinterDataEx</strong></p></td>
<td><p>同じ<strong>DeletePrinterData</strong>、追加のパラメーターを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeletePrinterKey</strong></p></td>
<td><p>指定したプリンターの下のレジストリに現在格納されている場合、指定したキーおよびそのサブキーを削除します<strong>PrinterDriverData</strong>キー。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumPrinterData</strong></p></td>
<td><p>それぞれの値の名前であり、現在割り当てられている指定されたプリンターの下のレジストリに格納されている値を返します<strong>PrinterDriverData</strong>キー。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumPrinterDataEx</strong></p></td>
<td><p>同じ<strong>EnumPrinterData</strong>、追加のパラメーターを使用します。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumPrinterKey</strong></p></td>
<td><p>指定したキー名の下のレジストリに現在含まれているサブキーの一覧を返します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetPrinterData</strong></p></td>
<td><p>指定したプリンターの下のレジストリに格納されている指定された値の名前に現在割り当てられている値を返します<strong>PrinterDriverData</strong>キー。</p></td>
</tr>
<tr class="even">
<td><p><strong>GetPrinterDataEx</strong></p></td>
<td><p>同じ<strong>GetPrinterData</strong>、追加のパラメーターを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SetPrinterData</strong></p></td>
<td><p>指定された値の名前と値を指定したプリンターの 、レジストリに格納<strong>PrinterDriverData</strong>キー。</p></td>
</tr>
<tr class="even">
<td><p><strong>SetPrinterDataEx</strong></p></td>
<td><p>同じ<strong>SetPrinterData</strong>、追加のパラメーターを使用します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-other-functions-gg"></a>その他の関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564255" data-raw-source="[&lt;strong&gt;XcvData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564255)"><strong>XcvData</strong></a></p></td>
<td><p>ポート モニター UI の DLL とポートの監視サーバー DLL 間の通信パスを提供します。</p></td>
</tr>
</tbody>
</table>

 

 

 




