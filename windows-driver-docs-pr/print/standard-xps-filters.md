---
title: 標準 XPS フィルター
description: Windows では、レベル 3 の XPS から PCL6 と PostScript への組み込みの変換をサポートするために 2 つの (標準) XPS フィルターを提供します。
ms.assetid: 6404D215-8154-4604-A67B-19B20D1CF229
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2f82f26ffdd457ef1580d20cae2cbf1ff788c33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363980"
---
# <a name="standard-xps-filters"></a>標準 XPS フィルター


Windows では、レベル 3 の XPS から PCL6 と PostScript への組み込みの変換をサポートするために 2 つの (標準) XPS フィルターを提供します。

Windows で提供されるフィルターの印刷クラス ドライバーとモデルに固有の v4 プリンター ドライバーの両方を利用できます。 既存のファームウェアの実装との互換性を確保するために必要に応じて、IHV 処理後のフィルターと同様に機能のフィルターを IHV これら XPS のフィルターを結合できます。

**注**これらの Windows で提供される XPS フィルターは、再頒布可能でないしは v3 プリンター ドライバーを使用できません。



## <a name="the-manifest-file"></a>マニフェスト ファイル


V4 ドライバー マニフェスト ファイルを Windows で提供される XPS フィルターを使用する RequiredFiles ディレクティブを使用する必要があります、 **DriverConfig**フィルターを指定するセクション。 これらは、フィルターの名前です。

*MSxpsPCL6.dll*します。 XPS から PCL6 への変換を提供します。
*MSxpsPS.dll*します。 XPS から PostScript レベル 3 への変換を提供します。
これらのフィルターのいずれかを利用する INF の更新プログラムは必要ありませんし、再配布がサポートされていません。
## <a name="print-filter-pipeline-configuration"></a>印刷フィルター パイプラインの構成


これらのフィルターを使用する印刷フィルター パイプラインを構成するには、次の例に示すように構成ファイルを作成する必要があります。

PCL6 への変換を示すサンプル構成ファイルです。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Filters>
  <Filter dll="MSxpsPCL6.dll" clsid="{3821E518-33AF-4d17-92B3-28EB410D46B6}" name="Microsoft XPS to PCL6">
    <Input guid="{4d47a67c-66cc-4430-850e-daf466fe5bc4}" comment="IID_IPrintReadStream" />
    <Output guid="{65bb7f1b-371e-4571-8ac7-912f510c1a38}" comment="IID_IPrintWriteStream" />
  </Filter>  
</Filters>
```

PostScript への変換を示すサンプル構成ファイルです。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Filters>
  <Filter dll="MSxpsPS.dll" clsid="{8636D90A-5E03-4d62-9269-E06493C57473}" name="Microsoft XPS to PS">
    <Input guid="{4d47a67c-66cc-4430-850e-daf466fe5bc4}" comment="IID_IPrintReadStream" />
    <Output guid="{65bb7f1b-371e-4571-8ac7-912f510c1a38}" comment="IID_IPrintWriteStream" />
  </Filter>  
</Filters>
```

## <a name="supported-features"></a>サポートされている機能


標準の XPS フィルターは、多くの一般的な機能をサポートします。 すべての機能の定義は、ドライバーの GPD または PPD ファイルを使用します。 *MSxpsPCL6.dll*フィルター GPD ファイルの使用に必要な構成では、および*MSxpsPS.dll*フィルター構成 PPD ファイルの使用が必要です。 明記されない限り、機能のカスタムの PDL コマンドが指定されている場合、それが使用されます。

挿入文字列は、特定のセクションが存在する場合 (指定されている、 **\*順序**コマンド)、GPD のファイルの場合、フィルターは多くのこれらの文字列のコンテンツに関する仮定すると、されが回避されます既定のコマンドを送信します。 これはため、既定のコマンドの送信はここでコマンドの衝突を発生可能性があります。 そのため GPD ファイルの作成者はこれらのガイドラインに従う必要があります。

-   ジョブ\_セットアップ\#o A PCL6 バイナリ Stream ヘッダー (例:")&lt;SP&gt;HP PCL XL; 1;&lt;CR&gt;&lt;LF&gt;") が存在する必要があります。
    すべての必須属性を含む o A BeginSession オペレーターが存在する必要があります。
    すべての必須属性を含む o An OpenDataSource オペレーターが存在する必要があります。
-   ページ\_セットアップ\#必要なすべての属性を含む、o A BeginPage オペレーターが存在する必要があります。
-   ページ\_完了。\# o An EndPage オペレーターが存在する必要があります。
-   ジョブ\_完了。\# o A CloseDataSource オペレーターが存在する必要があります。
    o An EndSession オペレーターが存在する必要があります。
    o An EndPJLCommands オペレーターが存在する必要があります。

XPS の標準的なフィルターの生成の PDL に適したデータに基づいて、ページの配信元の設定を\*PrintableArea、 \*PrintableOrigin または\*ImageableArea コマンド。 予想される配信元から追加のオフセットを回避するために GPD ファイルはいずれも指定しないと = SetPageOrigin コマンドで、\*用紙サイズの Cmd 文字列定義。

標準的な XPS フィルター、参照によってサポートされている PrintTicket 機能の詳細については[PrintTicket でサポートされる機能](supported-printticket-features.md)します。

## <a name="retrieving-printticket-in-post-processing-filters"></a>処理後のフィルターで PrintTicket を取得します。


MSxps のいずれかをフィルター処理した後、処理後のフィルターを追加したときに、Windows 8 でリリースされた v4 ドライバー モデルでも、処理前のフィルターを追加する必要があります。 処理前のフィルターを追加するジョブ レベルの印刷チケットをキャプチャする必要があります。 このアプローチは、オブジェクト モデルに基づくフィルター、フィルターの 1 つのストリーム ベース MSxps、結果として逆シリアル化し、印刷、PrintTicket を抽出するデータのシリアル化する前に本質的に追加します。

Windows 8.1 では、ユーザーの既定 PrintTicket MSxps フィルターでは、ジョブ レベル PrintTicket とマージされた PrintTicket とマージし、印刷フィルター パイプラインのプロパティ バッグに追加します。 マージされた PrintTicket は、ユーザー PrintTicket と同じ方法での印刷フィルター パイプラインのプロパティ バッグに追加されます。 プロパティの名前が次のとおりです。

```cpp
#define XPS_FP_JOB_LEVEL_PRINTTICKET    "JobPrintTicket"
```

実装の追加は InitializeFilter、中に MTI フィルター [IPrintReadStreamFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nn-filterpipeline-iprintreadstreamfactory)プロパティ バッグにします。 このインターフェイスの 1 つのメソッド、 **GetStream**、PrintTicket ストリームが利用可能になるまでブロックされます。 これは、プロパティへのアクセスを同期する手段を提供します。

**重要な**:場合**GetStream**呼びます InitializeFilter からデッドロックが発生します。



## <a name="other-features"></a>その他の機能


場合は、標準の XPS フィルターによってサポートされていない PrintTicket 機能フィルターは PrintTicket のすべてのメンバー/PPD、GPD で参照されるかどうかを確認してくださいし、出力するコマンドを指定します。 そうである場合は、指定されたコマンドが生成されます。

GPD 機能は、次の順序でマップされます。

1. PrintSchemaKeywordMap 値が指定され、PrintTicket 機能の名前と一致します。

2. PrintSchemaPrivateNamespaceURI 属性を指定し、GPD 機能名 PrintTicket の機能名に一致します。 機能名を照合する、簡単ではありませんし、さまざまなルールに従います。

a. 場合、 **\*順序**最初のオプションのセクションがページ\_セットアップまたはページ\_終了日、および GPD 機能が「ページ」で始まっていませんしを試みる前に、GPD 機能名に「ページ」が付加されます一致します。

b. 場合、 **\*順序**最初のオプションのセクションは、DOC\_セットアップまたはドキュメント\_終了日、および GPD 機能が"Document"で始まっていませんし、"Document"の先頭に付加する前に GPD 機能名一致するようにしようとしています。

c. 場合、 **\*順序**最初のオプションのセクションは、ジョブ\_セットアップまたはジョブ\_終了日、および GPD 機能が"Job"で始まっていませんし、一致するように試行する前に、GPD 機能名を「ジョブ」が付加されます.

d. 任意の文字でない\[A ~ Z\]、 \[a ~ z\]、 \[0 ~ 9\]または '\_' が置き換えられます、'\_' 一致を試みる前に文字。 ただし場合、 \*NoPunctuationCharSubstitute でしょうか属性が TRUE に設定し、フィルターは置き換えられません '。 '。 または '-' で、'\_' 文字。

PPD 機能は、次の順序でマップされます。
1. PrintSchemaKeywordMap 値を指定して、PrintTicket 機能の名前に一致します。

2. PrintSchemaPrivateNamespaceURI 属性を指定し、PPD 機能名 PrintTicket 機能名が一致します。 機能名を照合する、簡単ではありませんし、さまざまなルールに従います。

a. 場合、 **OrderDependency**セクションは ExitServer、プロローグまたは JCLSetup、し PPD 機能名が"Job"で始まらない、一致するように試行する前に、PPD 機能名を「ジョブ」が付加されます。

b. 場合、 **OrderDependency**セクションでは、DocumentSetup し PPD 機能名が"Document"で始まらないが"Document"一致を試みる前に PPD 機能名に付加されます。

c. 場合、 **OrderDependency**セクションは AnySetup、フィルターは、2 つの一致チェックを実行します。

i. PPD 機能名が"Document"で始まっていない場合、"Document"前に付加されます PPD 機能名と一致する前にします。

ii. 一致が検出されない場合、または PPD 機能名が"Job"で始まらない場合は、し、"Job"の先頭に付加 PPD 機能名一致を試みる前にします。

d. 場合、 **OrderDependency**セクションでは、PageSetup し PPD 機能名が「ページ」で始まらない、一致するように試行する前に、PPD 機能名を「ページ」が付加されます。

e. 任意の文字でない\[A ~ Z\]、 \[a ~ z\]、 \[0 ~ 9\]または '\_' が置き換えられます、'\_' 一致を試みる前に文字。 ただし場合、 \*MSNoPunctuationCharSubstitute でしょうか。 文字列が TRUE に設定されて、フィルターは置き換えられません '.' または '-' で、'\_' 文字。

GPD と PPD オプションは、次の順序でマップされます。
1. PrintSchemaKeywordMap 値を指定して、PrintTicket のオプション名と一致します。

2. PrintSchemaPrivateNamespaceURI 属性を指定し、GPD/PPD オプション名 PrintTicket のオプション名に一致します。 オプション名に一致する、簡単ではありませんし、さまざまなルールに従います。

a. GPD/PPD のオプション名で始まる場合\[0 ~ 9\]または '\_' を '\_' 文字が一致するように試行する前に GPD/PPD オプション名に付加されます。 ただし、次の追加ルールが適用されます。

i. GPD オプションでは、この場合、 \*NoPunctuationCharSubstitute でしょうか。 属性が TRUE に設定し、フィルターは付加されません '\_' で、'\_' 文字。

ii. PPD オプションでは、この場合、 \*MSNoPunctuationCharSubstitute でしょうか。 文字列が TRUE に設定し、フィルターは付加されません '\_' で、'\_' 文字。

b. 任意の文字でない\[A ~ Z\]、 \[a ~ z\]、 \[0 ~ 9\]または '\_' が置き換えられます、'\_' 一致を試みる前に文字。 ただし、次の追加ルールが適用されます。

i. GPD オプションでは、この場合、 \*NoPunctuationCharSubstitute でしょうか属性が TRUE に設定し、フィルターは置き換えられません '。 '。 または '-' で、'\_' 文字。

ii. PPD オプションでは、この場合、 \*MSNoPunctuationCharSubstitute でしょうか文字列が TRUE に設定し、フィルターは置き換えられません '。 '。 または '-' で、'\_' 文字。

## <a name="form-to-tray-mapping"></a>フォーム トレイへのマッピングから


PCL6 を XPS と XPS PS フィルターには、用紙トレイ マッピング テーブルをサポートします。 選択したメディア サイズ (文字など) をサポートして複数のトレイ、同順位がとおり中断フィルター。

1. (GPD または PPD ファイルで指定) と同じ既定のトレイを構成するには、指定されたメディアのサイズを使用する、既定のトレイが使用されます。

2. フィルターが最初のトレイ (上から下 GPD/PPD ファイルで指定された) を選択する場合は、指定したメディア サイズで構成されます。

## <a name="extra-backside-page-suppression"></a>余分なページのバックの抑制


PCL6 を XPS と XPS PS フィルターには、既定を空のページを挿入することで、メディアの混在のサイズ、メディアの種類、入力または出力のビンを含むドキュメントの両面印刷を処理します。 フィルターは、この空のページを挿入するときに新しいメディアの先頭に次のページを印刷するデバイスを強制します。 デバイスのバックのページ出力を必要としない場合、ドライバーの GPD または PPD ファイルに次のキーワードを追加することでこの動作を抑制できます。

| ファイルの種類 | バック ページ抑制キーワード    |
|-----------|--------------------------------------|
| GPD       | \*SuppressExtraBacksidePages:TRUE  |
| PPD       | \*MSSuppressExtraBacksidePages:True |



## <a name="optimizing-setpagedevice-commands"></a>SetPageDevice コマンドを最適化します。


MSxpsPS.dll でドライバーを使用する PostScript デバイスの既定の動作は SetPageDevice コマンドは、すべてのページの発行し、このコマンドは、ページの指定したオプションの完全なセットを示すことです。 一部のデバイスはこの手法でうまくが実行されていないことに注意してください。

ただし場合は、デバイスは MSxpsPS.dll と付随する PPD ファイルを使用して指定 **\*MSOptimizeSetPageDevice:True**、PostScript デバイスの動作を次に、: - すべてのページを指定されたオプションのセットを示すために新しい SetPageDevice コマンドが発行される前のページから SetPageDevice コマンドの一部が変更された、場所ページです。 ただし、なかった SetPageDevice コマンドの一部の変更前のページから SetPageDevice コマンドは、ページには発行されませんし、場合。

## <a name="related-topics"></a>関連トピック
[サポートされている PrintTicket 機能](supported-printticket-features.md)  
[V4 プリンター ドライバーの表示](v4-driver-rendering.md)  



