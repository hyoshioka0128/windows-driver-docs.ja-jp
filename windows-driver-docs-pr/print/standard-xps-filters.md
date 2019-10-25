---
title: 標準の XPS フィルター
description: Windows には、XPS から PCL6 および PostScript レベル3への組み込み変換をサポートする2つの (標準) XPS フィルターが用意されています。
ms.assetid: 6404D215-8154-4604-A67B-19B20D1CF229
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97e210a972c6cc197adb1ef7976f64efb1e64053
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840401"
---
# <a name="standard-xps-filters"></a>標準の XPS フィルター


Windows には、XPS から PCL6 および PostScript レベル3への組み込み変換をサポートする2つの (標準) XPS フィルターが用意されています。

Windows に用意されているフィルターは、印刷クラスドライバーとモデル固有の v4 印刷ドライバーの両方で使用できます。 これらの XPS フィルターは、既存のファームウェア実装との互換性を確保するために、必要に応じて、ihv 機能フィルターおよび IHV 後処理フィルターと組み合わせることができます。

**メモ** これらの Windows 提供の XPS フィルターは再配布できず、v3 プリンタードライバーでは使用できません。



## <a name="the-manifest-file"></a>マニフェストファイル


Windows が提供する XPS フィルターを使用するには、v4 ドライバーマニフェストファイルで、 **Driverconfig**セクションの requiredfiles ディレクティブを使用してフィルターを指定する必要があります。 フィルターの名前は次のとおりです。

*MSxpsPCL6*。 XPS から PCL6 への変換を提供します。
*Msxp .dll*。 XPS から PostScript レベル3への変換を提供します。
これらのフィルターのいずれかを使用するために INF の更新は必要ありません。再配布はサポートされていません。
## <a name="print-filter-pipeline-configuration"></a>印刷フィルターパイプラインの構成


これらのフィルターを使用するように印刷フィルターパイプラインを構成するには、次の例に示すように構成ファイルを作成する必要があります。

PCL6 への変換を指定するサンプル構成ファイルです。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Filters>
  <Filter dll="MSxpsPCL6.dll" clsid="{3821E518-33AF-4d17-92B3-28EB410D46B6}" name="Microsoft XPS to PCL6">
    <Input guid="{4d47a67c-66cc-4430-850e-daf466fe5bc4}" comment="IID_IPrintReadStream" />
    <Output guid="{65bb7f1b-371e-4571-8ac7-912f510c1a38}" comment="IID_IPrintWriteStream" />
  </Filter>  
</Filters>
```

PostScript への変換を指定するサンプル構成ファイルです。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Filters>
  <Filter dll="MSxpsPS.dll" clsid="{8636D90A-5E03-4d62-9269-E06493C57473}" name="Microsoft XPS to PS">
    <Input guid="{4d47a67c-66cc-4430-850e-daf466fe5bc4}" comment="IID_IPrintReadStream" />
    <Output guid="{65bb7f1b-371e-4571-8ac7-912f510c1a38}" comment="IID_IPrintWriteStream" />
  </Filter>  
</Filters>
```

## <a name="supported-features"></a>サポートされる機能


標準の XPS フィルターでは、多くの一般的な機能がサポートされています。 すべての機能定義で、ドライバーの GPD ファイルまたは PPD ファイルが使用されます。 *MSxpsPCL6*フィルターでは、構成に GPD ファイルを使用する必要があります。また、 *msxp の .dll*フィルターでは、構成に PPD ファイルを使用する必要があります。 特に明記されていない限り、カスタム PDL コマンドを機能に対して指定すると、そのコマンドが使用されます。

挿入文字列が特定のセクション ( **\*Order**コマンドで指定) の下に存在する場合、GPD ファイルの場合は、フィルターによってそれらの文字列の内容に関するいくつかの仮定が行われ、既定のコマンドの送信が回避されます。 これは、この場合に既定のコマンドを送信すると、コマンドの競合が発生する可能性があるためです。 したがって、GPD ファイルの作成者は、次のガイドラインに従う必要があります。

-   ジョブ\_セットアップ。\# o A PCL6 バイナリストリームヘッダー (例: ")&lt;SP&gt;HP-UX XL; 1;&lt;CR&gt;&lt;LF&gt;") が存在している必要があります。
    o BeginSession 演算子は、必要なすべての属性を含めて存在する必要があります。
    o 必要なすべての属性を含め、OpenDataSource 演算子が存在する必要があります。
-   ページ\_セットアップ を設定します。\# o BeginPage 演算子が必要です。これには、すべての必須属性が含まれます。
-   ページ\_完了します。\# o EndPage 演算子が存在する必要があります。
-   ジョブ\_完了します。\# o CloseDataSource 演算子が存在している必要があります。
    o EndSession オペレーターが存在している必要があります。
    o EndPJLCommands 演算子が存在する必要があります。

XPS 標準フィルターは、適切な PDL データを生成して、\*PrintableArea、\*Printablearea、または \*ImageableArea コマンドに基づいて、ページの配信元を設定します。 また、予想される起点からの追加のオフセットを回避するために、GPD ファイルでは、用紙サイズの \*Cmd 文字列定義に = SetPageOrigin コマンドを指定しないでください。

標準の XPS フィルターでサポートされる PrintTicket 機能の詳細については、「[サポートされている Printticket 機能](supported-printticket-features.md)」を参照してください。

## <a name="retrieving-printticket-in-post-processing-filters"></a>後処理フィルターでの PrintTicket の取得


Windows 8 と共にリリースされた v4 ドライバーモデルでは、MSxps フィルターのいずれかの後に後処理フィルターを追加したときに、前処理フィルターを追加することが必要になる場合もあります。 ジョブレベルの印刷チケットをキャプチャするには、事前処理フィルターを追加する必要がありました。 しかし、このアプローチでは、ストリームベースの MSxps フィルターの前にオブジェクトモデルベースのフィルターを追加し、逆シリアル化を行い、その後、単に PrintTicket を抽出するために印刷データをシリアル化します。

Windows 8.1 では、ユーザーの既定の PrintTicket が MSxps フィルターのジョブレベルの PrintTicket とマージされ、結合された PrintTicket が印刷フィルターパイプラインのプロパティバッグに追加されます。 結合された PrintTicket は、ユーザーの PrintTicket と同じ方法で、印刷フィルターパイプラインのプロパティバッグに追加されます。 プロパティの名前は次のとおりです。

```cpp
#define XPS_FP_JOB_LEVEL_PRINTTICKET    "JobPrintTicket"
```

InitializeFilter では、MTI フィルターによって[Iprintreadstreamfactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory)の実装がプロパティバッグに追加されます。 このインターフェイスの1つのメソッドである**system.resources.resourcemanager.getstream**は、PrintTicket ストリームが使用可能になるまでブロックされます。 これにより、プロパティへのアクセスを同期することができます。

**重要**: **System.resources.resourcemanager.getstream**が initializefilter から呼び出されると、デッドロックが発生します。



## <a name="other-features"></a>その他の機能


標準の XPS フィルターでサポートされていない PrintTicket 機能の場合、フィルターはすべての PrintTicket メンバーをチェックして、GPD/PPD で参照されているかどうかを確認し、出力するコマンドを指定します。 指定されている場合は、指定したコマンドが生成されます。

GPD の機能は、次の順序でマップされます。

1. PrintSchemaKeywordMap 値が指定され、PrintTicket 機能名と一致します。

2. PrintSchemaPrivateNamespaceURI 属性が指定されており、GPD 機能名が PrintTicket 機能名と一致します。 一致する機能名は簡単ではなく、いくつかの規則に従います。

a. 最初のオプションの [ **\*の順序**] セクションが [ページ\_セットアップまたはページ\_完了] の場合、GPD 機能の先頭が "ページ" ではない場合は、"page" が GPD 機能名の前に付加されてから、一致が試みられます。

b. 最初のオプションの [ **\*の順序**] セクションが DOC\_セットアップまたは DOC\_FINISH で、GPD 機能の先頭が "document" でない場合は、照合を試行する前に、"document" が GPD 機能名の前に付加されます。

c. 最初のオプションの [ **\*の順序**] セクションが [ジョブ\_セットアップまたはジョブ\_完了] で、GPD 機能の先頭が "job" でない場合は、一致する前に、"job" が GPD 機能名の前に付加されます。

d. -Z\]、\[a-z\]、\[0-9\] または '\_' 以外の \[文字は、照合を試行する前に '\_' 文字に置き換えられます。 ただし、\*NoPunctuationCharSubstitute の場合は、属性が TRUE に設定されている場合、フィルターは '. ' に置き換えられません。 '\_' 文字を含むまたは '-'。

PPD 機能は、次の順序でマップされます。
1. PrintSchemaKeywordMap 値が指定され、PrintTicket 機能名と一致します。

2. PrintSchemaPrivateNamespaceURI 属性が指定され、PPD 機能名が PrintTicket 機能名と一致します。 一致する機能名は簡単ではなく、いくつかの規則に従います。

a. **Orderdependency**セクションが Exitserver、プロローグ、または JCLSetup で、ppd 機能名が "Job" で始まらない場合は、照合を試行する前に、"job" という名前が ppd 機能名の前に付加されます。

b. **Orderdependency**セクションが documentsetup で、ppd 機能名が "Document" で始まらない場合は、照合を試行する前に、"document" が ppd 機能名の前に付加されます。

c. **Orderdependency**セクションが anysetup の場合、フィルターは2つの一致チェックを実行します。

i. PPD 機能名が "Document" で始まらない場合は、照合を試行する前に、"Document" が PPD 機能名の前に付加されます。

ii. 一致するものが見つからない場合、または PPD 機能名が "Job" で始まらない場合は、照合を試行する前に、"Job" が PPD 機能名の前に付加されます。

d. **Orderdependency**セクションが PageSetup で、ppd 機能名が "Page" で始まらない場合は、一致する前に、"page" が ppd 機能名の前に付加されます。

e. -Z\]、\[a-z\]、\[0-9\] または '\_' 以外の \[文字は、照合を試行する前に '\_' 文字に置き換えられます。 ただし、\*MSNoPunctuationCharSubstitute の場合は、 文字列を TRUE に設定すると、フィルターは '. ' に置き換えられません。 '\_' 文字を含むまたは '-'。

GPD オプションと PPD オプションは、次の順序でマップされます。
1. PrintSchemaKeywordMap 値が指定され、PrintTicket オプション名と一致します。

2. PrintSchemaPrivateNamespaceURI 属性が指定されており、GPD/PPD オプション名が PrintTicket オプション名と一致します。 一致するオプション名は簡単ではなく、いくつかの規則に従います。

a. GPD/PPD オプション名が \[0-9\] または '\_' で始まる場合、照合を試行する前に、'\_' 文字が GPD/PPD オプション名の前に付加されます。 ただし、次の追加の規則が適用されます。

i. これが GPD オプションであり、\*NoPunctuationCharSubstitute の場合は、属性が TRUE に設定されている場合、フィルターは '\_' の前に '\_' 文字を付加しません。

ii. これが PPD オプションであり、\*MSNoPunctuationCharSubstitute の場合は、文字列が TRUE に設定されている場合、フィルターは '\_' の前に '\_' 文字を付加しません。

b. -Z\]、\[a-z\]、\[0-9\] または '\_' 以外の \[文字は、照合を試行する前に '\_' 文字に置き換えられます。 ただし、次の追加の規則が適用されます。

i. これが GPD オプションであり、\*NoPunctuationCharSubstitute の場合は、属性が TRUE に設定されている場合、フィルターは '. ' に置き換えられません。 '\_' 文字を含むまたは '-'。

ii. これが PPD オプションであり、\*MSNoPunctuationCharSubstitute の場合は、文字列が TRUE に設定されている場合、フィルターは '. ' に置き換えられません。 '\_' 文字を含むまたは '-'。

## <a name="form-to-tray-mapping"></a>フォームからトレイへのマッピング


XPS to PCL6 および XPS to PS フィルターでは、フォームからトレイへのマッピングテーブルがサポートされています。 複数のトレイで選択したメディアサイズ (たとえば、文字) がサポートされている場合、フィルターは次のように結合を解除します。

1. GPD ファイルまたは PPD ファイルで指定されている既定のトレイが、指定されたメディアサイズを使用するように構成されている場合は、既定のトレイが使用されます。

2. それ以外の場合、フィルターは、指定したメディアサイズで構成されている最初のトレイ (GPD/PPD ファイルで指定されている上から下のトレイ) を選択します。

## <a name="extra-backside-page-suppression"></a>余分なバックページ抑制


既定では、XPS to PCL6 および XPS to PS フィルターは、空のページを挿入することによって、メディアサイズ、メディアタイプ、入力ビン、出力ビンが混在するドキュメントの両面印刷を処理します。 フィルターによってこの空のページが挿入されると、新しいメディアの前に次のページが印刷されます。 バックページを出力する必要がないデバイスでは、次のキーワードをドライバーの GPD または PPD ファイルに追加することで、この動作を抑制できます。

| ファイルの種類 | バック page 抑制キーワード    |
|-----------|--------------------------------------|
| GPD       | \*SuppressExtraBacksidePages?: TRUE  |
| PPD       | \*MSSuppressExtraBacksidePages: True |



## <a name="optimizing-setpagedevice-commands"></a>SetPageDevice コマンドの最適化


Msxp でドライバーを使用する PostScript デバイスの既定の動作では、すべてのページに対して SetPageDevice コマンドが発行されます。このコマンドは、ページに対して指定されたすべてのオプションのセットを示します。 この手法では、一部のデバイスがうまく動作しない場合があることに注意してください。

ただし、デバイスで Msxp の .dll を使用していて、付随する PPD ファイルによって **\*Ms最適化 Izesetpagedevice: True**が指定されている場合は、次のような PostScript デバイスの動作が行われます。SetPageDevice コマンドページに対して指定されているオプションのセットを示す新しい SetPageDevice コマンドが発行されます。 ただし、前のページ以降に SetPageDevice コマンドの一部が変更されていない場合は、そのページに対して SetPageDevice コマンドは発行されません。

## <a name="related-topics"></a>関連トピック
[サポートされている PrintTicket 機能](supported-printticket-features.md)  
[V4 プリンタードライバーのレンダリング](v4-driver-rendering.md)  



