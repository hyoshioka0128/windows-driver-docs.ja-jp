---
title: JavaScript API リファレンス
description: JavaScript API と Bidi XML ファイルを組み合わせて使用して、印刷デバイスへの USB 接続をサポートします。
ms.assetid: 604DF74E-AEF1-43DC-81B2-566A94B1CE8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a4c46ecc767bdb45718e39e2e25bf818b1bc107
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828932"
---
# <a name="javascript-api-reference"></a>JavaScript API リファレンス


製造元は、ここに記載されている JavaScript API を Bidi XML ファイルと組み合わせて使用して、印刷デバイスへの USB 接続を介した Bidi のサポートを提供できます。

印刷デバイスとの USB Bidi 通信の詳細については、「 [Usb Bidi Extender](usb-bidi-extender.md)」を参照してください。

## <a name="bidi-over-usb"></a>Bidi over USB


## <a name="getschemas-method"></a>getSchemas メソッド


このメソッドは、\\YellowInk: Level などの Bidi GET クエリを処理します。 JavaScript コードは、USB バスを使用してプリンターに対してクエリを実行し、応答が返されたときに応答を読み取ることができます。

構文

```javascript
function getSchemas(scriptContext, printerStream, schemaRequests, printerBidiSchemaResponses);
```

パラメーター

*Scriptcontext.echo*

関連するプロパティバッグへのアクセスを提供する[**Iプリンター Scriptcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)オブジェクトを\] に \[します。
*プリンターストリーム*

USB バスへの読み取りおよび書き込みアクセスを許可する[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)オブジェクト\] の \[ます。
*schemaRequests*

要求されたすべての Bidi クエリ文字列を含む\] 配列オブジェクトの \[。
*printerBidiSchemaResponses*

スクリプトがクエリキーへのすべての応答を格納するために使用する\] オブジェクトを \[します。
戻り値

| 戻り値 | 説明                                                                                                                                                                             |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | スクリプトは正常に完了しました。                                                                                                                                                      |
| 1            | アタッチされたデバイスは、要求された情報を提供する準備ができていませんでした。 処理中に追加された再クエリキーを使用して、印刷システムが関数を再度呼び出す必要があることを示します。 |



## <a name="setschema-method"></a>setSchema メソッド


このメソッドは、Bidi の設定操作を処理します。 このスクリプトでは、着信 Bidi スキーマ値を決定して、デバイスにデータを設定したり、デバイスで何らかのアクション (クリーンインクヘッドなど) を実行したりすることができます。

デバイスが指定されたデータを処理する準備ができていない場合、メソッドは値1を返すことができます。これは、待機期間後に呼び出しを再試行する必要があることを示します。

パラメーター

*Scriptcontext.echo*

関連するプロパティバッグへのアクセスを提供する[**Iプリンター Scriptcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)オブジェクトを\] に \[します。
*プリンターストリーム*

USB バスへの読み取りおよび書き込みアクセスを許可する[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)オブジェクト\] の \[ます。
*printerBidiSchemaElement*

設定する Bidi スキーマ値に関連付けられているすべてのデータを含む[IPrinterBidiSchemaElement](https://docs.microsoft.com/windows-hardware/drivers/print/iprinterbidischemaelement-interface)オブジェクト\] で \[します。
戻り値

| 戻り値 | 説明                                                                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | スクリプトは正常に完了しました。                                                                                                                                                   |
| 1            | アタッチされたデバイスは、要求された情報を提供する準備ができていませんでした。 指定された printerBidiSchemaElement を使用して、印刷システムが関数を再度呼び出す必要があることを示します。 |



## <a name="getstatus-method"></a>getStatus メソッド


このメソッドは、デバイスの印刷中にプリンターから要求されていない状態を取得するために使用します。 この関数は、印刷中にのみ呼び出されます。 デバイスは、このスクリプトが Bidi スキーマ値に解釈できる読み取りチャネルにデータを提供する必要があります。 デバイスへの書き込みチャネルは印刷データによってブロックされるため、ここでは要請されていない状態のみがサポートされています。

このメソッドは、印刷中に繰り返し呼び出されます。 使用可能な場合はデバイスがデータを返すだけで、スクリプトではそれを理解できることが想定されています。 デバイスが要請されていない状態をサポートしていない場合、またはこの関数を再度呼び出す必要がない場合、スクリプトは値2を返す必要があります。これにより、 **getStatus**実行スレッドが usbmon で正常に終了するように指示されます。

パラメーター

*Scriptcontext.echo*

関連するプロパティバッグへのアクセスを提供する**Iプリンター Scriptcontext**オブジェクトを\] に \[します。
*プリンターストリーム*

USB バスへの読み取りアクセスを許可する[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)オブジェクト\] の \[ます。
*printerBidiSchemaResponses*

スクリプトがクエリキーへのすべての応答を格納するために使用する\] オブジェクトを \[します。
戻り値

| 戻り値 | 説明                                                                                             |
|--------------|---------------------------------------------------------------------------------------------------------|
| 0            | スクリプトは正常に完了しました。                                                                      |
| 2            | アタッチされたデバイスは、要請されていない状態をサポートしなくなったため、この関数を再度呼び出すことはできません。 |



## <a name="startprintjob-method"></a>startPrintJob メソッド


USBMon は、StartDocPort 中にこのメソッドを呼び出します。 **StartPrintJob**を呼び出すと、ドライバーは印刷ストリームを変更したり、印刷デバイスがジョブを印刷するときに使用されるホストベースの要求/応答プロトコルを実装したりすることができます。 ジョブコンテキストオブジェクトが関数に渡され、製造元の JavaScript コードがジョブのプロパティを管理し、永続データストリームにアクセスできるようにします。 印刷データは、javascript コードが処理するための JavaScript 配列として渡されます。 **startPrintJob**は、次の方法でプリンターデバイスへのアクセスも提供します。

-   印刷ストリーム経由

-   USBMon が処理するための Bidi スキーマ応答を返すことができるオブジェクト経由

構文

```javascript
function startPrintJob(jobScriptContext, printerStream, printerBidiSchemaResponses);
```

パラメーター

*jobScriptContext*

を \[、 [**Iprinterscriptusbjobcontext**](https://docs.microsoft.com/windows-hardware/drivers/print/iprinterscriptusbjobcontext)オブジェクトを\] します。これにより、製造元の JavaScript コードがジョブプロパティバッグと永続データストリームにアクセスできるようになります。
*プリンターストリーム*

製造元の JavaScript コードで印刷デバイスのデータの読み取りと書き込みを行うために使用できる**IPrinterScriptableSequentialStream**オブジェクト\] の \[ます。
*printerBidiSchemaResponses*

製造元の JavaScript コードで Bidi スキーマ値の変更/更新を返すために使用できる[**IPrinterBidiSchemaResponses**](https://docs.microsoft.com/windows-hardware/drivers/print/iprinterbidischemaresponses)オブジェクト\] \[します。

| 戻り値 | 説明                                                                             |
|--------------|-----------------------------------------------------------------------------------------|
| 0            | ブランド.                                                                                |
| 1            | 失敗–ジョブコンテキストオブジェクトをクリーンアップし、エラーコードを印刷スプーラに返します。 |



## <a name="writeprintdata-method"></a>writePrintData メソッド


USBMon は、writePort 中にこのメソッドを呼び出します。 **Writeprintdata**を呼び出すと、ドライバーは印刷ストリームを変更したり、印刷デバイスがジョブを印刷している間に使用されるホストベースの要求/応答プロトコルを実装したりすることができます。 ジョブコンテキストオブジェクトはメソッドに渡され、製造元の JavaScript コードがジョブのプロパティを管理し、永続データストリームにアクセスできるようにします。 印刷データは、javascript コードが処理するための JavaScript 配列として渡されます。 **Writeprintdata**は、次の方法でプリンターデバイスへのアクセスも提供します。

-   印刷ストリーム経由

-   USBMon が処理するための Bidi スキーマ応答を返すことができるオブジェクト経由

```javascript
function writePrintData(jobScriptContext, writePrintDataProgress, printData, printerStream, printerBidiSchemaResponses);
```

パラメーター

*jobScriptContext*

を \[、 **Iprinterscriptusbjobcontext**オブジェクトを\] します。これにより、製造元の JavaScript コードがジョブプロパティバッグと永続データストリームにアクセスできるようになります。
*writePrintDataProgress*

製造元の JavaScript コードが印刷デバイスに対してデータの読み取りと書き込みを行うために使用できる**IPrinterScriptableSequentialStream**オブジェクト\] で \[します。
*printData*

現在の印刷データの JavaScript 配列である**IDispatch**オブジェクト\] で \[ます。 *Printdata*パラメーターを使用すると、JavaScript コードでデータを操作してから、 *jobscriptcontext*内のいずれかのデータストリームにキャッシュするか、またはプリンター*ストリーム*を使用してプリンターに送信することができます。
*プリンターストリーム*

製造元の JavaScript コードが印刷デバイスに対してデータの読み取りと書き込みを行うために使用できる**IPrinterScriptableSequentialStream**オブジェクト\] で \[します。
*printerBidiSchemaResponses*

製造元の JavaScript コードで Bidi スキーマ値の変更または更新を返すために使用できる**IPrinterBidiSchemaResponses**オブジェクト\] \[します。
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>戻り値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>0</td>
<td>ブランド. 印刷データストリームから処理されたバイト数 (<em>printdata</em>) は、 <em>Writeprintdataprogress</em>を通じて返されます。</td>
</tr>
<tr class="even">
<td>1</td>
<td>失敗–印刷スプーラにエラーコードを返します。</td>
</tr>
<tr class="odd">
<td>2</td>
<td><p>再試行- <em>printerBidiSchemaResponses</em>の bidi スキーマ更新 (bidi イベントを含む) をすべて処理してから、JavaScript 関数を再度呼び出して、製造元のコードがデータの処理を続行できるようにします。</p>
<p>印刷データストリームから処理されたバイト数 (<em>printdata</em>) は、 <em>Writeprintdataprogress</em>を通じて返されます。</p></td>
</tr>
<tr class="even">
<td>3</td>
<td><p>DeviceBusy –デバイスの通信チャネルは、現時点ではデータを受け入れていません。 これはエラーを示すものではありません。 USBMon は、デバイスがビジー状態であることをスプーラに知らせ、後で再び関数を呼び出します。</p>
<p>印刷データストリームから処理されたバイト数 (<em>printdata</em>) は、 <em>Writeprintdataprogress</em>を通じて返されます。</p></td>
</tr>
<tr class="odd">
<td>ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td>ジョブのキャンセル–デバイスはジョブの処理を続行できません。または、ユーザーが印刷デバイスの前面パネルを使用してジョブを取り消しました。 USBMon は、印刷ジョブを中止するためのメッセージを受信すると、ジョブを中止するために情報を印刷スプーラに渡してから制御を戻します。</td>
</tr>
</tbody>
</table>



## <a name="endprintjob-method"></a>endPrintJob メソッド


USBMon は、endDocPort 中にこのメソッドを呼び出します。 **EndPrintJob**を呼び出すと、ドライバーは印刷ストリームを変更したり、印刷デバイスがジョブを印刷するときに使用されるホストベースの要求/応答プロトコルを実装したりすることができます。 ジョブコンテキストオブジェクトがメソッドに渡され、製造元の JavaScript コードで次のことを行うことができます。

-   保存されているすべての印刷データの処理を完了する

-   印刷ストリーム経由でプリンターデバイスにアクセスする

-   USBMon に対する Bidi スキーマ応答を渡すことができるオブジェクトへのアクセス

```javascript
function endPrintJob(jobScriptContext, printerStream, printerBidiSchemaResponses);
```

パラメーター

*jobScriptContext*

を \[、IPrinterScriptUsbJobContext オブジェクトを\] します。これにより、製造元の JavaScript コードがジョブプロパティバッグと永続データストリームにアクセスできるようになります。
*プリンターストリーム*

製造元の JavaScript コードが印刷デバイスに対してデータの読み取りと書き込みを行うために使用できる IPrinterScriptableSequentialStream オブジェクト\] で \[します。
*printerBidiSchemaResponses*

製造元の JavaScript コードで Bidi スキーマ値の変更または更新を返すために使用できる IPrinterBidiSchemaResponses オブジェクト\] \[します。

| 戻り値 | 説明                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 成功–ジョブコンテキストオブジェクトをクリーンアップし、印刷スプーラに成功を返します。                                                                                                                                         |
| 1            | 失敗–ジョブコンテキストオブジェクトをクリーンアップし、エラーコードを印刷スプーラに返します。                                                                                                                                   |
| 2            | 再試行- *printerBidiSchemaResponses*の bidi スキーマ更新 (bidi イベントを含む) をすべて処理してから、javascript 関数を再度呼び出して、製造元の javascript コードがデータの処理を続行できるようにします。 |



## <a name="bidi-over-secondary-usb"></a>セカンダリ USB 経由の Bidi


デバイスでセカンダリ USB インターフェイスがサポートされている場合、デバイスは、 **Requeststatus**メソッドに加えて、前のセクションで説明した**Getschemas**および**setschema**メソッドを使用できます。

## <a name="requeststatus-method"></a>requestStatus メソッド


このメソッドは、 **getStatus**ではなく、 **Bidiusbstatusinterface**ディレクティブが v4 ドライバーのマニフェストファイルで指定されている場合に呼び出されます。 **Requeststatus**は、デバイスの印刷中に印刷デバイスから状態を取得するために使用されます。

次の図は、USB Bidi 拡張アーキテクチャの概要を示しています。これは、 **Bidiusbstatusinterface**ディレクティブが指定されていて、通信が代替の usb インターフェイスを経由してルーティングされるシナリオを示しています。

![requeststatus メソッドを使用した usb bidi エクステンダーアーキテクチャ](images/usbbidiext-arch2.png)

このメソッドは、印刷中に繰り返し呼び出されます。 使用可能な場合はデバイスがデータを返すだけで、スクリプトではそれを理解できることが想定されています。 デバイスが要請された状態をサポートしていない場合、またはこのメソッドを再度呼び出す必要がない場合、スクリプトは値2を返す必要があります。これにより、 **getStatus**実行スレッドが usbmon で正常に終了するように指示されます。

パラメーター

*Scriptcontext.echo*

関連するプロパティバッグへのアクセスを提供する**Iプリンター Scriptcontext**オブジェクトを\] に \[します。
*プリンターストリーム*

USB バスへの読み取りおよび書き込みアクセスを許可する**IPrinterScriptableSequentialStream**オブジェクト\] の \[ます。
*printerBidiSchemaResponses*

スクリプトがクエリキーへのすべての応答を格納するために使用する\] オブジェクトを \[します。
戻り値

| 戻り値 | 説明                                                                                           |
|--------------|-------------------------------------------------------------------------------------------------------|
| 0            | スクリプトは正常に完了しました。                                                                    |
| 2            | アタッチされたデバイスは、要請された状態をサポートしなくなったため、この関数を再度呼び出すことはできません。 |



## <a name="related-topics"></a>関連トピック
[**Iプリンター Scriptcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)  
[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)  
[USB Bidi Extender](usb-bidi-extender.md)  



