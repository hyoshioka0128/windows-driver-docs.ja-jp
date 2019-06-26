---
title: 保護された印刷のドライバー サポート
description: Windows 8.1 には、ユーザーが、ジョブ印刷する前に、プリンターを使用して、個人識別番号 (PIN) を指定する保護された印刷のサポートが含まれています。
ms.assetid: 43569030-224F-46C6-963F-FC3BE24A0FB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 020d4c1c358dd11d929f85390d18f2d5e2a556c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356063"
---
# <a name="driver-support-for-protected-printing"></a>保護された印刷のドライバー サポート


Windows 8.1 には、ユーザーが、ジョブ印刷する前に、プリンターを使用して、個人識別番号 (PIN) を指定する保護された印刷のサポートが含まれています。

Windows 8.1 では、コンテンツでは、出力がユーザーによって取得されることに関連する無駄な紙の使用量を削減するために、既定の PIN を指定することもできます。 このトピックでは、保護された印刷のサポートを提供するが可能な v4 印刷ドライバーをこのサポートを追加するために必要な手順についても説明します。 変更について説明します。

## <a name="print-schema-changes"></a>印刷スキーマの変更

Windows 8.1 には、使用できる PrintTicket と PrintCapabilities ドキュメントを指定する印刷保護されている新しい印刷スキーマ キーワードが導入されています。 これらのキーワードは、新しいで定義されている*printschemakeywordsv11*名前空間。 この名前空間の URI を次に示します。

*http://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11*

PrintTicket ファイルで保護された印刷を指定する方法については、次を参照してください。[印刷暗証番号 (pin) のサンプル ファイルは PrintTicket](sample-printticket-file-for-pin-printing.md)します。 PrintCapabilities ファイルで保護された印刷を指定する方法を参照してくださいと[暗証番号 (pin) 印刷用のサンプル PrintCapabilities ファイル](sample-printcapabilities-file-for-pin-printing.md)します。

仕様は、ここでダウンロードできます。

[印刷スキーマ仕様 1.1](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/print-schema-spec-1-1.zip)

[印刷スキーマの仕様を 2.0](http://download.microsoft.com/download/d/e/c/deca6e6b-3e81-48e7-b7ef-6d92a547d03c/print-schema-spec-2-0.zip)


## <a name="driver-changes"></a>ドライバーの変更


V4 ドライバーを使用している場合は、汎用的なプリンターの説明 (GPD) または PostScript プリンターの説明 (PPD) ファイル、およびその他のドライバーに関連するコード ファイルに変更を加える必要があります。 変更によって影響を受けるドライバー関連のコード ファイルは、次のように分類できます。

-   ドライバーの構成ファイル (GPD または PPD)
-   XPS 表示フィルター
-   プリンターの拡張機能
-   UWP デバイス アプリ

**注**  できますドライバーを使用する v3 印刷スキーマのキーワードで保護された印刷の場合、PTProvider コードで、必要な変更を行った場合に限りです。 それらの変更を行うための手順は、このトピックの範囲外です。

 

次のセクションでは、保護された印刷をサポートするために、v4 ドライバーができるようにする変更を実装する方法についての詳細情報を提供します。

**ドライバーの構成ファイル**

V4 印刷ドライバーのデータ ファイルで保護された印刷のサポートを示します。 データ ファイルは、GPD または PPD ファイルには、ドライバーを使用して任意の 1 つです。 保護された印刷を有効にする、MinLength と MaxLength のディレクティブを指定する必要があります。 次の表では、ドライバーの GPD または PPD ファイルに追加する必要があります、関連するキーワードについて説明します。

**GPD ファイルに追加すると**します。 ドライバーは、GPD ファイルを使用している場合は、この構文を使用して、次の新しいキーワードを追加します。

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
<th>Keyword</th>
<th>説明</th>
<th>Level</th>
<th>指定できる値</th>
<th>例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong><em>JobPasscodeMinLength</strong></td>
<td><p>サポートされている、暗証番号 (pin) の数値文字列の最小長。</p>
<p>この値は、少なくとも 4 つと 15 を超えるである必要があります。</p></td>
<td>ルート</td>
<td>すべて<a href="numeric-values.md" data-raw-source="[GPD numeric value](numeric-values.md)">GPD 数値</a></td>
<td></em>JobPasscodeMinLength:4</td>
</tr>
<tr class="even">
<td><strong><em>JobPasscodeMaxLength</strong></td>
<td><p>サポートされている、暗証番号 (pin) の数値文字列の最大長。</p>
<p>この値は、少なくとも 4 つと 15 を超えるである必要があります。 大きいまたは等しい必要があります、  <strong></em>JobPasscodeMinLength</strong>値。</p></td>
<td>ルート</td>
<td>すべて<a href="numeric-values.md" data-raw-source="[GPD numeric value](numeric-values.md)">GPD 数値</a></td>
<td>*JobPasscodeMaxLength:9</td>
</tr>
</tbody>
</table>

 

**PPD ファイルに追加すると**します。 ドライバーが PPD ファイルを使用する場合は、この構文を使用して、次の新しいキーワードを追加します。

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
<th>Keyword</th>
<th>説明</th>
<th>Level</th>
<th>指定できる値</th>
<th>例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong><em>MSJobPasscodeMinLength</strong></td>
<td><p>サポートされている、暗証番号 (pin) の数値文字列の最小長。</p>
<p>この値は、少なくとも 4 つと 15 を超えるである必要があります。</p></td>
<td>ルート</td>
<td><p>"int"(QuotedValue)</p>
<p>つまり、引用符で囲まれた整数値を表す必要があります。</p></td>
<td></em>MSJobPasscodeMinLength:「4」</td>
</tr>
<tr class="even">
<td><strong><em>MSJobPasscodeMaxLength</strong></td>
<td><p>サポートされている、暗証番号 (pin) の数値文字列の最大長。</p>
<p>この値は、少なくとも 4 つと 15 を超えるである必要があります。 大きいまたは等しい必要があります、  <strong></em>MSJobPasscodeMinLength</strong>値。</p></td>
<td>ルート</td>
<td><p>"int"(QuotedValue)</p>
<p>つまり、引用符で囲まれた整数値を表す必要があります。</p></td>
<td>\* MSJobPasscodeMaxLength:「9」</td>
</tr>
</tbody>
</table>

 

**ハードウェアの制約を指定する**します。 ハード ドライブなどのインストール可能なハードウェアなしの暗証番号 (pin) 印刷をサポートしていないデバイスがあれば、GPD または PPD のいずれかのファイルを使用してこれらの制約を指定します。 これを行うには、JobPasscode 機能と両方 JobPasscode オプションを表示し、(オンとオフ) に GPD または PPD ファイルを編集する必要があります。 ON/OFF オプションでは、適切な値に PrintSchemaKeywordMap または MSPrintSchemaKeywordMap のいずれかを設定する必要があります。

**ソフトウェアの制約**します。 これらはサポートされていません。

次の表では、保護された印刷およびハードウェアの制約のサポートを指定するキーワードを使用する必要がありますの有効な値を示します。

ファイルの種類のキーワードが有効な値は GPD\*機能 JobPasscode\*オプション
-   無効
-   ON

\*PrintSchemaKeywordMap
-   "Off"
-   "On"
-   "JobPasscode"

PPD\*機能 JobPasscode\*オプション
-   無効
-   ON

\*MSPrintSchemaKeywordMap
-   "Off"
-   "On"
-   "JobPasscode"

 

**GPD と PPD ファイルの例**

インストール可能なハードウェア制約を使用して JobPasscode を指定する GPD ファイルの例を次に示します。

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

**注**  使用する必要があります、\*から意図せずに表示されているオプションには、保護された印刷を防ぐために TRUE ConcealFromUI キーワードと設定します。 上記の GPD ファイルの例を参照してください。

 

インストール可能なハードウェア制約を使用して JobPasscode を指定する PPD ファイルの例を次に示します。

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

前の PPD ファイルの例でわかるように、 \*UIConstraints キーワードがハードウェアの制限を示します。

**注**  Windows オペレーティング システムは、保護された印刷機能とその関連するオプションのロケール固有の文字列を自動的に表示されます。 この機能またはオプションの場合は、新しいローカライズされた名前を指定することはできません。

 

**XPS 表示フィルター**

これらのドライバーは、暗証番号 (pin) の値の PrintTicket 形式をデバイスで認識される値に変換できるように、既存のデバイス用のドライバーは、レンダリング コードに変更を必要があります。 一般に、いずれかが必要になります、既存の XPS 表示フィルターにコードを追加または保護された印刷をサポートする新しい XPS 表示フィルターの追加。 PCL6 と PostScript 標準 XPS レンダリング フィルターを使用するドライバーは、フィルター パイプラインの新しいストリーム フィルターを開発する必要があります。 この新しいストリーム フィルターがストリームが標準のフィルターを通過した後は、そのフィルター パイプラインでは、描画前 PDL ストリームに適切なコマンドを挿入します。

、クライアントまたはサーバー コンピューター上のレンダリング要件を最小限に抑えるには、XPS または OpenXPS をサポートする新しいデバイスをサポートするように、新しいキーワード追加の変換を使用せずに Microsoft 提案されます。

**プリンターの拡張機能**

プリンターの拡張機能は、印刷設定 UI で保護された印刷コントロールを表示できる必要があります。 これにより、デスクトップ アプリのユーザーは、プリンターの拡張機能を使用する場合は、保護された印刷機能を構成できます。 Microsoft は、変更を行って、 [ **IPrintSchemaTicket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintschematicket)プリンターの拡張機能からの保護された印刷をサポートする Api のファミリです。

**UWP デバイス アプリ**

Microsoft は許可の変更を行っても、 [ **IPrintSchemaTicket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintschematicket)のコントロールを表示するデバイス アプリを UWP を使用する Api のファミリが、印刷設定 UI での印刷を保護します。

 

 




