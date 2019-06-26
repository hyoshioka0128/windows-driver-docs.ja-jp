---
title: JavaScript 制約
description: V3 IPrintOemPrintTicketProvider インターフェイスから派生した PrintTicket の処理を v4 プリンター ドライバー モデルは、拡張の制約をサポートします。
ms.assetid: CD2EF726-CF0F-4BB6-9F41-794699568F17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26dae5178f80192a3d0b4abfea23514bd08ed126
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377530"
---
# <a name="javascript-constraints"></a>JavaScript 制約


V4 プリンター ドライバー モデルは、拡張の制約の新しいモデルをサポートしているし、PrintTicket の処理は、v3 から派生した[IPrintOemPrintTicketProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintoemprintticketprovider)インターフェイス。

ただし、プラグインのコンパイル済みの構成を使用してではなく v4 プリンター ドライバーでは、JavaScript を使用して、JavaScript の制約が呼び出される Api を実装して、プリンター ドライバーは、1 つ以上の必要に応じてそれらを実装できます。 詳細については、内の関数を参照してください、 **JavaScript 制約 Api**このトピックの最後のセクション。

PrintCapabilities の強化、PrintTickets を検証して PrintTicket DEVMODE、またはその逆の変換を処理する JavaScript の制約を使用できます。 ただし、JavaScript の制約では、いくつかの制限があります。 主な制限事項の一覧を次には。

-   機能と CompletePrintCapabilities を使用して追加のオプションだけでなく validatePrintTicket で指定した制約は、デスクトップのプリンターの基本設定ウィンドウには表示されません。

-   機能と CompletePrintCapabilities を使用して追加のオプションは、パブリックの DEVMODE に永続化されません。

-   JavaScript の制約は、追加された機能とオプションまたはパラメーターをローカライズするリソース dll から言語のリソースにアクセスできません。

そのため、適切な場所にのみ、JavaScript の制約が使用されることをお勧めします。 機能とオプションは、JavaScript では、可能であり、唯一の複雑な制約を表現する必要があります GPD または PPD ファイルで指定する必要があります。

## <a name="debugging-javascript-files"></a>JavaScript ファイルのデバッグ


JavaScript ファイルの基本的な構文の検証は Windows ベースのスクリプト ホストでは、JavaScript ファイルを開くことでサポートされています。 これを行うには、JavaScript ファイルを右クリックして**プログラムから開く**、Windows ベースの一覧のエントリをスクリプト ホストを選択します。 エラーがスローされない場合、JavaScript は構文が無効です。 それ以外の場合、次のスクリーン ショットに示すように、問題の行番号を指摘にされます。

![javascript 構文エラー ダイアログ](images/script-host-err.png)

公開されている JavaScript の検証ツールは、JavaScript ファイルのスタイルを評価する際に、サポート機能として役に立つ場合もあります。

次のレジストリ キーを作成して対話形式デバッグを有効にすることができます。

**キー名:** HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\印刷

**値の名前:** EnableJavaScriptDebugging

**種類:** DWORD

**値:** 1

ただし、 *PrintConfig.dll*が読み込まれ、出力するアプリのデバッグに多くの場合、アンロードはテストおよびデバッグの推奨される戦略ではありません。 代わりに、Microsoft では、製造元がこれらのパブリック Api を使用して、JavaScript の制約に関連するエントリ ポイントの各を呼び出すテスト アプリを構築することお勧めします。[PTGetPrintCapabilities](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptgetprintcapabilities)、 [PTConvertDevModeToPrintTicket](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertdevmodetoprintticket)、 [PTConvertPrintTicketToDevMode](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertprinttickettodevmode)、および[PTMergeAndValidatePrintTicket](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)します。

テスト アプリだけでは、デバッグを有効にするだけで十分ですも全体のドライバーが PrintTicket、PrintCapabilities と期待どおりに制約を処理していることを確認する単体テストを追加します。 Visual Studio の単体テストを構築する方法の詳細については、次のトピックを参照してください。

[単体テストを Visual Studio チーム テストのチュートリアル](https://docs.microsoft.com/previous-versions/ms379625(v=vs.80))

[Microsoft Visual Studio 2010 および Team Foundation Server での単体テスト](https://channel9.msdn.com/Events/TechEd/Australia/2010/DEV362)

上記のテキストに示すようにレジストリ キーが作成され、ホスト プロセスが再起動されて後、は、JavaScript ソース ファイルをデバッグできます。

ソース ファイルを解析できない場合、デバッガーは呼び出されませんし、デバッグ環境が失敗したかのように思われるは場合に重要です。 ソース ファイルの解析に失敗するを参照してください。 [Windows Script Host](https://docs.microsoft.com/previous-versions/9bbdkx3k(v=vs.85))続行する方法の詳細について。

エラーがないソース ファイルが正常に解析された場合は、次のように、ソース ファイルをデバッグします。

1. Microsoft Visual Studio 2012、または後で、テスト コンピューターにインストールします。

2. 制約の JavaScript コードが含まれているドライバーを使用して印刷キューを作成します。

3. この印刷キューは、既定値として設定します。

4. アプリのテストまたは出力し、呼び出される JavaScript 制約が原因となるシナリオを開始するアプリを起動します。 JavaScript 制約; に分割するために、アプリが PrintTicket と PrintCapabilities Api を呼び出す必要があります。メモ帳などの古いアプリはこれらの Api を呼び出さないでくださいが、XPS ビューアー アプリは。 シナリオをより簡単に分離して再現するために、マイクロソフトは、ここでは、テスト アプリの使用を推奨します。

5. この時点で、「Visual Studio Just-In-Time デバッガー」がポップアップ表示という"でハンドルされない例外が発生しました&lt;アプリ&gt;"。

6. Visual Studio 2012 またはそれ以降の新しいインスタンスを起動します。

7. デバッグを選択し、プロセスにアタッチします。

8. ダイアログのプロセスにアタッチ、ことを確認する接続先: スクリプト コードに設定されています。

9. テスト アプリまたはアプリの印刷を選択するようになりましたし、最後にアタッチ をクリックしてください

10. "すべて中断 をクリックします。

11. 今すぐ「Visual Studio Just-In-Time デバッガー」ダイアログに戻り、[いいえ] をクリックします

12. Visual Studio は、現在のテストに呼び出される場所でデバッガーに中断されます。 通常、コードをデバッグすることがありますようになりました。

## <a name="javascript-constraint-apis"></a>制約の JavaScript Api


このセクションでは、制約の JavaScript ファイルで使用するための API エントリ ポイントとして機能する関数を指定します。 関数は、次に示します。

-   ValidatePrintTicket
-   completePrintCapabilities
-   ConvertDevModeToPrintTicket
-   ConvertPrintTicketToDevMode

## <a name="validateprintticket-function"></a>validatePrintTicket 関数


この API は PrintTicket オブジェクトが特定のプリンターに対して有効であることを確認するために呼び出されます。 これは機能的に似ています、 [ **IPrintOemPrintTicketProvider::ValidatePrintTicket** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553184(v=vs.85)) API。

構文

```javascript
function validatePrintTicket(printTicket, scriptContext)
```

パラメーター

*printTicket*

\[\]\[アウト\]、 [ **IPrintSchemaTicket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintschematicket)を検証するオブジェクト。
*scriptContext*

\[\] 、 [ **IPrinterScriptContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptcontext)ドライバーのプロパティ バッグ、キューのプロパティ バッグ、およびユーザーのプロパティ バッグへのアクセスを提供するオブジェクト。
戻り値

| 戻り値 | 説明                                                                                                                                                                                                |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 示します、 *printTicket*パラメーターが無効でありは修正できませんでした。 等価[E\_PRINTTICKET\_形式](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)します。 |
| 1            | 示します、 *printTicket*パラメーターがこのプリンターの有効な PrintTicket します。 等価[S\_PT\_いいえ\_競合](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)します。   |
| 2            | 示します、 *printTicket*パラメーターが有効になるように変更されました。 等価[S\_PT\_競合\_解決済み](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)します。       |

 

## <a name="completeprintcapabilities-function"></a>completePrintCapabilities 関数


この API は PrintCapabilities オブジェクトの変更を許可すると呼ばれます。 これは、条件付きの機能を使用する必要があります (たとえば、ボーダーレスはでのみサポート写真紙) または GPD または PPD ファイル (たとえば、入れ子になった機能の定義) を生成できませんでした機能を表します。 これは機能的に似ています、 [ **IPrintOemPrintTicketProvider::CompletePrintCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-completeprintcapabilities) API。

構文

```javascript
function completePrintCapabilities(printTicket, scriptContext, printCapabilities)
```

パラメーター

*printTicket*

\[\] 、 [ **IPrintSchemaTicket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintschematicket)オブジェクトを生成された PrintCapabilities ドキュメントを制限する入力。
*scriptContext*

\[\] 、 [ **IPrinterScriptContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptcontext)ドライバーのプロパティ バッグ、キューのプロパティ バッグ、およびユーザーのプロパティ バッグへのアクセスを提供するオブジェクト。
*printCapabilities*

\[\]\[アウト\]、 [ **IPrintSchemaCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintschemacapabilities)構成モジュールによって生成された基本 PrintCapabilities オブジェクトを表すオブジェクト。
戻り値

なし。

## <a name="convertdevmodetoprintticket-function"></a>convertDevModeToPrintTicket 関数


この API は、PrintTicket DEVMODE プロパティ バッグからの値に変換すると呼ばれます。 これは機能的に似ています、 [ **IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553161(v=vs.85)) API では、この実装に DEVMODE のプライベート セクションをカプセル化する点を除いて、[ **IPrinterScriptablePropertyBag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablepropertybag)オブジェクトし、対象の DEVMODE のパブリック セクションへのアクセスは許可されません。

構文

```javascript
function convertDevModeToPrintTicket(devModeProperties, scriptContext, printTicket)
```

パラメーター

*devModeProperties*

\[\] 、 **IPrinterScriptablePropertyBag** DEVMODE プロパティ バッグを表すオブジェクト。
*scriptContext*

\[\] 、 [ **IPrinterScriptContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptcontext)ドライバーのプロパティ バッグ、キューのプロパティ バッグ、およびユーザーのプロパティ バッグへのアクセスを提供するオブジェクト。
*printTicket*

\[\]\[アウト\]、 [ **IPrintSchemaTicket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintschematicket) PrintTicket を表すオブジェクト。
戻り値

なし。

## <a name="convertprinttickettodevmode-function"></a>convertPrintTicketToDevMode 関数


この API は、PrintTicket から DEVMODE プロパティ バッグに値を変換すると呼ばれます。 これは機能的に似ています、 [ **IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode) API では、この実装に DEVMODE のプライベート セクションをカプセル化する点を除いて、**IPrinterScriptablePropertyBag**オブジェクトし、対象の DEVMODE のパブリック セクションへのアクセスは許可されません。

構文

```javascript
function convertPrintTicketToDevMode(printTicket, scriptContext, devModeProperties)
```

パラメーター

*printTicket*

\[\] 、 **IPrintSchemaTicket**変換される PrintTicket を表すオブジェクト。
*scriptContext*

\[\] 、 **IPrinterScriptContext**ドライバーのプロパティ バッグ、キューのプロパティ バッグ、およびユーザーのプロパティ バッグへのアクセスを提供するオブジェクト。
*devModeProperties*

\[\]\[アウト\]、 **IPrinterScriptablePropertyBag** DEVMODE プロパティ バッグを表すオブジェクト。
戻り値

なし。

## <a name="constraint-best-practices"></a>制約のベスト プラクティス


Windows 8 の印刷ダイアログ ボックスと印刷設定のエクスペリエンスは、印刷スキーマのキーワード名前空間のサブセットのみをサポートします。 その結果、勧めしませんまたは UI の基本設定を印刷するには、Windows 8 の印刷ダイアログ ボックスでサポートされている機能とユーザーがこのような制約を解決する機会があるないため、その UI にない機能の間の制約を使用します。

たとえば、Photo という PageMediaType オプションが 1200 dpi の PageResolution 値でのみ動作する制約がある場合、ユーザーことはありませんできなく写真メディアの種類を選択します。 このような場合、ユーザーの意図 (写真メディア) と一致し、これが発生するために必要な設定を調整することをお勧めします。 これらの調整は、制約の JavaScript コードにすることができます。

ドライバーが JavaScript の制約を使用しない場合、ファイルが用意されている必要はありません。 場合は、ドライバーは、エントリ ポイント (たとえば、validatePrintTicket) のサブセットのみを JavaScript の制約を使用して、JavaScript ファイルから他のエントリ ポイントを完全省略必要があります。

JavaScript の制約を使用する方法の詳細については、次を参照してください。、[印刷ドライバー制約サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617946)します。

 

 




