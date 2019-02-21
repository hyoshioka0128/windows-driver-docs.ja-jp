---
title: V4 プリンター ドライバーのプロパティ バッグ
description: V4 印刷ドライバー モデルは、さまざまなレンダリング プロセスをカスタマイズした UI アプリケーションからのデータ フローを容易にするプロパティ バッグを提供します。
ms.assetid: 4E20303A-BEB3-4928-BA5A-356D978FA2BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8a0d9c5515f67b8507933fc0143c9e5e20a6d74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528121"
---
# <a name="v4-printer-driver-property-bags"></a>V4 プリンター ドライバーのプロパティ バッグ


V4 印刷ドライバー モデルは、さまざまなレンダリング プロセスをカスタマイズした UI アプリケーションからのデータ フローを容易にするプロパティ バッグを提供します。

これらのプロパティ バッグは、カスタム プロパティをカスタマイズした UI で作成してレンダリング プロセスによって消費されるフィーチャーの定義を許可します。 使用して公開されるすべてのプロパティ バッグ、 [ **IPrinterScriptablePropertyBag** ](https://msdn.microsoft.com/library/windows/hardware/hh973217)インターフェイスを JavaScript でまたはを使用して、 [ **IPrinterPropertyBag** ](https://msdn.microsoft.com/library/windows/hardware/hh439547)他の環境でのインターフェイス。

次の表では、さまざまなコンポーネントを使用して、v4 印刷ドライバーのさまざまな部分からプロパティ バッグ オブジェクトを取得する方法の概要を示します。

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
<td>JavaScript の制約のスクリプト</td>
<td>ドライバーとキューのプロパティ バッグは、scriptContext のパラメーターを使用して JavaScript 制約のスクリプトに渡されます。 このパラメーターは型<a href="https://msdn.microsoft.com/library/windows/hardware/hh768279" data-raw-source="[&lt;strong&gt;IPrinterScriptContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh768279)"> <strong>IPrinterScriptContext</strong> </a>子が含まれています。DriverProperties – は、ドライバーのプロパティ バッグを指します。
QueueProperties – は、キューのプロパティ バッグを指します。
ユーザーのプロパティ-ユーザーのプロパティ バッグ。
DEVMODE プロパティ バッグは、対象の DEVMODE に渡される&lt; - &gt; PrintTicket 変換の方法として、 <em>devModeProperties</em>パラメーター (型の<strong>IPrinterScriptablePropertyBag</strong>)。 他の方法でご利用いただけません。</td>
</tr>
<tr class="even">
<td>USB Bidi JavaScript</td>
<td>ドライバーとキューのプロパティ バッグは、scriptContext のパラメーターを使用して USB Bidi JavaScript スクリプトに渡されます。 このパラメーターは型<strong>IPrinterScriptContext</strong>子が含まれています。DriverProperties – は、ドライバーのプロパティ バッグを指します。
QueueProperties – は、キューのプロパティ バッグを指します。</td>
</tr>
<tr class="odd">
<td>プリンター拡張アプリ</td>
<td>すべてのプロパティ バッグの一部として渡されます、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh973207" data-raw-source="[&lt;strong&gt;IPrinterExtensionEventArgs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh973207)"> <strong>IPrinterExtensionEventArgs</strong> </a> OnDriverEvent ハンドラーのパラメーター。 これらはすべて型<strong>IPrinterPropertyBag</strong>します。 これらは、次のよう指定します。DriverProperties – は、ドライバーのプロパティ バッグを指します。
ユーザーのプロパティ-ユーザーのプロパティ バッグ。
PrinterQueue.GetProperties() – キューのプロパティ バッグを参照します。</td>
</tr>
<tr class="even">
<td>UWP デバイス アプリ</td>
<td>すべてのプロパティ バッグは、ライセンス認証を使用して中にで渡される、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh406649" data-raw-source="[&lt;strong&gt;IPrinterExtensionContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406649)"> <strong>IPrinterExtensionContext</strong> </a>オブジェクト。 として指定されています。DriverProperties – は、ドライバーのプロパティ バッグを指します。
ユーザーのプロパティ-ユーザーのプロパティ バッグ。
PrinterQueue.GetProperties() – キューのプロパティ バッグを参照します。</td>
</tr>
<tr class="odd">
<td>XPS 表示フィルター</td>
<td><p>XPS フィルター内からドライバーのプロパティ バッグにアクセスできる、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff561066" data-raw-source="[&lt;strong&gt;Print Filter Pipeline Property Bag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561066)"><strong>印刷フィルター パイプラインのプロパティ バッグ</strong></a>プロパティ名を使用して&quot;DriverPropertyBag&quot;、または定義済みの値XPS_FP_PROPERTY_BAG <em>filterpipeline.h</em>します。 DriverPropertyBag に関する情報を次に示します。</p>
<strong>プロパティの種類:</strong>VT_UNKNOWN<strong>説明。</strong>IUnknown インターフェイスへのポインター。 ドライバーのプロパティ バッグに IPrinterPropertyBag インターフェイスへのポインターを取得する QueryInterface を呼び出してください。
<p>XPS フィルター キューのプロパティ バッグ内からアクセスできますプロパティ名を使用して印刷フィルター パイプラインのプロパティ バッグと&quot;QueuePropertyBag&quot;、または、定義されている値から XPS_FP_QUEUE_PROPERTY_BAG <em>filterpipeline.h</em>. QueuePropertyBag に関する情報を次に示します。</p>
<strong>プロパティの種類:</strong>VT_UNKNOWN<strong>説明。</strong>IUnknown インターフェイスへのポインター。 キューのプロパティ バッグに IPrinterPropertyBag インターフェイスへのポインターを取得する QueryInterface を呼び出してください。</td>
</tr>
</tbody>
</table>



JavaScript の実装では、プロパティ バッグはパラメーターとして渡されます。 プリンター拡張機能のアプリケーションでは、プロパティ バッグはアプリケーションを起動するために使用するイベント引数のメンバーとして渡されます。

Javascript の実装では、プロパティ バッグ アクセサーと同様に、COM IPrinterQueue、IPrinterExtensionContext および IPrinterExtensionEventArgs インターフェイスによって提供されるプロパティ バッグのアクセサーは例外をスロー プロパティ バッグを指定しない場合または、見つかりませんでした。 さらに、IPrinterPropertyBag インターフェイス上の個々 のプロパティの照会は例外をスロー プロパティが見つからない場合。 プロパティが使用できない場合は、クラッシュを回避するために、try catch ステートメントを使用する必要があります。

## <a name="driver-property-bag"></a>ドライバーのプロパティ バッグ


ドライバーのプロパティ バッグとは、ドライバーをドライバーが読み取り専用に使用するためのプロパティまたはデータの blob を事前に定義のデータ ストアです。 V4 のマニフェスト ファイルで"PropertyBag"ディレクティブを使用して指定することができ、実行時に変更できません。

Windows ドライバー キットには、ドライバーのプロパティ バッグのプロジェクト テンプレートが含まれています。 ドライバーのプロパティ バッグとは、コンパイル済みのバイナリの blob です。 Visual Studio には、コンパイル済みのドライバーのプロパティ バッグを生成するテンプレートが含まれています。 このテンプレートで生成される XML ファイルがプロパティ バッグが、代わりに、このテンプレートのコンパイル済みの出力は、プロパティ バッグ ファイル v4 のマニフェスト ファイルで指定する必要があります。

## <a name="user-property-bag"></a>ユーザーのプロパティ バッグ


ユーザーのプロパティ バッグは、パートナーのユーザー コンピューターのローカル コンテキストで設定を保存できます。 このプロパティ バッグは、「今後表示しない」のようなユーザー設定用のストレージ メカニズムとしても適しています。 このプロパティ バッグは管理者が管理することと、プリンターの共有時にクライアントとサーバー間で同期されません。 ユーザーのプロパティ バッグは実行時にのみ設定しはのみのプリンター拡張、UWP デバイスのアプリ、および JavaScript の制約を使用できます。

**注**印刷中に制約のための JavaScript が、ユーザー コンテキストの外部で呼び出すことも可能性があります、この時点では、ユーザーのプロパティ バッグは使用できません、および Windows には、HRESULT が返されます\_FROM\_WIN32 (エラー\_いない\_が見つかりました)。



## <a name="devmode-property-bag"></a>DEVMODE プロパティ バッグ


DEVMODE プロパティ バッグを使用して、DEVMODE 構造体のプライベート セクションの内容を整理します。 ConvertPrintTicketToDevMode の呼び出し中に JavaScript が DEVMODE プロパティ バッグのコンテンツの入力に呼び出されます。 ConvertDevModeToPrintTicket の呼び出し時に、DEVMODE プロパティ バッグから永続化された設定を読み取るし、PrintTicket に保管する JavaScript が呼び出されます。

このプロパティ バッグは、一部のシナリオでデータ損失を回避するには、DEVMODE 構造体をシリアル化が必要であるために、60 KB 未満 (正確な量は、対象の DEVMODE の割り当て済みのセクションのサイズに基づいては異なります)、サイズ制限されます。 使用可能な正確なサイズは、DEVMODE のパブリック セクションには構成モジュールによって管理されるプライベート セクションのサイズによって決定されますので、ドライバーによって異なります。

DEVMODE プロパティ バッグは、プロパティ バッグのメンバーを指定する XML ファイルを使用し、変換を処理するために convertPrintTicketToDevMode と convertDevModeToPrintTicket Api を使用します。 XML DEVMODE のマッピング ファイルは、DevModeMap ディレクティブを使用して v4 マニフェストで指定する必要があります。

次のコード スニペットでは、DEVMODE プロパティ バッグ マッピング XML サンプルを示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Properties xmlns="http://schemas.microsoft.com/windows/2011/08/printing/devmodemap">
  <Property Name="FabrikamAccountCode">
    <String Length="32"></String>
  </Property>  
</Properties>
```

次のスクリーン ショットは、DEVMODE プロパティ バッグ マッピング XML スキーマを示し、WDK のインストール フォルダーに次のパスに見つかんだことができます。\\含める\\um\\printerdriverdevmodemap.xsd.pr

![devmode プロパティ バッグのマッピングの xml スキーマ](images/propbagmapschema.png)

DEVMODE プロパティ バッグのマッピングの XML ファイルは、INFGate ツールによって検証されます。

## <a name="queue-property-bag"></a>キューのプロパティ バッグ


キューのプロパティ バッグは、トレイ マッピングとインストール可能なオプションと同様に、プリンターのプロパティの構成のフォームを含む、キューごとの構成設定を格納します。 ドライバー定義のプロパティとプリンターのプロパティは PowerShell では、構成可能なトレイ マッピングするためのフォームは、プリンターのプロパティ UI で構成できます。 プリンターの拡張機能は、プロパティ値のいずれかを編集できません。

キューのプロパティ バッグは、多くの v4 プリンター ドライバー用に自動的に作成されますが、ドライバーは、XML ファイルを使用して構成する追加のプロパティを提供も可能性があります。 ドライバーのプロパティ バッグのツールを使用してこの XML ファイルをコンパイルできません必要があります。 キューのプロパティ バッグは、次のいずれかを実行する v4 印刷ドライバーによってサポートされているプリンターを使用できます。

1. 複数のトレイを指定または

2. GPD または PPD ファイルでインストール可能なオプションを指定または

3. QueueProperties ディレクティブを使用してマニフェストをドライバーでは、キューのプロパティ バッグを指定します。

管理者は、PowerShell を使用してキューのプロパティ バッグを構成します。 次のコマンドの使用 (コマンドレット) は、Get プリンター コマンドレットを使用して取得できるプリンター オブジェクトの子です。

| コマンドレット名                                                                                                  | 説明                                                             |
|--------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Get-PrinterProperty -printerName &lt;printerName&gt; -name &lt;propertyName\*&gt;                            | 1 つまたは複数のプロパティを取得します (-名グロビングをサポートしています)              |
| セット PrinterProperty inputObject &lt;printerPropertyObject&gt;                                               | 印刷キューを永続化された printerPropertyObject を使用してプロパティを変更します。 |
| セット PrinterProperty printerName &lt;printerName&gt; -propertyname &lt;propertyName&gt; -値&lt;値&gt; | 指定された値に指定されたプロパティを変更します。                  |



**インストール可能なオプション**します。 両面印刷ユニットでの状態など、これらのオプションは、キューのプロパティ バッグに個々 のプロパティとして公開されます。 機能名は、ドライバーの GPD または PPD ファイルから機能の名前をに基づいて、次のように各プロパティの名前は。

- Config:&lt;機能名&gt;

たとえば、Config:DuplexUnit

プロパティの値は、管理者が選択されているオプションのキーワード名前です。 たとえば、次のようにインストールします。 インストール可能なオプションでは、キューのプロパティに使用される同じセット PrinterProperty コマンドレットを使用して編集できます。

**注**以降 Windows 8.1 では、管理者の権限を持つユーザーまたは印刷キューを作成したユーザーを変更できますインストール可能なオプションとキューのプロパティ バッグのキューごとの構成設定 UWP デバイス アプリから。



**トレイ マッピングするためのフォーム**します。 プリンター、v4 印刷ドライバー、および"FormTrayTable"という名前のプロパティでキューのプロパティ バッグを使用して 1 つ以上のトレイに「トレイにフォーム」のマッピングが公開されています。

このプロパティは、形式のペアを含む null で終わる文字列として書式設定"&lt;トレイ名&gt;、&lt;フォーム名&gt;、"形式の名前は、次のいずれか。

1. 用紙サイズが GPD または PPD ファイルに印刷スキーマにマップされている場合 (標準を使用して\*PaperSize/\*PageSize キーワード、または\*(ミリ秒) PrintSchemaKeywordMap)、フォーム名には、次の形式に従います。

PrintSchema:&lt;用紙サイズ名&gt;

たとえば、PrintSchema:NorthAmericaLetter

2. 場合は、フォームによって決定される、ユーザー定義のフォームが\_し、ユーザーのフラグ、フォーム名を次のようになります。 フォームのインデックスは、スプーラの形式のデータベースで使用される同じ値です。 これは、ユーザー フォームとして PrintTicket の用紙サイズを指定した場合に使用されるインデックスを一貫性のある&lt;フォーム インデックス&gt;します。

ユーザー フォーム&lt;形式のインデックス&gt;

たとえば、UserForm123

3. それ以外の場合、フォーム名は、次の形式、フォーム名がフォロー GPD ので指定された名前\*PaperSize または PPD の\*PageSize します。

Config:&lt;名&gt;

たとえば、構成:\_8\_5 x 16

完全な例文字列よう表示。"Config:Tray1、PrintSchema:NorthAmericaLetter、Config:Tray2、Config:\_8\_5 X 16 の Config:Manual、UserForm123、\\0"です。

フィルターを表示、着信 PrintTicket の PageMediaSize の設定を読み取るし、FormTrayTable から、フォーム名の値でその値を検索する必要があります。

**キューのプロパティ バッグの XML サンプル**します。 次のコード スニペットでは、3 つのプロパティ、Name1、Name2、Name3 およびその子要素を使用できる XML 構文を示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Properties xmlns= "http://schemas.microsoft.com/windows/2011/08/printing/queueproperties">
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

**キューのプロパティ バッグの XML スキーマ**します。 次のスクリーン ショットはキュー プロパティ バッグの XML スキーマを示し、WDK のインストール フォルダーに次のパスに見つかんだことができます。\\含める\\um\\printqueueproperties.xsd します。

![キューのプロパティ バッグの xml スキーマ](images/queuepropbagschem.png)

## <a name="related-topics"></a>関連トピック
[**IPrinterExtensionContext**](https://msdn.microsoft.com/library/windows/hardware/hh406649)  
[**IPrinterExtensionEventArgs**](https://msdn.microsoft.com/library/windows/hardware/hh973207)  
[**IPrinterPropertyBag**](https://msdn.microsoft.com/library/windows/hardware/hh439547)  
[**IPrinterScriptablePropertyBag**](https://msdn.microsoft.com/library/windows/hardware/hh973217)  
[**IPrinterScriptContext**](https://msdn.microsoft.com/library/windows/hardware/hh768279)  
[**印刷フィルター パイプラインのプロパティ バッグ**](https://msdn.microsoft.com/library/windows/hardware/ff561066)  



