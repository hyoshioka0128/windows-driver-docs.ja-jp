---
title: JavaScript 制約
description: V4 プリンタードライバーモデルは、v3 IPrintOemPrintTicketProvider インターフェイスから派生した拡張制約と PrintTicket の処理をサポートしています。
ms.assetid: CD2EF726-CF0F-4BB6-9F41-794699568F17
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2cfcd6c317606eba2765e52661fe11f03c5ff5f7
ms.sourcegitcommit: 581fb777a2376854ca12e767d366e2cb79724b73
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84461835"
---
# <a name="javascript-constraints"></a>JavaScript 制約

V4 プリンタードライバーモデルでは、v3 [IPrintOemPrintTicketProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)インターフェイスから派生した拡張制約と PrintTicket 処理の新しいモデルがサポートされています。

ただし、コンパイル済みの構成プラグインを使用する代わりに、v4 プリンタードライバーは javascript を使用して JavaScript 制約と呼ばれる Api を実装します。また、必要に応じて、プリンタードライバーが1つ以上の Api を実装できます。 詳細については、このトピックの最後にある「 **JavaScript 制約 api**の関数」を参照してください。

JavaScript の制約を使用すると、PrintCapabilities を補強し、PrintTickets を検証し、PrintTicket から DEVMODE への変換や、その逆の処理を行うことができます。 ただし、JavaScript の制約にはいくつかの制限があります。 主な制限事項の一覧を次に示します。

- CompletePrintCapabilities を使用して追加された機能とオプション、および validatePrintTicket に指定された制約は、[デスクトッププリンターの設定] ウィンドウに表示されません。

- CompletePrintCapabilities を使用して追加された機能とオプションは、パブリック DEVMODE には保存されません。

- JavaScript の制約では、リソース dll から言語リソースにアクセスして、追加された機能とオプションまたはパラメーターをローカライズすることはできません。

そのため、JavaScript の制約は、適切な場所でのみ使用することをお勧めします。 機能とオプションは、可能であれば GPD ファイルまたは PPD ファイルで指定する必要があります。また、JavaScript では、複雑な制約のみを表す必要があります。

## <a name="debugging-javascript-files"></a>JavaScript ファイルのデバッグ

JavaScript ファイルの基本的な構文検証は、Windows ベースのスクリプトホストで JavaScript ファイルを開くことによってサポートされます。 これを行うには、JavaScript ファイルを右クリックし、[ファイルを**開くアプリケーション**の選択] を選択して、一覧の [Windows ベースのスクリプトホスト] エントリを選択します。 エラーがスローされなかった場合は、JavaScript の構文が有効になります。 それ以外の場合は、次のスクリーンショットに示すように、問題の行番号が示されます。

![javascript 構文エラーダイアログ](images/script-host-err.png)

一般公開されている JavaScript 検証ツールは、JavaScript ファイルのスタイルを評価する際の支援として有益な場合もあります。

対話型デバッグを有効にするには、次のレジストリキーを作成します。

**キー名:** HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Control \\ Print

**値の名前:** EnableJavaScriptDebugging

**型:** DWORD

**値:** 1

ただし、 *Printconfig .dll*は頻繁に読み込まれ、アンロードされるため、印刷するアプリのデバッグは、推奨されるテスト/デバッグ戦略ではありません。 代わりに、製造元は、 [PTGetPrintCapabilities](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptgetprintcapabilities)、 [ptconvertdevmodetoprintticket](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertdevmodetoprintticket)、 [PTConvertPrintTicketToDevMode](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertprinttickettodevmode)、 [ptmergeandvalidateprintticket](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)というパブリック api を使用して、JavaScript の制約に関連する各エントリポイントを呼び出すテストアプリを構築することをお勧めします。

テストアプリだけではデバッグを有効にすることができますが、ドライバー全体が PrintTicket、PrintCapabilities、および制約を想定どおりに処理するように単体テストを追加することも有益です。 Visual Studio で単体テストをビルドする方法の詳細については、次のトピックを参照してください。

[Visual Studio チームテストを使用した単体テストのチュートリアル](https://docs.microsoft.com/previous-versions/ms379625(v=vs.80))

[Microsoft Visual Studio 2010 および Team Foundation Server を使用した単体テスト](https://channel9.msdn.com/Events/TechEd/Australia/2010/DEV362)

前のテキストに示されているレジストリキーが作成され、ホストプロセスが再起動されると、JavaScript のソースファイルをデバッグできるようになります。

ソースファイルを解析できない場合、デバッガーは呼び出されず、デバッグ環境が失敗したように見えることに注意してください。 ソースファイルの解析に失敗した場合は、「 [Windows スクリプトホスト](https://docs.microsoft.com/previous-versions/9bbdkx3k(v=vs.85))」で、続行する方法の詳細を確認してください。

エラーがなく、ソースファイルが正常に解析された場合は、次のようにソースファイルをデバッグします。

1. テストコンピューターに Microsoft Visual Studio 2012 以降をインストールする

1. 制約 JavaScript コードを含むドライバーを使用して印刷キューを作成する

1. この印刷キューを既定値として設定します。

1. テストアプリまたはアプリを起動して、JavaScript の制約が呼び出されるシナリオを印刷して開始します。 JavaScript の制約に割り込むためには、アプリは PrintTicket/PrintCapabilities Api を呼び出す必要があります。メモ帳などの古いアプリはこれらの Api を呼び出すことはありませんが、XPS ビューアーアプリでは呼び出されます。 このシナリオはより簡単に分離して再現できるため、ここではテストアプリを使用することをお勧めします。

1. 現時点では、"Visual Studio Just-in-time デバッガー" がポップアップ表示され、"アプリでハンドルされない例外が発生しました" という内容が表示されます。 &lt; &gt;

1. Visual Studio 2012 以降の新しいインスタンスを起動します

1. [デバッグ]、[プロセスにアタッチ] の順に選択

1. [プロセスにアタッチ] ダイアログボックスで、[アタッチ先] が [スクリプトコード] に設定されていることを確認します。

1. 次に、テストアプリまたはアプリの印刷を選択し、最後に [アタッチ] を選択します。

1. [すべて中断] をクリックします。

1. 次に、[Visual Studio Just-in-time デバッガー] ダイアログに戻り、[いいえ] をクリックします。

1. Visual Studio は、現在のテストによって呼び出された場所でデバッガーを中断します。 コードを正常にデバッグできるようになりました。

## <a name="javascript-constraint-apis"></a>JavaScript 制約 Api

このセクションでは、JavaScript 制約ファイルで使用する API エントリポイントとして機能する関数を指定します。 関数は次のとおりです。

- validatePrintTicket

- completePrintCapabilities

- convertDevModeToPrintTicket

- convertPrintTicketToDevMode

## <a name="validateprintticket-function"></a>validatePrintTicket 関数

この API は、特定のプリンターに対して PrintTicket オブジェクトが有効であることを検証するために呼び出されます。 これは、 [**IPrintOemPrintTicketProvider:: ValidatePrintTicket**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553184(v=vs.85)) API に似ています。

**構文**

```javascript
function validatePrintTicket(printTicket, scriptContext)
```

**パラメーター**

- *printTicket*

  \[\] \[ \] 検証対象の[**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)オブジェクト。

- *Scriptcontext.echo*

  \[\]ドライバープロパティバッグへのアクセスを提供する[**Iプリンター scriptcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)オブジェクト、キュープロパティバッグ、およびユーザープロパティバッグ。

**戻り値**

| 戻り値 | 説明 |
| --- | --- |
| 0 | *PrintTicket*パラメーターが無効であり、修正できなかったことを示します。 E の[ \_ PRINTTICKET \_ 形式](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)に相当します。 |
| 1 | *Printticket*パラメーターがこのプリンターの有効な printticket であることを示します。 [S PT と \_ は \_ \_ 競合しません](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)。 |
| 2 | *PrintTicket*パラメーターが有効になるように変更されたことを示します。 [S \_ PT \_ CONFLICT \_ ](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)と同じように解決されます。 |

## <a name="completeprintcapabilities-function"></a>completePrintCapabilities 関数

この API は、PrintCapabilities オブジェクトを変更できるようにするために呼び出されます。 これは、条件付き機能 (たとえば、縁なしの画像でのみサポートされます) や、GPD または PPD ファイル (入れ子になった機能の定義など) によって生成できなかった機能を表す場合に使用します。 これは、 [**IPrintOemPrintTicketProvider:: CompletePrintCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-completeprintcapabilities) API に似ています。

**構文**

```javascript
function completePrintCapabilities(printTicket, scriptContext, printCapabilities)
```

**パラメーター**

- *printTicket*

  \[\]生成された PrintCapabilities ドキュメントを制限するための[**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)オブジェクト入力。

- *Scriptcontext.echo*

  \[\]ドライバープロパティバッグへのアクセスを提供する[**Iプリンター scriptcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)オブジェクト、キュープロパティバッグ、およびユーザープロパティバッグ。

- *printCapabilities*

  \[ここでは、 \] \[ \] 構成モジュールによって生成された基本 PrintCapabilities オブジェクトを表す[**Iprintschemacapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemacapabilities)オブジェクトを示します。

**戻り値**

[なし] :

## <a name="convertdevmodetoprintticket-function"></a>convertDevModeToPrintTicket 関数

この API は、DEVMODE プロパティバッグから PrintTicket に値を変換するために呼び出されます。 これは、 [**IPrintOemPrintTicketProvider:: ConvertDevModeToPrintTicket**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553161(v=vs.85)) API に似ていますが、この実装では devmode のプライベートセクションを[**Iプリンター scriptablepropertybag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablepropertybag)オブジェクトにカプセル化し、devmode のパブリックセクションにアクセスできない点が異なります。

**構文**

```javascript
function convertDevModeToPrintTicket(devModeProperties, scriptContext, printTicket)
```

**パラメーター**

- *devModeProperties*

\[\]DEVMODE プロパティバッグを表す**Iプリンター Scriptablepropertybag**オブジェクト。

- *Scriptcontext.echo*

  \[\]ドライバープロパティバッグへのアクセスを提供する[**Iプリンター scriptcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)オブジェクト、キュープロパティバッグ、およびユーザープロパティバッグ。

- *printTicket*

  \[ここでは、 \] \[ \] PrintTicket を表す[**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)オブジェクト。

**戻り値**

[なし] :

## <a name="convertprinttickettodevmode-function"></a>convertPrintTicketToDevMode 関数

この API は、PrintTicket の値を DEVMODE プロパティバッグに変換するために呼び出されます。 これは[**IPrintOemPrintTicketProvider:: ConvertPrintTicketToDevMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode) API に似ていますが、この実装では devmode のプライベートセクションを**i scriptablepropertybag**オブジェクトにカプセル化し、devmode のパブリックセクションにアクセスできない点が異なります。

**構文**

```javascript
function convertPrintTicketToDevMode(printTicket, scriptContext, devModeProperties)
```

**パラメーター**

- *printTicket*

  \[\]変換される PrintTicket を表す**IPrintSchemaTicket**オブジェクト。

- *Scriptcontext.echo*

  \[\]ドライバープロパティバッグへのアクセスを提供する**Iプリンター scriptcontext**オブジェクト、キュープロパティバッグ、およびユーザープロパティバッグ。

- *devModeProperties*

  \[では、 \] \[ \] DEVMODE プロパティバッグを表す**Iプリンター scriptablepropertybag**オブジェクトを出力します。

**戻り値**

[なし] :

## <a name="constraint-best-practices"></a>制約のベストプラクティス

Windows 8 の [印刷] ダイアログと印刷設定エクスペリエンスでサポートされるのは、Print Schema Keywords 名前空間のサブセットのみです。 このため、Microsoft では、Windows 8 の [印刷] ダイアログボックスでサポートされている機能と、その UI に含まれていない機能の間に制約を使用しないことをお勧めします。これは、ユーザーがこのような制約を解決する機会がないためです。

たとえば、Photo という PageMediaType オプションが PageResolution 値 1200 dpi でのみ機能するように制約されている場合、ユーザーは写真メディアの種類を選択できません。 このような場合は、ユーザーの意図 (写真メディア) を一致させ、この問題を発生させるために必要な設定を調整することをお勧めします。 これらの調整は、JavaScript の制約コードで行うことができます。

ドライバーが JavaScript の制約を使用しない場合、ファイルが提供される必要はありません。 ドライバーがエントリポイントのサブセット (validatePrintTicket など) に対してのみ JavaScript 制約を使用する場合、他のエントリポイントはすべて JavaScript ファイルから完全に省略する必要があります。

JavaScript 制約の使用方法の詳細については、「 [Print driver constraints サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/print-driver-constraints-sample)」を参照してください。
