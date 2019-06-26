---
title: JavaScript API リファレンス
description: 印刷デバイスを USB 接続経由でサポートを提供するのに Bidi XML ファイルでは、JavaScript API を組み合わせて使用します。
ms.assetid: 604DF74E-AEF1-43DC-81B2-566A94B1CE8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23a7fd4ed3049d0ef6f001925586eff95079b22d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377532"
---
# <a name="javascript-api-reference"></a>JavaScript API リファレンス


製造元は、印刷デバイスを USB 接続経由で双方向のサポートを提供する Bidi XML ファイルと組み合わせて、ここでは、表示、JavaScript API を使用できます。

印刷デバイスとの USB の双方向通信の詳細については、次を参照してください。 [USB Bidi エクステンダー](usb-bidi-extender.md)します。

## <a name="bidi-over-usb"></a>USB 経由での Bidi


## <a name="getschemas-method"></a>getSchemas メソッド


このメソッドは双方向を取得するクエリ処理など\\Printer.Consumables.YellowInk:Level します。 JavaScript コードは、USB バスを使用してプリンターにクエリを行い、応答を読み取るように再びアクセスすることです。

構文

```javascript
function getSchemas(scriptContext, printerStream, schemaRequests, printerBidiSchemaResponses);
```

パラメーター

*scriptContext*

\[\] 、 [ **IPrinterScriptContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptcontext)関連するプロパティ バッグへのアクセスを提供するオブジェクト。
*printerStream*

\[\] 、 [IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)読み取りおよび USB バスへの書き込みアクセスを許可するオブジェクト。
*schemaRequests*

\[\]双方向の要求のクエリ文字列のすべてを含む配列オブジェクト。
*printerBidiSchemaResponses*

\[out\]オブジェクトのクエリ キーをすべての応答を格納する、スクリプトを使用します。
戻り値

| 戻り値 | 説明                                                                                                                                                                             |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | スクリプトが正常に完了しました。                                                                                                                                                      |
| 1            | 要求されたいくつかの情報を提供する接続しているデバイスができていません。 印刷システムがもう一度処理中に追加された任意の Requery キーを使用して関数を呼び出すことを示します。 |



## <a name="setschema-method"></a>setSchema メソッド


このメソッドは、双方向の設定の操作を処理します。 スクリプトは、デバイスでデータを設定するか、クリーンアップと同様に、デバイスで何らかのアクションを実行する受信の Bidi スキーマ値を決定できますヘッドをインクします。

デバイスが、指定されたデータを処理する準備されていない場合は、メソッドは待機期間の後の呼び出しを再試行するかを示す 1 の値を返すことができます。

パラメーター

*scriptContext*

\[\] 、 [ **IPrinterScriptContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptcontext)関連するプロパティ バッグへのアクセスを提供するオブジェクト。
*printerStream*

\[\] 、 [IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)読み取りおよび USB バスへの書き込みアクセスを許可するオブジェクト。
*printerBidiSchemaElement*

\[\] 、 [IPrinterBidiSchemaElement](https://docs.microsoft.com/windows-hardware/drivers/print/iprinterbidischemaelement-interface) Bidi スキーマの値を設定するに関連付けられているすべてのデータを格納しているオブジェクト。
戻り値

| 戻り値 | 説明                                                                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | スクリプトが正常に完了しました。                                                                                                                                                   |
| 1            | 要求されたいくつかの情報を提供する接続しているデバイスができていません。 印刷システムがもう一度指定 printerBidiSchemaElement を使用して関数を呼び出すことを示します。 |



## <a name="getstatus-method"></a>getStatus メソッド


このメソッドは、デバイスが印刷中に、プリンターから要請されていない状態を取得に使用されます。 この関数は印刷時にのみ呼び出されます。 デバイスは、Bidi スキーマの値にこのスクリプトを解釈する読み取りのチャネルでデータを提供する必要があります。 印刷データをデバイスに書き込みチャネルがブロックされているためには、ここでは要請されていない状態のみがサポートします。

このメソッドは、印刷時に繰り返し呼び出されます。 デバイスはデータのみを返す場合、使用可能になるし、スクリプトが理解できると想定されます。 デバイスが要請されていない状態をサポートしていない、またはこの関数を再度呼び出す必要はありません、スクリプトは 2 の値を返す必要があります、 **getStatus**実行スレッドが正常に終了する USBMon でします。

パラメーター

*scriptContext*

\[\] 、 **IPrinterScriptContext**関連するプロパティ バッグへのアクセスを提供するオブジェクト。
*printerStream*

\[\] 、 [IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream) USB バスへの読み取りアクセスを許可するオブジェクト。
*printerBidiSchemaResponses*

\[out\]オブジェクトのクエリ キーをすべての応答を格納する、スクリプトを使用します。
戻り値

| 戻り値 | 説明                                                                                             |
|--------------|---------------------------------------------------------------------------------------------------------|
| 0            | スクリプトが正常に完了しました。                                                                      |
| 2            | 接続しているデバイスが不要になった要請されていない状態をサポートし、この関数が再度呼び出されません。 |



## <a name="startprintjob-method"></a>startPrintJob メソッド


USBMon は、StartDocPort 中にこのメソッドを呼び出します。 呼び出す**startPrintJob**印刷ストリームを変更するか、印刷デバイスのジョブを印刷中に使用するホスト ベースの要求/応答プロトコルを実装するために、ドライバーを使用します。 ジョブのコンテキスト オブジェクトは、製造元の JavaScript コードと永続的なデータ ストリームへのアクセスを取得するジョブのプロパティを管理できるようにする関数に渡されます。 印刷データを処理する JavaScript コードの JavaScript 配列として渡されます。 **startPrintJob**も次の方法でプリンター デバイスへのアクセスを提供します。

-   印刷のストリームを使用して

-   処理する USBMon の Bidi スキーマの応答を返す可能性のあるオブジェクトを使って

構文

```javascript
function startPrintJob(jobScriptContext, printerStream, printerBidiSchemaResponses);
```

パラメーター

*jobScriptContext*

\[\] 、 [ **IPrinterScriptUsbJobContext** ](https://docs.microsoft.com/windows-hardware/drivers/print/iprinterscriptusbjobcontext)ジョブのプロパティ バッグと永続的なデータ ストリームを製造元の JavaScript コードへのアクセスを提供するオブジェクト。
*printerStream*

\[\] 、 **IPrinterScriptableSequentialStream**オブジェクト、製造元の JavaScript コードが、印刷デバイスにデータの読み書きに使用できます。
*printerBidiSchemaResponses*

\[out\] 、 [ **IPrinterBidiSchemaResponses** ](https://docs.microsoft.com/windows-hardware/drivers/print/iprinterbidischemaresponses) Bidi スキーマの値の変更/更新を返す、製造元の JavaScript コードを使用しているオブジェクトします。

| 戻り値 | 説明                                                                             |
|--------------|-----------------------------------------------------------------------------------------|
| 0            | 成功しました。                                                                                |
| 1            | 失敗時-クリーンアップ ジョブのコンテキスト オブジェクトと、印刷スプーラーをエラー コードを返します。 |



## <a name="writeprintdata-method"></a>writePrintData メソッド


USBMon は、writePort 中にこのメソッドを呼び出します。 呼び出す**writePrintData**印刷ストリームを変更するか、印刷デバイスのジョブを印刷中に使用するホスト ベースの要求/応答プロトコルを実装するために、ドライバーを使用します。 ジョブのコンテキスト オブジェクトは、製造元の JavaScript コードと永続的なデータ ストリームへのアクセスを取得するジョブのプロパティを管理できるようにするメソッドに渡されます。 印刷データを処理する JavaScript コードの JavaScript 配列として渡されます。 **writePrintData**も次の方法でプリンター デバイスへのアクセスを提供します。

-   印刷のストリームを使用して

-   処理する USBMon の Bidi スキーマの応答を返す可能性のあるオブジェクトを使って

```javascript
function writePrintData(jobScriptContext, writePrintDataProgress, printData, printerStream, printerBidiSchemaResponses);
```

パラメーター

*jobScriptContext*

\[\] 、 **IPrinterScriptUsbJobContext**ジョブのプロパティ バッグと永続的なデータ ストリームを製造元の JavaScript コードへのアクセスを提供するオブジェクト。
*writePrintDataProgress*

\[\] 、 **IPrinterScriptableSequentialStream**オブジェクト、製造元の JavaScript コードは、印刷デバイスにデータの読み書きに使用できます。
*printData*

\[\] 、 **IDispatch**オブジェクト、現在の印刷データの JavaScript 配列。 *PrintData*パラメーターは、いずれか 1 つのデータ ストリームにキャッシュする前にデータを操作する JavaScript コードを使用できます*jobScriptContext*経由でプリンターに送信したり *。printerStream*します。
*printerStream*

\[\] 、 **IPrinterScriptableSequentialStream**オブジェクト、製造元の JavaScript コードは、印刷デバイスにデータの読み書きに使用できます。
*printerBidiSchemaResponses*

\[out\] 、 **IPrinterBidiSchemaResponses** Bidi スキーマを返す値の変更または更新プログラム、製造元の JavaScript コードを使用しているオブジェクトします。
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
<td>成功しました。 印刷データ ストリームからバイト数の処理 (<em>printData</em>) 経由で返されます<em>writePrintDataProgress</em>します。</td>
</tr>
<tr class="even">
<td>1</td>
<td>失敗時-印刷スプーラーには、エラー コードを返します。</td>
</tr>
<tr class="odd">
<td>2</td>
<td><p>再試行 - (Bidi イベントを含む) における Bidi スキーマ更新プログラムで処理<em>printerBidiSchemaResponses</em>、データの処理を続行する製造元のコードを許可するには、もう一度 JavaScript 関数を呼び出します。</p>
<p>印刷データ ストリームからバイト数の処理 (<em>printData</em>) 経由で返されます<em>writePrintDataProgress</em>します。</p></td>
</tr>
<tr class="even">
<td>3</td>
<td><p>DeviceBusy – デバイスの通信チャネルを受け入れていませんデータこの時点で。 これは、操作では、エラーは示されません。 USBMon は、デバイスがビジー状態でと、後でもう一度、関数を呼び出す、スプーラーを知らせる必要があります。</p>
<p>印刷データ ストリームからバイト数の処理 (<em>printData</em>) 経由で返されます<em>writePrintDataProgress</em>します。</p></td>
</tr>
<tr class="odd">
<td>4</td>
<td>AbortTheJob – デバイスを続行できません、ジョブを処理または、ユーザーが印刷デバイスの前面パネルを使用してジョブをキャンセルします。 USBMon では、印刷ジョブを中止するメッセージを受信したときに、印刷スプーラーを返す前に、ジョブを中止する情報を渡します。</td>
</tr>
</tbody>
</table>



## <a name="endprintjob-method"></a>endPrintJob メソッド


USBMon は、endDocPort 中にこのメソッドを呼び出します。 呼び出す**endPrintJob**印刷ストリームを変更するか、印刷デバイスのジョブを印刷中に使用するホスト ベースの要求/応答プロトコルを実装するために、ドライバーを使用します。 ジョブ コンテキスト オブジェクトは、製造元の JavaScript コードを許可するメソッドに渡されます。

-   印刷データが永続化の処理が完了します。

-   印刷のストリームを使用してプリンター デバイスへのアクセスします。

-   応答を処理する USBMon Bidi スキーマを渡すことができるオブジェクトへのアクセスします。

```javascript
function endPrintJob(jobScriptContext, printerStream, printerBidiSchemaResponses);
```

パラメーター

*jobScriptContext*

\[\] An IPrinterScriptUsbJobContext オブジェクト、ジョブのプロパティ バッグと永続的なデータ ストリームに、製造元の JavaScript コードのアクセスです。
*printerStream*

\[\]製造元の JavaScript コードは、印刷デバイスにデータの読み書きに使用できる、IPrinterScriptableSequentialStream オブジェクト。
*printerBidiSchemaResponses*

\[out\] An IPrinterBidiSchemaResponses オブジェクト、製造元の JavaScript コードが、Bidi スキーマを返す値の変更または更新プログラムを使用できます。

| 戻り値 | 説明                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 成功時-クリーンアップ ジョブのコンテキスト オブジェクトと、印刷スプーラーを戻り値の成功します。                                                                                                                                         |
| 1            | 失敗時-クリーンアップ ジョブのコンテキスト オブジェクトと、印刷スプーラーをエラー コードを返します。                                                                                                                                   |
| 2            | 再試行 - (Bidi イベントを含む) における Bidi スキーマ更新プログラムで処理*printerBidiSchemaResponses*、データの処理を続行する製造元の JavaScript コードを許可するには、もう一度 JavaScript 関数を呼び出します。 |



## <a name="bidi-over-secondary-usb"></a>セカンダリ USB 経由での Bidi


デバイスが、セカンダリの USB インターフェイスをサポートしているデバイスを使用できるかどうか、 **getSchemas**と**setSchema**に加え、前のセクションで説明した方法、 **requestStatus**メソッド。

## <a name="requeststatus-method"></a>requestStatus メソッド


代わりにこのメソッドが呼び出されます**getStatus**場合、 **BidiUSBStatusInterface** v4 ドライバーのマニフェスト ファイルでディレクティブが指定されています。 **requestStatus**デバイスが印刷中に、印刷デバイスからステータスを取得するために使用します。

次の図は、シナリオを示す双方向の USB 拡張機能のアーキテクチャの概要を**BidiUSBStatusInterface**ディレクティブが指定されており、別の USB 経由で通信がルーティングされるためインターフェイスです。

![requeststatus メソッドを使用した usb bidi エクステンダーのアーキテクチャ](images/usbbidiext-arch2.png)

このメソッドは、印刷時に繰り返し呼び出されます。 デバイスはデータのみを返す場合、使用可能になるし、スクリプトが理解できると想定されます。 デバイスが要請された状態をサポートしていない、またはこのメソッドをもう一度呼び出す必要はありません、スクリプトは 2 の値を返す必要があります、 **getStatus**実行スレッドが正常に終了する USBMon でします。

パラメーター

*scriptContext*

\[\] 、 **IPrinterScriptContext**関連するプロパティ バッグへのアクセスを提供するオブジェクト。
*printerStream*

\[\] 、 **IPrinterScriptableSequentialStream**読み取りおよび USB バスへの書き込みアクセスを許可するオブジェクト。
*printerBidiSchemaResponses*

\[out\]オブジェクトのクエリ キーをすべての応答を格納する、スクリプトを使用します。
戻り値

| 戻り値 | 説明                                                                                           |
|--------------|-------------------------------------------------------------------------------------------------------|
| 0            | スクリプトが正常に完了しました。                                                                    |
| 2            | 接続しているデバイスが不要になった要請された状態をサポートし、この関数が再度呼び出されません。 |



## <a name="related-topics"></a>関連トピック
[**IPrinterScriptContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptcontext)  
[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)  
[USB Bidi エクステンダー](usb-bidi-extender.md)  



