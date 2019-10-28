---
title: フィルター パイプライン構成ファイルに関するページ
description: フィルター パイプライン構成ファイルに関するページ
ms.assetid: 586247bd-6d06-4728-a5f0-ee3fe1d09321
keywords:
- XPSDrv プリンタードライバー WDK、render モジュール
- レンダーモジュール WDK XPSDrv、フィルターパイプライン構成ファイル
- フィルターパイプライン構成ファイル WDK XPSDrv
- プライベートキーワード WDK XPSDrv
- フィルターパイプラインプロパティバッグ WDK XPSDrv
- プロパティバッグ WDK フィルターパイプライン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 341e1db13c2957bdd33cc5d26db92c5c4da5c65e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843259"
---
# <a name="filter-pipeline-configuration-file"></a>フィルター パイプライン構成ファイルに関するページ


*フィルターパイプライン構成ファイル*は、次のものを定義する XML ファイルです。

-   パイプライン内のフィルターの順序。 この順序は、フィルターパイプライン構成ファイル内の XML 要素の順序によって定義されます。

-   インターフェイスをフィルター処理します。 これらのインターフェイスは、フィルターパイプライン構成ファイルの XML 属性によって定義されます。

-   各フィルターの入力形式と出力形式。 これらの形式は、フィルターパイプライン構成ファイルの XML 要素によって定義されます。

次のコード例は、一般的なフィルターパイプライン構成ファイルを示しています。

```xml
<Filters>
    <Filter      dll="XDWMark.dll"
 clsid="{D647D658-BEF6-415f-AFAC-070D64074C5D}"
                name="Watermark filter">
        <Input  guid="{b8cf8530-5562-47c4-ab67-b1f69ecf961e}" comment="IID_IXpsDocumentProvider"/>
        <Output guid="{4368d8a2-4181-4a9f-b295-3d9a38bb9ba0}" comment="IID_IXpsDocumentConsumer"/>
    </Filter>
 <Filter dll="XDScale.dll"
 clsid="{B9B52406-92D3-4721-86E6-3CF78F6D5FC5}"
 name="Page Scaling filter">
 <Input guid="{4d47a67c-66cc-4430-850e-daf466fe5bc4}" comment="IID_IPrintReadStream"/>
 <Output guid="{65bb7f1b-371e-4571-8ac7-912f510c1a38}" comment="IID_IPrintWriteStream"/>
 </Filter>
    <Filter      dll="XDColMan.dll"
 clsid="{8E56FC37-0799-447e-A643-16F4FB18244C}"
 name="Colour Management filter">
         <Input guid="{b8cf8530-5562-47c4-ab67-b1f69ecf961e}" comment="IID_IXpsDocumentProvider"/>
        <Output guid="{4368d8a2-4181-4a9f-b295-3d9a38bb9ba0}" comment="IID_IXpsDocumentConsumer"/>
    </Filter>
    <Filter      dll="XDBook.dll"
 clsid="{7DFC96C6-CEA2-46d8-B354-887C47B7986D}"
                name="Booklet filter">
         <Input guid="{b8cf8530-5562-47c4-ab67-b1f69ecf961e}" comment="IID_IXpsDocumentProvider"/>
        <Output guid="{4368d8a2-4181-4a9f-b295-3d9a38bb9ba0}" comment="IID_IXpsDocumentConsumer"/>
    </Filter>
    <Filter      dll="XDNUp.dll"
 clsid="{1b5bee16-511c-440f-8017-2123f481091a}"
                name="NUp filter">
         <Input guid="{b8cf8530-5562-47c4-ab67-b1f69ecf961e}" comment="IID_IXpsDocumentProvider"/>
        <Output guid="{4368d8a2-4181-4a9f-b295-3d9a38bb9ba0}" comment="IID_IXpsDocumentConsumer"/>
    </Filter>
</Filters>
```

### <a name="private-keywords"></a>プライベートキーワード

[XPSDrv 構成モジュール](xpsdrv-configuration-module.md)は、 [**DrvDocumentEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent)関数呼び出し中に[XPS ドライバードキュメントイベント](xps-driver-document-events.md)を処理するときに、PrintTicket エントリに*プライベートキーワード*を含めることができます。 これらの PrintTicket エントリは、フィルターが PrintTicket を読み取っている間に、印刷フィルターパイプラインの処理フィルターによって読み取られます。

### <a name="filter-pipeline-property-bag"></a>フィルターパイプラインプロパティバッグ

構成モジュールは、*フィルターパイプラインプロパティバッグ*を使用してデータを格納したり、フィルターパイプラインに情報を渡したりすることもできます。 プロパティバッグを使用して構成サービスを公開するには、構成モジュールで**DrvPopulateFilterServices**メソッドをエクスポートする必要があります。 また、フィルターパイプライン構成ファイルには、各サービスの **&lt;FilterServiceProvider&gt;** 要素が含まれている必要があります。 プロバイダーモジュールは、 **DllCanUnloadNow**関数を実装してエクスポートする必要があります。 通常、これらのプロバイダーは、プロパティバッグに COM インターフェイスを公開します。 これらのインターフェイスを使用している間は、プロバイダーを読み込む必要があります。

もう1つの要素である、&lt;の [ **&gt;** ] を選択すると、サービスプロバイダーの dll が使用できない場合に、パイプラインマネージャーで印刷ジョブを続行できます。 個々のフィルターは、オプションのサービスプロバイダーが存在しない場合にその動作を定義する必要があります。 そうしないと **&lt;FilterServiceProvider&gt;** が使用され、dll を読み込めない場合、ジョブは失敗します。 **&lt;の&gt;** 要素は、Windows 7 以降でサポートされています。

次のコード例は、 **DrvPopulateFilterServices**関数を示しています。

```cpp
HRESULT
DrvPopulateFilterServices(
    __in IPrintPipelinePropertyBag  *pPropertyBag
    );
```

前の関数の詳細については、「 [**DrvPopulateFilterServices**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-drvpopulatefilterservices)」を参照してください。

次のコード例は、フィルターパイプライン構成ファイルの **&lt;FilterServiceProvider&gt;** 要素の XML 構文を示しています。

```xml
<Filters>
    <Filter ... />
    <FilterServiceProvider dll = "providerA.dll"/>
    <FilterServiceProvider dll = "providerB.dll"/>
</Filters>
```

### <a name="interleaving-mode-for-the-output-device"></a>出力デバイスのインターリーブモード

*インターリーブ*とは、XPS ドキュメントの個々のリソース部分を、FixedPage ドキュメントパーツと共にストリーム配信する方法を指します。 フィルターパイプラインによって、パイプラインで XPS ドキュメントインターフェイスを使用した最初のフィルター用の XPS ドキュメントオブジェクトモデルが作成されると、XPS スプールファイルのインターリーブ順序が適用されなくなります。 ただし、XPS ドキュメントインターフェイスを使用するパイプラインの最後のフィルターでは、XPS コンテンツをシリアル化するときにパイプラインが使用する、フィルター構成ファイルのインターリーブ順序を指定できます。 出力デバイスまたは出力ファイルと最も互換性のあるインターリーブ順序を選択すると、後続のドキュメント処理のパフォーマンスが向上します。

次のフィルターの例は、前の例のフィルター構成ファイルからの抜粋であり、インターリーブオプションの使用方法を示すために変更されています。 この例では、例として、両方のインターリーブオプションを示していますが、実際のフィルター構成ファイルには、フィルター定義内の **&lt;インターリーブ&gt;** 要素が1つだけあります。

```xml
    <Filter     dll="XDNUp.dll"
      clsid="{1b5bee16-511c-440f-8017-2123f481091a}"
        name="NUp filter">
      <Input guid="{b8cf8530-5562-47c4-ab67-b1f69ecf961e}" comment="IID_IXpsDocumentProvider"/>
       <Output guid="{4368d8a2-4181-4a9f-b295-3d9a38bb9ba0}" comment="IID_IXpsDocumentConsumer"/>
     <Interleaving mode="ResourcesFirst"\>
     <Interleaving mode="MarkupFirst"\>
    </Filter>
```

フィルターパイプラインでは、次のインターリーブ順序がサポートされています。

-   **Resourcesfirst**インターリーブ順序は、リソースに依存する FixedPage の前に依存する各リソースをストリームします。 このインターリーブ順序は、プリンタードライバーや直接使用プリンターの場合に適しています。これは、レンダリングが開始される直前に、プリンターがテキストとページのコンテンツをレンダリングするために必要なフォントおよびイメージリソースを提供するためです。

-   **MarkupFirst**インターリーブ順序は、ドキュメントのテキストとマークアップ、およびリソースが使用されてから実際のリソースをストリーミングする方法に関する情報をストリームします。 このインターリーブ順序は、アーカイブファイルの保存先と、ドキュメントをオンラインで表示するアプリケーションに最適です。

### <a name="archive-optimized-xps-output"></a>アーカイブに最適化された XPS 出力

この機能により、印刷ドライバーはアーカイブ最適化 XPS 出力をスプールファイルとして明示的に要求できます。 Windows 8 では、Microsoft XPS ドキュメントライター v4 (MXDW) は、Microsoft XPS Document Converter (MXDC) の MXDW でのみ使用できるコードパスを使用して、このアーカイブ対応 XPS 出力を生成します。 そのため、印刷ドライバーは、このアーカイブ最適化 XPS を MXDC から生成できます。

次のコード例は、フィルターパイプライン構成ファイルで &lt;Archive&gt; 要素を使用してこの機能を有効にする XML 構文を示しています。

```xml
<Filters>
    ...
    <Archive enabled="true"/>
</Filters>
```
