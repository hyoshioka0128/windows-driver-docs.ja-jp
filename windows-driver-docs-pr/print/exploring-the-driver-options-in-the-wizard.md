---
title: ウィザードのドライバー オプションの詳細
description: このトピックでは、v4 印刷ドライバーの作成ウィザードの最初のセクションのドライバーオプションについて説明します。
ms.assetid: 48FF0A37-BBAF-49D1-9BDE-128AED00BEEF
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: a4964c8846188171e3e730c3bd536cdd1292d9e4
ms.sourcegitcommit: f0e54ea159d168a77643bf2e098d6b90e92b528c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455554"
---
# <a name="exploring-the-driver-options-in-the-wizard"></a>ウィザードのドライバー オプションの詳細

このトピックでは、 **V4 印刷ドライバーの作成**ウィザードの最初のセクションのドライバーオプションについて説明します。

ここでは、さまざまな機能のオプションについて簡単に確認できるように、この情報を概要形式で提供しています。 すべての機能に関する詳細情報が必要な場合は、詳細情報を提供する関連トピックへのリンクを参照してください。

## <a name="driver-rendering-type"></a>ドライバーレンダリングの種類

### <a name="v4-print-driver-with-custom-rendering-filters-accepts-xps-only"></a>カスタムレンダリングフィルターを使用した V4 印刷ドライバー (XPS のみを受け入れる)

入力として Microsoft XPS 形式のみを受け入れるプリンタードライバーを作成する場合は、このオプションを選択します。 このドライバーは、 **[DRIVER XPS format の選択**] フィールドでの選択に応じて、xps 形式または OpenXPS 形式で出力を生成することができます。

### <a name="v4-print-driver-with-class-driver-rendering"></a>V4 印刷ドライバーとクラスドライバーのレンダリング

このオプションを選択すると、XPS または OpenXPS のいずれかの形式で入力を受け付けることができるプリンタードライバーを作成します。 また、このドライバーを選択するときに、このウィザードの次のページで、表示に使用する印刷クラスドライバーの名前を指定する必要があります。

### <a name="microsoft-xps-to-pcl6-render-filter-accepts-xps-only"></a>Microsoft XPS to PCL6 render filter (XPS のみを受け入れる)

このオプションを使用すると、入力として XPS 形式のみを受け入れるフィルタードライバーモジュールを作成し、入力を PCL6 に変換できます。 このドライバーは、 **[DRIVER XPS format の選択**] フィールドでの選択に応じて、xps 形式または OpenXPS 形式で出力を生成することができます。

### <a name="microsoft-xps-to-postscript-render-filter-accepts-xps-only"></a>Microsoft XPS から PostScript へのレンダリングフィルター (XPS のみを受け入れる)

このオプションを使用すると、入力として XPS 形式のみを受け入れるフィルタードライバーモジュールを作成し、入力を PostScript に変換することができます。 このドライバーは、 **[DRIVER XPS format の選択**] フィールドでの選択に応じて、xps 形式または OpenXPS 形式で出力を生成することができます。

## <a name="driver-xps-format"></a>Driver XPS 形式

### <a name="xps"></a>XPS

このオプションは、XPS 形式でのみ出力を生成するようにドライバーを構成します。

### <a name="openxps"></a>OpenXPS

このオプションは、OpenXPS 形式でのみ出力を生成するようにドライバーを構成します。

### <a name="xps-openxps"></a>XPS、OpenXPS

このオプションを使用すると、ドライバーは xps 形式または OpenXPS 形式で出力を生成するように構成され、XPS は INF ファイルで既定として設定されます。

### <a name="openxps-xps"></a>OpenXPS、XPS

このオプションは、OpenXPS または XPS 形式の出力を生成するようにドライバーを構成し、INF ファイルでは OpenXPS を既定として設定します。

## <a name="driver-configuration-type"></a>ドライバーの構成の種類

### <a name="gpd-driver"></a>GPD ドライバー

このオプションを選択すると、ウィザードによって、プリンタードライバーを含む汎用プリンターの説明 (GPD) 言語ファイルが作成されます。

### <a name="ppd-driver"></a>PPD ドライバー

このオプションを選択すると、ウィザードによって、プリンタードライバーを含む PostScript プリンターの説明 (PPD) 言語ファイルが作成されます。

## <a name="protected-printing"></a>保護された印刷

### <a name="enable-protected-printing"></a>保護された印刷を有効にする

プリンターに送信される印刷要求をロックするために PIN を使用できるようにする場合は、このオプションを選択します。 エンドユーザーは、印刷のためにロックされた印刷要求を解放するために、プリンターで同じ PIN を指定する必要があります。 詳細については、「[保護された印刷に対するドライバーのサポート](driver-support-for-protected-printing.md)」を参照してください。

## <a name="additional-functionality"></a>その他の機能

### <a name="driver-property-bag"></a>ドライバープロパティバッグ

これは、ドライバープロパティバッグの内容を記述する XML ファイルです。 このファイルで指定されたプロパティと、プロジェクトの ByteArray または IStream フォルダーに追加されたデータファイルで提供される情報は、ドライバープロパティバッグにコンパイルされます。 詳細については、「 [V4 プリンタードライバーのプロパティバッグ](v4-driver-property-bags.md)」を参照してください。

また、ドライバープロパティバッグテンプレートの XML スキーマは、Windows ドライバーキットの次のフォルダーにあります。このフォルダーには、 * \\ Include \\ um \\ printdriverproperties .xml が含ま*れています。

### <a name="driver-event-file"></a>ドライバーイベントファイル

このファイルは、ドライバーイベントを発生させる可能性のある Bidi クエリとトリガーを記述するために使用されます。 また、ドライバーイベントは標準の文字列のみをサポートすることに注意してください。 ドライバーイベントと標準文字列の詳細については、「カスタマイズされた[UI のドライバーサポート](driver-support-for-customized-ui.md)」を参照してください。

### <a name="devmode-mapping-file"></a>DevMode マッピングファイル

これは、JavaScript コードでの PrintTicket < > DEVMODE 変換と共に使用される XML ファイルです。 このファイルを指定する場合は、 [V4 ドライバーマニフェスト](v4-driver-manifest.md)で指定する必要があります。

### <a name="queue-property-bag"></a>キュープロパティバッグ

このテンプレートを使用すると、フォームからトレイへのマッピングや、インストール可能なオプションなどのプリンタープロパティの構成など、キューごとの構成設定を行うことができます。 詳細については、「 [V4 プリンタードライバーのプロパティバッグ](v4-driver-property-bags.md)」を参照してください。

### <a name="resource-dll"></a>リソース DLL●りそーすdll○

このテンプレートを使用すると、外部に格納されているフォント、アイコン、その他のビットマップ、ローカライズ可能なユーザーインターフェイスのテキスト文字列などのリソースの説明を指定できます。 詳細については、「[ミニドライバーでのリソース dll の使用](using-resource-dlls-in-a-minidriver.md)」、「 [v4 ドライバーマニフェスト](v4-driver-manifest.md)」、および「 [v4 プリンタードライバーのローカライズ](v4-driver-localization.md)」を参照してください。

### <a name="constraints-js"></a>制約 JS

このテンプレートは、サポートされているすべての JavaScript 制約エントリポイントのメソッドヘッダーを提供します。 詳細については、「 [JavaScript の制約](javascript-constraints.md)」を参照してください。

### <a name="autoconfiguration-gdl"></a>自動構成 GDL

これにより、v4 印刷ドライバー用の基本的な自動構成ファイルが提供されます。 自動構成の GDL 構文、およびサンプルファイルを調べる方法については、「 [Print Auto Configuration Sample](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/print-auto-configuration-sample)」を参照してください。

### <a name="tcpmon-bidi-extension-xml"></a>TCPMon Bidi 拡張 XML

これにより、単純な TCP/IP Bidi 拡張ファイルが提供されます。 標準 TCP/IP ポートモニターの Bidi 構文の詳細については、「 [Tcp/ip スキーマ拡張](tcp-ip-schema-extensions.md)」を参照してください。

### <a name="wsdmon-bidi-extension-xml"></a>WSDMon Bidi 拡張 XML

これにより、単純な WSD Bidi 拡張ファイルが提供されます。 WSDMon の Bidi 構文の詳細については、「 [WSD スキーマ拡張](wsd-schema-extensions.md)」を参照してください。

### <a name="usbmon-bidi-extension-xml--js"></a>USBMon Bidi 拡張 XML + JS

これにより、シンプルな USB Bidi 拡張ファイルが提供されます。 これは、一致した USB Bidi エクステンダー JavaScript の存在に依存します。 詳細については、「 [USB Bidi Extender](usb-bidi-extender.md)」を参照してください。
