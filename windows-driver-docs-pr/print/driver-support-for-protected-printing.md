---
title: 保護された印刷のドライバー サポート
description: Windows 8.1 には、ジョブを印刷する前に、ユーザーがプリンターで使用する暗証番号 (PIN) を指定できるようにする、保護された印刷のサポートが含まれています。
ms.assetid: 43569030-224F-46C6-963F-FC3BE24A0FB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6210f67860aedabc190fc851fc11c136cad053b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845051"
---
# <a name="driver-support-for-protected-printing"></a>保護された印刷のドライバー サポート


Windows 8.1 には、ジョブを印刷する前に、ユーザーがプリンターで使用する暗証番号 (PIN) を指定できるようにする、保護された印刷のサポートが含まれています。

また Windows 8.1 を使用すると、管理者は既定の PIN を指定して、印刷されたコンテンツに関連する、ユーザーが取得していないコンテンツの使用量を減らすことができます。 このトピックでは、保護された印刷をサポートするために加えられた変更について説明します。また、このサポートを v4 印刷ドライバーに追加するために必要な手順の概要も示します。

## <a name="print-schema-changes"></a>スキーマ変更の印刷

Windows 8.1 には、PrintTicket および PrintCapabilities ドキュメントで保護された印刷を指定するために使用できる新しい印刷スキーマキーワードが導入されています。 これらのキーワードは、新しい*printschemakeywordsv11*名前空間で定義されています。 この名前空間の URI を次に示します。

*http://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11*

PrintTicket ファイルで保護された印刷を指定する方法については、「[ピン印刷用の Printticket ファイルの例](sample-printticket-file-for-pin-printing.md)」を参照してください。 また、PrintCapabilities ファイルで保護された印刷を指定する方法については、「 [PIN 印刷用のサンプル PrintCapabilities ファイル](sample-printcapabilities-file-for-pin-printing.md)」を参照してください。

仕様は次の場所でダウンロードできます。

[印刷スキーマの仕様1.1](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/print-schema-spec-1-1.zip)

[印刷スキーマの仕様2.0](http://download.microsoft.com/download/d/e/c/deca6e6b-3e81-48e7-b7ef-6d92a547d03c/print-schema-spec-2-0.zip)


## <a name="driver-changes"></a>ドライバーの変更


V4 ドライバーを使用している場合は、汎用プリンターの説明 (GPD) または PostScript プリンターの説明 (PPD) ファイル、およびその他のドライバー関連のコードファイルに変更を加える必要があります。 変更の影響を受けるドライバー関連のコードファイルは、次のように分類できます。

-   ドライバー構成ファイル (GPD または PPD)
-   XPS レンダリングフィルター
-   プリンターの拡張機能
-   UWP デバイス アプリ

詳細については、PTProvider コードで必要な変更を行っている限り、保護された印刷用の Print Schema キーワードで v3 ドライバーを使用**する  ます**。 ただし、これらの変更を行う手順は、このトピックの範囲外です。

 

以下のセクションでは、v4 ドライバーが保護された印刷をサポートできるようにする変更を実装する方法について詳しく説明します。

**ドライバー構成ファイル**

V4 印刷ドライバーのデータファイルで保護された印刷のサポートを指定します。 データファイルは、GPD または PPD ファイルのいずれかです。ドライバーで使用されます。 保護された印刷を有効にするには、MinLength ディレクティブと MaxLength ディレクティブの両方を指定する必要があります。 次の表では、ドライバーの GPD ファイルまたは PPD ファイルに追加する必要がある関連キーワードについて説明します。

**GPD ファイルに追加するもの**。 ドライバーで GPD ファイルが使用されている場合は、次の新しいキーワードをこの構文を使用して追加します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>キーワード</th>
<th>説明</th>
<th>レベル</th>
<th>使用できる値</th>
<th>例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong><em>Jobpass Codeminlength</strong></td>
<td><p>サポートされている PIN の数値文字列の最小文字数。</p>
<p>この値は、少なくとも4で15以下でなければなりません。</p></td>
<td>Root</td>
<td>任意の<a href="numeric-values.md" data-raw-source="[GPD numeric value](numeric-values.md)">GPD の数値</a></td>
<td></em>Jobpass Codeminlength: 4</td>
</tr>
<tr class="even">
<td><strong><em>Jobpass Codemaxlength</strong></td>
<td><p>サポートされている PIN の数値文字列の最大長。</p>
<p>この値は、少なくとも4で15以下でなければなりません。 <strong></em>Jobpass Codeminlength</strong>値以上である必要があります。</p></td>
<td>Root</td>
<td>任意の<a href="numeric-values.md" data-raw-source="[GPD numeric value](numeric-values.md)">GPD の数値</a></td>
<td>\* Jobpass Codemaxlength: 9</td>
</tr>
</tbody>
</table>

 

**PPD ファイルに追加する内容**。 ドライバーで PPD ファイルが使用されている場合は、次の新しいキーワードをこの構文を使用して追加します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>キーワード</th>
<th>説明</th>
<th>レベル</th>
<th>使用できる値</th>
<th>例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong><em>Msjobpass Codeminlength</strong></td>
<td><p>サポートされている PIN の数値文字列の最小文字数。</p>
<p>この値は、少なくとも4で15以下でなければなりません。</p></td>
<td>Root</td>
<td><p>"int" (QuotedValue)</p>
<p>言い換えると、整数値は引用符で囲む必要があります。</p></td>
<td></em>Msjobpass Codeminlength: "4"</td>
</tr>
<tr class="even">
<td><strong><em>Msjobpass Codemaxlength</strong></td>
<td><p>サポートされている PIN の数値文字列の最大長。</p>
<p>この値は、少なくとも4で15以下でなければなりません。 <strong></em>Msjobpass Codeminlength</strong>値以上である必要があります。</p></td>
<td>Root</td>
<td><p>"int" (QuotedValue)</p>
<p>言い換えると、整数値は引用符で囲む必要があります。</p></td>
<td>\* Msjobpass Codemaxlength: "9"</td>
</tr>
</tbody>
</table>

 

**ハードウェアの制約を指定**します。 ハードドライブなどのインストール可能なハードウェアを使用せずに、ピン印刷をサポートしていないデバイスがある場合は、GPD または PPD ファイルを使用してこれらの制約を指定します。 これを行うには、GPD または PPD ファイルを編集して、JobPasscode コード機能と JobPasscode コードの両方のオプション (On と Off) を表示する必要があります。 ON/OFF オプションでは、PrintSchemaKeywordMap または MSPrintSchemaKeywordMap のいずれかを適切な値に設定する必要があります。

**ソフトウェアの制約**。 これらはサポートされていません。

次の表は、保護された印刷およびハードウェアの制約のサポートを指定する場合に使用する必要があるキーワードの有効な値を示しています。

ファイルの種類のキーワード有効値 GPD \*Feature JobPasscode コード \*オプション
-   無効
-   有効

\*PrintSchemaKeywordMap
-   オート
-   代わっ
-   "JobPasscode コード"

PPD \*Feature JobPasscode コード \*オプション
-   無効
-   有効

\*MSPrintSchemaKeywordMap
-   オート
-   代わっ
-   "JobPasscode コード"

 

**GPD と PPD ファイルの例**

GPD ファイルの例を次に示します。これは、インストール可能なハードウェア制約で JobPasscode コードを指定するものです。

```GDP
*%
*GPDSpecVersion: "1.0"
*GPDFileVersion: "1.0"

*Include:        "StdNames.gpd"
*Include:        "MSxpsinc.gpd"
*ResourceDLL:    "unires.dll"

*GPDFileName:    "FAsmpl.gpd"
*ModelName:      "Fabrikam JobPasscode Sample"
*MasterUnits:    PAIR(1200, 1200)
*PrinterType:    PAGE
*MaxCopies:      999

*JobPasscodeMinLength: 4
*JobPasscodeMaxLength: 15

*%******************************************************************************
*%                             JobPasscode
*%******************************************************************************
*Feature: JobPasscode
{
    *Name: ”Job Passcode”
    *DefaultOption: OFF
    *ConcealFromUI: TRUE
    *PrintSchemaKeywordMap: “JobPasscode”

    *Option: OFF
    {
     *PrintSchemaKeywordMap: “Off”
        *Name: ”Off”
    }

    *Option: ON
    {
     *PrintSchemaKeywordMap: “On”
        *Name: ”On”
    }
}

*Feature:PrinterHardDisk
{
    *rcNameID: RESDLL.PCL5ERES.430
    *FeatureType: PRINTER_PROPERTY
    *DefaultOption: FALSE
    *Option: FALSE
    {
     *DisabledFeatures: LIST(JobPasscode)
        *rcNameID: RESDLL.PCL5ERES.444
    }
    *Option: TRUE
    {
        *rcNameID: RESDLL.PCL5ERES.443
    }
}
```

\*ConcealFromUI キーワードを使用して、保護された印刷オプションが誤って表示されないように TRUE に設定する必要がある  に**注意**してください。 前の GPD ファイルの例を参照してください。

 

インストール可能なハードウェア制約で JobPasscode コードを指定する PPD ファイルの例を次に示します。

```PPD
*MSJobPasscodeMinLength: "4"
*MSJobPasscodeMaxLength: "15"

*OpenGroup: InstallableOptions/Installable Options

*% ===== Optional Hard Disk =====
*OpenUI *HardDisk/Printer Hard Disk: Boolean
*DefaultHardDisk:  False
*HardDisk False/Not Installed: ""
*HardDisk True/Installed: ""
*CloseUI: *HardDisk

*CloseGroup: InstallableOptions

*% ===== JobPasscode Feature =====
*OpenUI *JobPasscode: PickOne
*DefaultJobPasscode: On
*JobPasscode On: ""
*CloseUI: *JobPasscode

*MSPrintSchemaKeywordMap: JobPasscode  *JobPasscode
*MSPrintSchemaKeywordMap: JobPasscode  On *JobPasscode On

*UIConstraints: *HardDisk False *JobPasscode
```

前の PPD ファイルの例でわかるように、\*UIConstraints キーワードはハードウェアの制約を示しています。

Windows オペレーティングシステムによって、保護された印刷機能のロケール固有の文字列とそれに関連するオプションが自動的に表示さ  **ことに注意**してください。 この機能またはそのオプションに新しいローカライズされた名前を指定することはできません。

 

**XPS レンダリングフィルター**

既存のデバイスのドライバーは、レンダリングコードを変更する必要があります。これにより、これらのドライバーが PIN 値の PrintTicket 表現をデバイスが認識できる値に変換できるようになります。 一般に、既存の XPS 表示フィルターにコードを追加するか、保護された印刷をサポートするために新しい XPS レンダリングフィルターを追加する必要があります。 PCL6 および PostScript 用の標準の XPS レンダリングフィルターを使用するドライバーは、フィルターパイプラインの新しいストリームフィルターを作成する必要があります。 ストリームが標準フィルターを通過した後、この新しいストリームフィルターは、フィルターパイプラインの事前レンダリングされた PDL ストリームに適切なコマンドを挿入します。

Microsoft の推奨事項として、クライアントまたはサーバー PC のレンダリング要件を最小限に抑えるために、XPS または OpenXPS をサポートする新しいデバイスでは、追加の変換を使用せずに新しいキーワードをサポートする必要があります。

**プリンターの拡張機能**

プリンターの拡張機能は、印刷設定の UI で、保護された印刷のコントロールを表示できる必要があります。 これにより、デスクトップアプリのユーザーは、プリンターの拡張機能を使用するときに、保護された印刷機能を構成できます。 Microsoft は、 [**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)ファミリの api がプリンター拡張機能からの保護された印刷をサポートできるように変更を加えています。

**UWP デバイスアプリ**

また、Microsoft は、 [**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)ファミリの API が UWP デバイスアプリと連携して、印刷設定の UI で保護された印刷のコントロールを表示できるように変更を加えています。

 

 




