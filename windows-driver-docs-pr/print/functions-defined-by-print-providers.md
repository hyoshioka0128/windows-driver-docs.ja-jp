---
title: 印刷プロバイダーによって定義されている関数
description: 印刷プロバイダーによって定義されている関数
ms.assetid: 4fae4b69-ed4b-47b6-b6e8-41733aed51a5
keywords:
- 印刷プロバイダー WDK、functions
- functions WDK 印刷プロバイダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e617511b1d4e5f508ded0e53d9fe2907925a55d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845299"
---
# <a name="functions-defined-by-print-providers"></a>印刷プロバイダーによって定義されている関数





**警告**   Windows 10 以降では、サードパーティの印刷プロバイダーをサポートする api は非推奨とされます。 Microsoft では、サードパーティの印刷プロバイダーに投資することはお勧めしません。 さらに、Windows 8 および v4 印刷ドライバーモデルが使用可能な新しい製品では、サードパーティ製の印刷プロバイダーが v4 印刷ドライバーを使用するキューを作成または管理できないことがあります。

 

このトピックでは、印刷プロバイダーが提供できるすべての関数の一覧を示します。 これらの関数の大部分については、Microsoft Windows SDK のドキュメントを参照してください。 関数が Windows Driver Kit (WDK) で記述されている場合、関数名は関連付けられている参照ページへのリンクを提供します。

すべての印刷プロバイダーは、一覧表示されているすべての関数のポインターを提供する必要があります。 ただし、ほとんどのベンダーが提供する印刷プロバイダーは、関数によって定義される操作の多くをサポートする必要がない "部分プロバイダー" です。 したがって、関数ポインターの多くは**NULL**にすることができます。 部分的な印刷プロバイダーの詳細については、「[ネットワーク印刷プロバイダーの作成](writing-a-network-print-provider.md)」を参照してください。

次の関数の一覧では、サポートする必要がある関数に "Required" というラベルが付いています。

すべての印刷プロバイダーは、初期化関数[**Initializeprintプロビジョニング Dor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintprovidor)をエクスポートする必要があります。 他のすべての関数へのポインターは、 [**Print、または**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_printprovidor)構造体で指定する必要があります。 (これらの2つの名前はスペルが間違っていますが、ヘッダーファイルに表示されている名前と一致していることに注意してください。

関数はグループに分割され、次のセクションに示されています。

初期化関数

印刷キュー管理関数

プリンタードライバー管理機能

印刷ジョブの作成関数

印刷ジョブのスケジュール関数

フォーム管理関数

プリントプロセッサ管理関数

印刷モニターの管理機能

ポート管理関数

レジストリ管理関数

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintprovidor" data-raw-source="[&lt;strong&gt;InitializePrintProvidor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintprovidor)"><strong>Initializeprintプロビジョニング Dor</strong></a> (必須)</p></td>
<td><p>印刷プロバイダーを初期化し、指定された関数へのポインターを返します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-print-queue-management-functions-gg"></a>印刷キュー管理関数

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
<td><p><strong>Interactivesession.addprinter</strong></p></td>
<td><p>印刷プロバイダーによって管理される一覧に印刷キューを追加し、印刷プロセッサを印刷キューに関連付けます。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPrinterConnection</strong></p></td>
<td><p>指定された印刷キューへの接続を作成します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Closeprinter</strong> (必須)</p></td>
<td><p>指定した印刷キューへの呼び出し元のアクセスを無効にします。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeletePrinter</strong></p></td>
<td><p>印刷プロバイダーによって管理されている一覧から印刷キューを削除します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeletePrinterConnection 接続</strong></p></td>
<td><p>指定した印刷キューへの接続を削除します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Enumprinters</strong> (必須)</p></td>
<td><p>印刷プロバイダーによって現在管理されている印刷キューの一覧を列挙します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FindClosePrinterChangeNotification</strong></p></td>
<td><p><strong>FindFirstPrinterChangeNotification</strong>によって有効にされたプリンターの変更通知を無効にします。</p></td>
</tr>
<tr class="even">
<td><p><strong>FindFirstPrinterChangeNotification</strong></p></td>
<td><p>指定されたプリンターイベントを待機するために呼び出し元が使用できる待機オブジェクトへのハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Getprinter</strong> (必須)</p></td>
<td><p>指定された印刷キューの現在のパラメーター値を返します。</p></td>
</tr>
<tr class="even">
<td><p><strong>OpenPrinter</strong> (必須)</p></td>
<td><p>指定した印刷キューへの呼び出し元のアクセスを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff561930(v=vs.85)" data-raw-source="[&lt;strong&gt;RefreshPrinterChangeNotification&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561930(v=vs.85))"><strong>RefreshPrinterChangeNotification</strong></a></p></td>
<td><p>クライアントが<strong>FindNextPrinterChangeNotification</strong>を呼び出した場合 (Microsoft Windows SDK のドキュメントを参照)、PRINTER_NOTIFY_OPTIONS_REFRESH フラグが設定されている場合、ルーターによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>ResetPrinter</strong></p></td>
<td><p>印刷キューのデータ型または<a href="https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)"><strong>Devmodew</strong></a>構造体を変更します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Setprinter</strong> (必須)</p></td>
<td><p>指定された印刷キューのパラメーターを設定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>WaitForPrinterChange</strong></p></td>
<td><p>使われていません。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-printer-driver-management-functions-gg"></a>プリンタードライバー管理機能

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
<td><p><strong>Addプリンタードライバー</strong></p></td>
<td><p>指定されたプリンターのドライバーファイルを指定されたサーバーに追加します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Addプリンター Driverex</strong></p></td>
<td><p><strong>Addプリンタードライバー</strong>と同じですが、パラメーターが追加されています。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Deleteプリンタードライバー</strong></p></td>
<td><p>指定したサーバーで、指定したプリンターのドライバーファイルへのアクセスを削除します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Deleteプリンター Driverex</strong></p></td>
<td><p><strong>Deleteプリンタードライバー</strong>と同じですが、パラメーターが追加されています。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Enumプリンタードライバー</strong></p></td>
<td><p><strong>Addprinter driver</strong>または<strong>Addprinter driverex</strong>を呼び出して、指定されたサーバーに追加されているプリンタードライバーの一覧を返します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Getプリンタードライバー</strong></p></td>
<td><p>プリンタードライバーに関する情報を返します。この情報は、呼び出し元が<strong>Addprinter driver</strong>に渡すことができます。 (通常、返された情報は INF ファイルから取得されます)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Getプリンター Driverex</strong></p></td>
<td><p><strong>Getプリンタードライバー</strong>と同じですが、パラメーターが追加されています。</p></td>
</tr>
<tr class="even">
<td><p><strong>Getプリンター Driverdirectory</strong></p></td>
<td><p>サーバーのプリンタードライバーディレクトリの名前を返します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-print-job-creation-functions-gg"></a>印刷ジョブの作成関数

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
<strong>プリンターの強制</strong>(必須)</td>
<td><p>指定された印刷キューから現在のジョブを削除しようとします。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>Addjob</strong> (必須)</td>
<td><p>ジョブ識別子とスプールファイルパスを返します。 呼び出し元は、 <a href="https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)"><strong>CreateFile</strong></a>と<strong>WriteFile</strong>を使用して、スプールファイルにデータを送信します。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>Enddocprinter</strong> (必須)</td>
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
<strong>Schedulejob</strong> (必須)</td>
<td><p>指定されたジョブをスケジュールできることをプロバイダーに通知します。 このジョブは、 <strong>Addjob</strong>によって以前に返されたジョブ識別子によって指定されます。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>Startdocprinter</strong> (必須)</td>
<td><p>印刷プロバイダーが印刷ジョブのスプールを開始できるように準備します。</p></td>
</tr>
<tr class="even">
<td><p><strong>StartPagePrinter</strong></p></td>
<td><p>印刷プロバイダーに印刷ジョブページを受け取る準備をします。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>Writeprinter</strong> (必須)</td>
<td><p>印刷ジョブのデータストリームの一部を受け取ります。</p></td>
</tr>
</tbody>
</table>

 

**Addjob**   に**注意**してください...**Schedulejob**シーケンスは、 **startdocprinter**の代替手段です...**Enddocprinter**シーケンス。

 

### <a href="" id="ddk-print-job-scheduling-functions-gg"></a>印刷ジョブのスケジュール関数

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
<strong>Enumjobs</strong> (必須)</td>
<td><p>スケジュールされた印刷ジョブの一覧を返します。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>Getjob</strong> (必須)</td>
<td><p>ジョブのパラメーターを返します。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>Setjob</strong> (必須)</td>
<td><p>印刷ジョブをキャンセル、一時停止、再開、または再起動するか、ジョブパラメーターを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-forms-management-functions-gg"></a>フォーム管理関数

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
<td><p>指定したプリンターで使用できるフォームの一覧に、指定したフォームを追加します。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeleteForm</strong></p></td>
<td><p>指定したプリンターで使用可能な一覧から、指定したフォームを削除します。</p></td>
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

 

### <a href="" id="ddk-print-processor-management-functions-gg"></a>プリントプロセッサ管理関数

関数の説明**Addprintprocessor**

指定されたサーバーに印刷プロセッサをインストールし、印刷プロバイダーが呼び出すことのできるリストに追加します。

**DeletePrintProcessor**

印刷プロバイダーが呼び出すことができるプリントプロセッサの一覧から、プリントプロセッサを削除します。

**EnumPrintProcessorDataTypes 型**

印刷プロバイダーによって呼び出し可能な、印刷プロセッサによってサポートされるデータ型の一覧を返します。

**EnumPrintProcessors**

印刷プロバイダーが呼び出すことができるプリントプロセッサの一覧を返します。

**GetPrintProcessorDirectory**

印刷プロセッサファイルを格納するディレクトリパスを返します。

 

### <a href="" id="ddk-print-monitor-management-functions-gg"></a>印刷モニターの管理機能

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
<td><p>印刷プロバイダーが呼び出すことのできる一覧に印刷モニターを追加します。</p></td>
</tr>
<tr class="even">
<td><p><strong>DeleteMonitor</strong></p></td>
<td><p>印刷プロバイダーが呼び出すことのできるリストから印刷モニターを削除します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumMonitors</strong></p></td>
<td><p>印刷プロバイダーが呼び出すことのできる印刷モニターの一覧を返します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-port-management-functions-gg"></a>ポート管理関数

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
<td><p>プリンターポートを使用可能な一覧に追加します。通常は、指定したポートモニターの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui" data-raw-source="[&lt;strong&gt;AddPortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui)"><strong>AddPortUI</strong></a>関数を呼び出します。</p></td>
</tr>
<tr class="even">
<td><p><strong>AddPortEx</strong></p></td>
<td><p><strong>Addport</strong>と同じですが、追加のパラメーターがあります。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>ConfigurePort</strong> (必須)</td>
<td><p>プリンターポートを構成します。通常は、指定したポートモニターの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui" data-raw-source="[&lt;strong&gt;ConfigurePortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui)"><strong>ConfigurePortUI</strong></a>関数を呼び出します。</p></td>
</tr>
<tr class="even">
<td><p></p>
<strong>Deleteport</strong> (必須)</td>
<td><p>使用可能なプリンターポートを一覧から削除します。通常は、指定したポートモニターの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-deleteportui" data-raw-source="[&lt;strong&gt;DeletePortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-deleteportui)"><strong>DeletePortUI</strong></a>関数を呼び出します。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<strong>Enumports</strong> (必須)</td>
<td><p>使用可能なプリンターポートの一覧を返します。</p></td>
</tr>
<tr class="even">
<td><p><strong>SetPort</strong></p></td>
<td><p>指定したプリンターポートのパラメーターを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-registry-management-functions-gg"></a>レジストリ管理関数

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
<td><p><strong>Deleteプリンターデータ</strong></p></td>
<td><p>指定したプリンターのプリンター<strong>ドライバーデータ</strong>キーの下にある、指定した値の名前に現在割り当てられている値を削除します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Deleteプリンター Dataex</strong></p></td>
<td><p><strong>Deleteプリンターデータ</strong>と同じですが、追加のパラメーターがあります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Deleteプリンターキー</strong></p></td>
<td><p>指定したプリンターの printer <strong>Driverdata</strong>キーの下にあるレジストリに現在格納されている場合は、指定したキーとそのサブキーを削除します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Enumプリンターデータ</strong></p></td>
<td><p>値の名前と現在割り当てられている値を返します。値は、指定したプリンターのプリンターのプリンター <strong>Driverdata</strong>キーの下にあるレジストリに格納されています。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Enumプリンター Dataex</strong></p></td>
<td><p><strong>Enumプリンターデータ</strong>と同じです。追加のパラメーターがあります。</p></td>
</tr>
<tr class="even">
<td><p><strong>Enumプリンターキー</strong></p></td>
<td><p>指定されたキー名の下にあるレジストリに現在格納されているサブキーの一覧を返します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Getプリンターデータ</strong></p></td>
<td><p>指定された値の名前に現在割り当てられている値を返します。指定されたプリンターのプリンタ<strong>ドライバデータ</strong>キーの下にあるレジストリに格納されています。</p></td>
</tr>
<tr class="even">
<td><p><strong>Getプリンター Dataex</strong></p></td>
<td><p><strong>Getプリンターデータ</strong>と同じですが、パラメーターが追加されています。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Setプリンターデータ</strong></p></td>
<td><p>指定した値の名前と値をレジストリの指定したプリンターのプリンター<strong>ドライバーデータ</strong>キーの下に格納します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Setプリンター Dataex</strong></p></td>
<td><p><strong>Setプリンターデータ</strong>と同じですが、パラメーターが追加されています。</p></td>
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
<td><p><a href="https://docs.microsoft.com/previous-versions/ff564255(v=vs.85)" data-raw-source="[&lt;strong&gt;XcvData&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))"><strong>XcvData</strong></a></p></td>
<td><p>ポートモニターの UI DLL とポート監視サーバーの DLL との間に通信パスを提供します。</p></td>
</tr>
</tbody>
</table>

 

 

 




