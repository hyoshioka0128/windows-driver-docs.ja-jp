---
title: V4 プリンター ドライバー プロパティ バッグ
description: V4 印刷ドライバーモデルは、カスタマイズされた UI アプリケーションからレンダリングプロセスへのデータフローを容易にする多数のプロパティバッグを提供します。
ms.assetid: 4E20303A-BEB3-4928-BA5A-356D978FA2BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51919d93e288268d3456903eaac287b4ffeeb4a9
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653002"
---
# <a name="v4-printer-driver-property-bags"></a>V4 プリンター ドライバー プロパティ バッグ


V4 印刷ドライバーモデルは、カスタマイズされた UI アプリケーションからレンダリングプロセスへのデータフローを容易にする多数のプロパティバッグを提供します。

これらのプロパティバッグを使用すると、カスタマイズされた UI でカスタムプロパティと機能定義を作成し、レンダリングプロセスで使用することができます。 すべてのプロパティバッグは、JavaScript の[**Iプリンター Scriptablepropertybag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablepropertybag)インターフェイスまたは他の環境の[**iプリンター propertybag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterpropertybag)インターフェイスを使用して公開されます。

次の表は、さまざまなコンポーネントを使用して、v4 印刷ドライバーのさまざまな部分からプロパティバッグオブジェクトを取得する方法の概要を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>JavaScript 制約スクリプト</td>
<td>ドライバーとキューのプロパティバッグは、scriptContext パラメーターを使用して JavaScript 制約スクリプトに渡されます。 このパラメーターの型は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext" data-raw-source="[&lt;strong&gt;IPrinterScriptContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)"><strong>Iプリンター Scriptcontext</strong></a>で、子を含んでいます。 driverproperties –は、ドライバープロパティバッグを表します。
QueueProperties –キュープロパティバッグを参照します。
ユーザー–ユーザープロパティバッグ。
DEVMODE プロパティバッグは、DEVMODE &lt;-&gt; PrintTicket 変換メソッドに<em>Devmodeproperties</em>パラメーター ( <strong>Iプリンター scriptablepropertybag</strong>型) として渡されます。 他の方法では使用できません。</td>
</tr>
<tr class="even">
<td>USB Bidi JavaScript</td>
<td>ドライバーとキューのプロパティバッグは、scriptContext パラメーターを使用して、USB Bidi JavaScript スクリプトに渡されます。 このパラメーターの型は<strong>Iプリンター Scriptcontext</strong>で、子を含んでいます。 driverproperties –は、ドライバープロパティバッグを表します。
QueueProperties –キュープロパティバッグを参照します。</td>
</tr>
<tr class="odd">
<td>プリンター拡張アプリ</td>
<td>すべてのプロパティバッグは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs" data-raw-source="[&lt;strong&gt;IPrinterExtensionEventArgs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs)"><strong>Iプリンター Extensioneventargs</strong></a>パラメーターの一部として OnDriverEvent ハンドラーに渡されます。 これらの型はすべて<strong>Iプリンター propertybag</strong>です。 これらは次のように指定されています: DriverProperties –は、ドライバープロパティバッグを参照します。
ユーザー–ユーザープロパティバッグ。
GetProperties () –キュープロパティバッグを参照します。</td>
</tr>
<tr class="even">
<td>UWP デバイスアプリ</td>
<td>すべてのプロパティバッグは、アクティブ化時に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioncontext" data-raw-source="[&lt;strong&gt;IPrinterExtensionContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioncontext)"><strong>Iプリンター Extensioncontext</strong></a>オブジェクトを使用して渡されます。 次のように指定します。 DriverProperties –は、ドライバープロパティバッグを表します。
ユーザー–ユーザープロパティバッグ。
GetProperties () –キュープロパティバッグを参照します。</td>
</tr>
<tr class="odd">
<td>XPS 表示フィルター</td>
<td><p>XPS フィルターは、プロパティ名 "DriverPropertyBag" を使用して、<a href="https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag" data-raw-source="[&lt;strong&gt;Print Filter Pipeline Property Bag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag)"><strong>印刷フィルターパイプラインプロパティバッグ</strong></a>内からドライバープロパティバッグにアクセスできます。または、 <em>filterpipeline. h</em>から XPS_FP_PROPERTY_BAG 定義された値を使用します。 DriverPropertyBag に関する情報を次に示します。</p>
<strong>プロパティの種類:</strong>VT_UNKNOWN <strong>Description:</strong> IUnknown インターフェイスへのポインター。 QueryInterface を呼び出して、ドライバープロパティバッグへの Iプリンター Propertybag インターフェイスへのポインターを取得します。
<p>および XPS フィルターは、プロパティ名 "QueuePropertyBag" を使用して、印刷フィルターパイプラインプロパティバッグ内からキュープロパティバッグにアクセスできます。また、 <em>filterpipeline. h</em>から XPS_FP_QUEUE_PROPERTY_BAG 定義された値を使用することもできます。 QueuePropertyBag に関する情報を次に示します。</p>
<strong>プロパティの種類:</strong>VT_UNKNOWN <strong>Description:</strong> IUnknown インターフェイスへのポインター。 QueryInterface を呼び出して、キュープロパティバッグへの Iプリンター Propertybag インターフェイスへのポインターを取得します。</td>
</tr>
</tbody>
</table>



JavaScript の実装では、プロパティバッグはパラメーターとして渡されます。 プリンター拡張機能アプリケーションでは、プロパティバッグは、アプリケーションを起動するために使用されるイベント引数のメンバーとして渡されます。

COM Iプリンターキュー、Iプリンター Extensioncontext、および Iプリンター Extensioneventargs インターフェイスによって提供されるプロパティバッグアクセサー、および Javascript 実装のプロパティバッグアクセサーは、プロパティバッグが指定されていない場合に例外をスローします。または見つかりません。 さらに、Iプリンター Propertybag インターフェイスの個々のプロパティを照会すると、プロパティが見つからない場合に例外がスローされます。 プロパティが使用できない場合は、try catch ステートメントを使用してクラッシュを回避する必要があります。

## <a name="driver-property-bag"></a>ドライバープロパティバッグ


ドライバーのプロパティバッグは、ドライバーによって読み取り専用で使用されるプロパティまたはデータ blob を事前に定義するドライバーのデータストアです。 V4 マニフェストファイルの "PropertyBag" ディレクティブを使用して指定することができ、実行時に変更することはできません。

Windows Driver Kit には、ドライバープロパティバッグのテンプレートプロジェクトが含まれています。 ドライバーのプロパティバッグは、コンパイル済みのバイナリ blob です。 Visual Studio には、コンパイル済みドライバーのプロパティバッグを生成するためのテンプレートが含まれています。 このテンプレート用に生成された XML ファイルはプロパティバッグではありません。代わりに、このテンプレートのコンパイル済み出力は、v4 マニフェストファイルで指定する必要があるプロパティバッグファイルです。

## <a name="user-property-bag"></a>ユーザープロパティバッグ


ユーザープロパティバッグを使用すると、パートナーはユーザーごとのローカルコンテキストで設定を保存できます。 このプロパティバッグは、ユーザー設定のストレージメカニズムとしてよく使用されます。 このプロパティバッグは、管理者が管理することはできません。また、プリンターの共有中にクライアントとサーバーの間で同期されることもありません。 ユーザープロパティバッグは実行時にのみ設定され、プリンターの拡張機能、UWP デバイスアプリ、および JavaScript の制約でのみ使用できます。

**メモ** JavaScript の制約はユーザーコンテキストの外部でも呼び出される可能性があるため、despooling 中に、ユーザープロパティバッグは現時点では使用できず、Windows は WIN32\_から HRESULT\_を返します (エラー\_\_見つかりません)。



## <a name="devmode-property-bag"></a>DEVMODE プロパティバッグ


Devmode プロパティバッグは、DEVMODE 構造体のプライベートセクションのコンテンツを整理するために使用されます。 ConvertPrintTicketToDevMode の呼び出し中に、JavaScript が呼び出され、DEVMODE プロパティバッグの内容が設定されます。 ConvertDevModeToPrintTicket 呼び出し中に、JavaScript が呼び出され、DEVMODE プロパティバッグから永続化された設定が読み取られ、PrintTicket に格納されます。

このプロパティバッグのサイズは 60 KB 未満に制限されています (正確な量は DEVMODE の割り当て済みセクションのサイズによって異なります)。一部のシナリオでは、データの損失を回避するために DEVMODE 構造体にシリアル化する必要があるためです。 使用できる正確なサイズは、ドライバーごとに異なります。これは、DEVMODE のパブリックセクションのサイズと構成モジュールによって管理されるプライベートセクションのサイズによって決まります。

DEVMODE プロパティバッグは、プロパティバッグのメンバーを指定するために XML ファイルを使用し、convertPrintTicketToDevMode および convertDevModeToPrintTicket Api を使用して変換を処理します。 XML DEVMODE マッピングファイルは、DevModeMap ディレクティブを使用して v4 マニフェストで指定する必要があります。

次のコードスニペットは、DEVMODE プロパティバッグマッピング XML サンプルを示しています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Properties xmlns="https://schemas.microsoft.com/windows/2011/08/printing/devmodemap">
  <Property Name="FabrikamAccountCode">
    <String Length="32"></String>
  </Property>  
</Properties>
```

次のスクリーンショットは、DEVMODE プロパティバッグのマッピング XML スキーマを示しています。これは、WDK インストールフォルダーの次のパスにあります。 \\\\um\\printerdriverdevmodemap.xsd.pr が含まれています。

![devmode プロパティバッグマッピング xml スキーマ](images/propbagmapschema.png)

DEVMODE プロパティバッグマッピングの XML ファイルは、INFGate ツールによって検証されます。

## <a name="queue-property-bag"></a>キュープロパティバッグ


キュープロパティバッグには、キューごとの構成設定が格納されます。これには、トレイマッピングのフォームや、インストール可能なオプションなどのプリンタープロパティの構成が含まれます。 ドライバーで定義されたプロパティとプリンターのプロパティは PowerShell で構成できますが、フォームからトレイへのマッピングは、プリンターのプロパティ UI で構成できます。 プリンター拡張では、プロパティ値を編集できません。

多くの v4 印刷ドライバーに対して、キュープロパティバッグは自動的に作成されますが、ドライバーが XML ファイルを使用して構成するための追加のプロパティを提供する場合もあります。 この XML ファイルは、ドライバーのプロパティバッグツールを使用してコンパイルしないでください。 キュープロパティバッグは、次のいずれかを実行する v4 印刷ドライバーでサポートされているプリンターで使用できます。

1. 複数のトレイを指定します。

2. GPD または PPD ファイルでインストール可能なオプションを指定します。または、

3. QueueProperties ディレクティブを使用して、ドライバーマニフェスト内のキュープロパティバッグを指定します。

管理者は、PowerShell を使用してキューのプロパティバッグを構成します。 次のコマンドレット (コマンドレット) は、プリンターオブジェクトの子であり、Get-help コマンドレットを使用して取得できます。

| コマンドレット名                                                                                                  | 説明                                                             |
|--------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| PrinterName &lt;printerName&gt;-name &lt;propertyName\*&gt;                            | 1つ以上のプロパティを取得します (-name はグロビングをサポートします)              |
| 設定-プリンタープロパティ-inputObject &lt;プリンター Propertyobject&gt;                                               | 永続化されたプリンターの Propertyobject を使用して、印刷キューのプロパティを変更します。 |
| printerName &lt;printerName&gt;-PropertyName &lt;propertyName&gt;-Value &lt;value&gt; | 指定されたプロパティを、指定された値に変更します。                  |



**インストール可能なオプション**。 これらのオプション (両面印刷の状態など) は、個別のプロパティとしてキュープロパティバッグに公開されます。 各プロパティは次のように名前が付けられます。機能名は、ドライバーの GPD ファイルまたは PPD ファイルの機能名に基づきます。

- Config:&lt;機能名&gt;

たとえば、Config: DuplexUnit のようになります。

プロパティの値は、管理者によって選択されたオプションのキーワード名です。 たとえば、がインストールされているとします。 インストール可能なオプションは、キューのプロパティに使用されるものと同じ Set-プリンタープロパティのコマンドレットを使用して編集できます。

**メモ** Windows 8.1 以降では、管理者権限を持つユーザー、または印刷キューを作成したユーザーは、UWP デバイスアプリからキュープロパティバッグのインストール可能なオプションとキューごとの構成設定を変更できます。



**フォームからトレイへのマッピング**。 V4 印刷ドライバーを使用し、複数のトレイがあるプリンターの場合、"FormTrayTable" という名前のプロパティのキュープロパティバッグを介して "フォーム to tray" マッピングが公開されます。

このプロパティは、"&lt;トレイ名&gt;、&lt;フォーム名&gt;" の形式のペアを含む null で終わる文字列として書式設定されます。フォーム名は次のいずれかになります。

1. 用紙サイズが GPD または PPD ファイルの印刷スキーマにマップされている場合 (standard \*PaperSize/\*PageSize キーワードを使用するか、\*(MS) PrintSchemaKeywordMap)、フォーム名は次の形式に従います。

PrintSchema:&lt;用紙サイズの名前&gt;

たとえば、PrintSchema: NorthAmericaLetter のようになります。

2. フォームがユーザー定義のフォームである場合\_USER フラグの形式によって決まりますが、フォーム名は次のようになります。 フォームインデックスは、スプーラのフォームデータベースで使用される値と同じです。 これは、ユーザーが&lt;フォームインデックス&gt;として、PrintTicket で用紙サイズが指定されている場合に使用されるインデックスと一致します。

ユーザー&lt;フォームインデックス&gt;

たとえば、UserForm123 のようになります。

3. それ以外の場合、フォーム名は次の形式に従います。フォーム名は、GPD の \*PaperSize または PPD の \*PageSize で指定された名前です。

Config:&lt;名&gt;

たとえば、Config:\_8\_5x16 のようになります。

完全なサンプル文字列は、"Config: Tray1, PrintSchema: NorthAmericaLetter, Config: Tray2, Config:\_8\_5X16, Config: Manual, UserForm123,\\0" のように読み取られます。

レンダリングフィルターでは、入力された PrintTicket の PageMediaSize 設定を読み取り、その値を FormTrayTable のフォーム名の値で検索する必要があります。

**Queue プロパティバッグ XML サンプル**。 次のコードスニペットは、3つのプロパティ、Name1、Name2、Name3、およびそれらの子要素に使用できる XML 構文を示しています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Properties xmlns= "https://schemas.microsoft.com/windows/2011/08/printing/queueproperties">
  <Property Name="Name1">
    <String>String1</String>
  </Property>
  <Property Name="Name2">
    <Int32>3244</Int32>
  </Property>
  <Property Name="Name3">
    <Bool>true</Bool>
  </Property>
</Properties>
```

**キュープロパティバッグの XML スキーマ**。 次のスクリーンショットは、キュープロパティバッグ XML スキーマを示しています。これは、WDK インストールフォルダーの次のパスにあります。 \\には、\\um\\printqueueproperties. xsd が含まれています。

![queue プロパティバッグ xml スキーマ](images/queuepropbagschem.png)

## <a name="related-topics"></a>関連トピック
[**Iプリンター Extensioncontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioncontext)  
[**Iプリンター Extensioneventargs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs)  
[**Iプリンター Propertybag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterpropertybag)  
[**Iプリンター Scriptablepropertybag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablepropertybag)  
[**IPrinterScriptContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)  
[**印刷フィルターパイプラインプロパティバッグ**](https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag)  



