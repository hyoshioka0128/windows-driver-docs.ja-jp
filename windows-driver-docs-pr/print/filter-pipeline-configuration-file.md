---
title: フィルター パイプライン構成ファイルに関するページ
description: フィルター パイプライン構成ファイルに関するページ
ms.assetid: 586247bd-6d06-4728-a5f0-ee3fe1d09321
keywords:
- XPSDrv プリンター ドライバー WDK、モジュールを表示します。
- WDK XPSDrv モジュールを表示、フィルター パイプライン構成ファイル
- フィルター パイプライン構成ファイルを WDK XPSDrv
- プライベート キーワード WDK XPSDrv
- パイプラインのプロパティ バッグ WDK XPSDrv をフィルター処理します。
- プロパティ バッグ WDK フィルター パイプライン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3998e550f4abf47a937242617042c5bc7d0a0a46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382585"
---
# <a name="filter-pipeline-configuration-file"></a>フィルター パイプライン構成ファイルに関するページ


*フィルター パイプライン構成ファイル*は、次を定義する XML ファイルです。

-   パイプライン内のフィルターの順序。 この順序は、フィルター パイプライン構成ファイル内の XML 要素の順序によって定義されます。

-   インターフェイスをフィルター処理します。 これらのインターフェイスは、フィルター パイプライン構成ファイル内の XML 属性によって定義されます。

-   各フィルターの入力と出力の形式。 これらの形式は、フィルター パイプライン構成ファイル内の XML 要素によって定義されます。

次のコード例では、一般的なフィルター パイプライン構成ファイルを示します。

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

### <a name="private-keywords"></a>Private キーワード

[XPSDrv 構成モジュール](xpsdrv-configuration-module.md)配置できる*プライベート キーワード*PrintTicket のエントリを処理する際に、 [XPS ドライバーのドキュメント イベント](xps-driver-document-events.md)中に、 [ **DrvDocumentEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentevent)関数呼び出し。 これらの PrintTicket エントリは、フィルターは、PrintTicket の読み取り中に印刷フィルター パイプラインで処理フィルターによって読み取られます。

### <a name="filter-pipeline-property-bag"></a>パイプラインのプロパティ バッグをフィルター処理します。

構成モジュールを使用することも、*フィルター パイプラインのプロパティ バッグ*データを格納するか、フィルター パイプラインに情報を渡します。 プロパティ バッグを使用して、構成サービスを公開するには構成モジュールをエクスポートする必要があります、 **DrvPopulateFilterServices**メソッド。 さらに、フィルター パイプライン構成ファイルを含める必要があります、 **&lt;FilterServiceProvider&gt;** サービスごとの要素。 プロバイダーのモジュールを実装およびエクスポートする必要があります、 **DllCanUnloadNow**関数。 通常、これらのプロバイダーは、プロパティ バッグ内の COM インターフェイスを公開します。 プロバイダーは、これらのインターフェイスが使用中にアンロードする必要があります維持します。

別の要素、  **&lt;OptionalFilterServiceProvider&gt;** 、により、パイプラインをサービス プロバイダーの dll が利用できない場合は、印刷ジョブを続行するマネージャー。 個別のフィルターは、省略可能なサービス プロバイダーがない場合、動作を定義する必要があります。 の場合 **&lt;FilterServiceProvider&gt;** されると、dll を読み込むことができません、ジョブが失敗します。 **&lt;OptionalFilterServiceProvider&gt;** 要素は、Windows 7 以降でサポートされています。

次のコード例は、 **DrvPopulateFilterServices**関数。

```cpp
HRESULT
DrvPopulateFilterServices(
    __in IPrintPipelinePropertyBag  *pPropertyBag
    );
```

前の関数の詳細については、次を参照してください。 [ **DrvPopulateFilterServices**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nf-filterpipeline-drvpopulatefilterservices)します。

次のコード例の XML 構文を示しています、 **&lt;FilterServiceProvider&gt;** フィルター パイプライン構成ファイル内の要素。

```xml
<Filters>
    <Filter ... />
    <FilterServiceProvider dll = "providerA.dll"/>
    <FilterServiceProvider dll = "providerB.dll"/>
</Filters>
```

### <a name="interleaving-mode-for-the-output-device"></a>出力デバイスのモードをインターリーブ

*インターリーブ*FixedPage のドキュメント パーツと共に、XPS ドキュメントの個々 のリソース部分をストリーミングする方法を参照します。 フィルター パイプラインは、パイプライン内の XPS ドキュメントのインターフェイスを持つ最初のフィルターは、XPS ドキュメント オブジェクト モデルを作成するとき、XPS スプール ファイルのインターリーブの順序の後に不要になった。 ただし、XPS ドキュメントのインターフェイスを使用して、パイプラインで最後のフィルターは、XPS コンテンツをシリアル化時に使用するパイプラインのフィルターの構成ファイルでインターリーブの順序を指定できます。 出力デバイスまたは出力ファイルで最も互換性のあるインターリーブの順序を選択すると、ドキュメントの後続の処理のパフォーマンスを向上させることができます。

次のフィルターの例は、インターリーブのオプションを使用する方法について説明するように変更されている前の例フィルター構成ファイルから抜粋です。 この例では、説明のために両方のインターリーブ オプションでは、実際のフィルターの構成ファイルが、1 つだけ **&lt;Interleaving&gt;** フィルターの定義内の要素。

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

フィルター パイプラインには、次のインターリーブ注文がサポートされています。

-   **ResourcesFirst** FixedPage リソースに依存する前に依存する各リソースのストリームの順序をインターリーブします。 このインターリーブの順序はコンテンツにレンダリングするテキストとページ レンダリングが開始する前に、プリンターが必要なフォントおよびイメージ リソースを提供するための使用量が直接プリンターとプリンター ドライバーの適切です。

-   **MarkupFirst**ドキュメントのテキストとマークアップと実際のリソースをストリームする前のリソースの使用方法については、ストリームの順序をインターリーブします。 このインターリーブの順序は、アーカイブ ファイルの送信先やオンライン ドキュメントを表示するアプリケーションに最適なは。

### <a name="archive-optimized-xps-output"></a>XPS のアーカイブ用に最適化された出力

この機能は、印刷ドライバー操作のスプール ファイルとして XPS のアーカイブ用に最適化された出力を明示的に要求を使用できます。 Windows 8 で、Microsoft XPS Document Writer v4 (MXDW) のみ MXDW Microsoft XPS ドキュメント コンバーター (MXDC) で使用可能なコード パスを経由してこのアーカイブ可能な XPS の出力を生成します。 したがって、印刷ドライバーでは、MXDC からこのアーカイブに最適化された XPS を生成できます。

次のコード例を使用する XML 構文を示しています、&lt;アーカイブ&gt;この機能を有効にするフィルター パイプライン構成ファイル内の要素。

```xml
<Filters>
    ...
    <Archive enabled="true"/>
</Filters>
```
