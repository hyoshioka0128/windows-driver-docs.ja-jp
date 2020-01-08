---
title: OpenXPS のドライバー サポート
description: OpenXPS は、ドキュメントの Open XML Paper Specification 形式であり、エクマインターナショナルの標準仕様に基づいています。
ms.assetid: 9BC9787E-A54D-4A11-B256-57BE5D206404
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a66f4e884e471cb576e802044cea57db2be113f
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652808"
---
# <a name="driver-support-for-openxps"></a>OpenXPS のドライバー サポート


OpenXPS は、ドキュメントの Open XML Paper Specification 形式であり、エクマインターナショナルの標準仕様に基づいています。

この仕様の最新情報については、「 [OPEN XML Paper specification](https://www.ecma-international.org/publications/standards/Ecma-388.htm)」を参照してください。

Windows 8 は OpenXPS を完全にサポートしており、既存の Microsoft XPS 形式を引き続きサポートしています。 このトピックでは、v4 ドライバーモデルによる OpenXPS のサポートに焦点を当てています。 Windows アプリケーション開発者に関連する OpenXPS サポートについては、「 [OpenXPS 印刷のアプリサポート](https://docs.microsoft.com/windows/desktop/printdocs/app-support-for-openxps-printing)」を参照してください。

## <a name="supported-openxps-scenarios"></a>サポートされている OpenXPS シナリオ


Windows 印刷パスは、送信された XPS 形式が対象の印刷ドライバーのサポートされている形式と一致するように開発され、必要に応じて形式が変換されます。 また、Windows は印刷ドライバーにクエリを実行するための Api も提供します。これにより、アプリケーションは互換性のある要素を提供し、印刷システム内での追加変換を回避できます。

印刷ドライバーは、そのマニフェストを使用して、Microsoft XPS、Open XPS、または両方の形式をサポートしているかどうかを示すことができます。 既存のストリームとオブジェクトモデル (OM) インターフェイスを使用して、Microsoft XPS または OpenXPS を印刷フィルターパイプラインのフィルターに提示できます。 OpenXPS をサポートするために、ドライバーは新しいインターフェイスを必要としません。 フィルターに表示される形式は、ドライバーでサポートされている形式、またはアプリケーションによって提供される形式によって異なります。

Microsoft XPS ドキュメントライター (MXDW) が更新され、MXDW が任意の Windows デスクトップアプリケーションから Microsoft XPS または OpenXPS を出力できるようになりました。 同様に、Windows 8 の Microsoft XPS ビューアーとリーダーアプリでも XPS 形式を開くことができます。 必要に応じて、ユーザーは XPS ビューアーから MXDW に印刷して、形式を変換することができます。

## <a name="unsupported-openxps-scenarios"></a>サポートされていない OpenXPS シナリオ


一部のレガシ機能はサポートされていないか、OpenXPS で使用したときにダウングレードされたエクスペリエンスを提供します。

サポートされて*いませ*ん: OpenXPS ファイルをスプーラに直接送信します (XPS 印刷 API をバイパス)。サポートされていないシナリオです。 この操作を行うと、次の機能の問題が発生します。

-   スプーラに直接送信された XPS スプールファイルは、MSXPS として扱われ、それに応じて処理されます。
-   OpenXPS ファイルをスプーラに直接送信した結果は未定義であるため、印刷ジョブが失敗する可能性があります。

このシナリオのサポートを提供する予定がない  に**注意**してください。

 

*推奨されません*: OpenXPS ストリームをアプリケーションから XPS 印刷 API に直接送信する方法はお勧めできません。 たとえば、OpenXPS ストリームを StartXPSPrintJob メソッドに直接送信しないでください。 これを行うと、あるフレーバーをストリームとして変換すると、パフォーマンスが非常に高くなる可能性があります。

代わりに、IPrintDocumentPackageTarget を使用して、印刷ジョブを XPS OM として送信し、パフォーマンスの低下を回避する必要があります。

*推奨されません*: XPS スプールファイルをスプーラに直接送信します。 これを行うと、印刷パス Api によって追加された必要なメタデータが印刷システムによって検出されず、形式が MSXPS であると想定され、OpenXPS への変換が試行されます。 スプーラに直接送信されたスプールファイルが OpenXPS 形式のファイルであった場合、印刷フィルターパイプラインによる OpenXPS への ' 変換 ' の試行は、未定義の結果になります。 スプーラに送信されたファイルが MSXPS 形式のファイルであり、ドライバーが OpenXPS のみのドライバーである場合、OpenXPS への印刷フィルターパイプラインによる変換は正常に実行されます。 ただし、この遅延段階の変換によって、印刷システムのパフォーマンスが大幅に低下します。

## <a name="impact-on-app-developers"></a>アプリ開発者への影響


OpenXPS の Windows 8 サポートに関するアプリ開発者への影響については、「 [App support For OpenXPS 印刷](https://docs.microsoft.com/windows/desktop/printdocs/app-support-for-openxps-printing)」を参照してください。

## <a name="impact-on-driver-developers"></a>ドライバー開発者への影響


V4 印刷ドライバーで OpenXPS を有効にするための基本的な手順を次に示します。

-   ドライバーマニフェスト: Driver Render セクションに "OpenXPS" を追加します。
-   ドライバーマニフェスト: FileSave セクションに "oxps" を追加します (該当する場合)。
-   フィルターパイプライン: 印刷フィルターを更新して OpenXPS 要素を処理します。

クライアントは、特定のストリームと、適切なオブジェクトインターフェイスを使用して、OpenXPS 形式を使用して、印刷フィルターパイプラインのフィルターにデータを転送できます。 データストリームを転送するために、クライアントは、IPrintReadStream および IID\_IPrintWriteStream インターフェイス\_の IID を使用します。 OM コンポーネントにデータを転送するために、クライアントは、の IID\_IXpsDocumentProvider と IID\_Ixpsdocumentprovider インターフェイスを使用します。 OpenXPS のサポートを宣言するドライバーは、パイプラインマネージャーからこの形式を受信するときに、指定された印刷フィルターが OpenXPS 形式を正しく処理できるようにする必要があります。

**ドライバーマニフェスト: DriverRender セクション**。 ドライバーのインストール中に、セットアッププロセスによってマニフェストの DriverRender セクションがチェックされ、XpsFormat エントリに OpenXPS が含まれているかどうかが確認されます。 XpsFormat エントリには、デュアルサポートを示すために XPS (for Microsoft XPS) と OpenXPS の両方を含めることができます。 XpsFormat エントリに表示される2つの形式の順序によって、ドライバーの優先形式が決まります。

DriverRender セクションを更新する方法の例をいくつか次に示します。

OpenXPS のみのサポートを示す:

```Manifest
[DriverRender]
XpsFormat = OpenXPS
```

MSXPS のみのサポートを示します。

```Manifest
[DriverRender]
XpsFormat = XPS
```

OpenXPS の設定を使用して、両方の形式のサポートを示します。

```Manifest
[DriverRender]
XpsFormat = OpenXPS,XPS
```

両方の形式のサポートを示します。 MSXPS の場合は次のようになります。

```Manifest
[DriverRender]
XpsFormat = XPS,OpenXPS
```

ドライバー開発者は、V4 印刷ドライバーに適した形式を決定します。この決定は、ドライバーが提供するように設計された機能に基づいて行われます。 たとえば、印刷ドライバーを開発して、再現性の高いイメージに対して JPEG XR のサポートを提供できます。

印刷システムは、マニフェスト内の DriverRender 情報に基づいてさまざまな決定を行います。 これらの決定の例をいくつか次に示します。

-   V4 ドライバーに送信された GDI ベースの印刷ジョブ

    Microsoft XPS Document Converter (MXDC) は、GDI 印刷ジョブの入力を受け取り、ジョブを XPS スプールファイルに変換します。 そのスプールファイルの形式は、マニフェストの DriverRender セクションに示されている優先 XPS 形式と一致します。

-   XPS 印刷 API 形式の変換

    XPS Print API は、サポートされている XPS 形式でターゲットドライバーを照会します。 ドライバーが両方の形式をサポートしている場合、XPS 印刷 API は、アプリケーションによって送信された XPS 印刷ジョブをスプーラに渡します。 変換は実行されません。

    ターゲットドライバーがサポートしている形式が1つまたはそれ以外の場合は、スプール前にジョブが正しい形式に変換されます。

    マニフェストで XpsFormat が指定されていない場合、動作は既定で MSXPS のみになります。 OpenXPS の入力が MSXPS に変換されます。 この動作により、ドライバーの最も強力な旧バージョンとの互換性が提供されます。

-   スプーラに直接送信される XPS ファイル

    スプーラに直接送信される XPS ファイルは、既定では MSXPS になります。 スプーラへの OpenXPS direct の送信はサポートされていません。 ただし、4.5 より前の .NET では、独自の MSXPS をシリアル化し、そのジョブをスプーラに直接送信していました。 この動作は、XPS 印刷 API (xp) の導入前に実装されました。

    これらの .NET アプリケーションの旧バージョンとの互換性を確保するために、印刷フィルターパイプラインマネージャーはスプールファイルをチェックして、直接スプーラを受信したかどうかを確認します。 その場合は、MSXPS と見なされます。 印刷フィルターパイプラインマネージャーは、その時点でドライバーの XPS 形式に対してクエリを実行します。 ドライバーが MSXPS をサポートしている場合、変換は実行されません。 ドライバーが OpenXPS のみをサポートしている場合は、印刷フィルターパイプラインマネージャーによってファイルの変換が実行されます。 ジョブのこの時点での変換はパフォーマンスが高くなります。ただし、従来の .NET アプリで新しい v4 OpenXPS ドライバーに印刷できるようになります。

**ドライバーマニフェスト: FileSave セクション**。 V4 印刷ドライバーマニフェストの FileSave セクションには、PORTPROMPT: ポートで使用される**ファイル保存**ダイアログの拡張機能が用意されています。 (PORTPROMPT: は、ファイルの代わりに使用する必要があります: Windows 8.1 では、アプリケーションが低権限モードで実行されている場合でも、ユーザーが権限を持っているすべてのファイルの場所にアクセスできるようにします)。FileSave セクションのエントリは、インデックスによって DriverRender セクションのエントリに関連付けられています。

次に例を示します。

```Manifest
[FileSave]
xps=0
oxps=0

[DriverRender]
XpsFormat=XPS,OpenXPS
```

これにより、ユーザーがこのドライバーに印刷ジョブを送信するときに、ポートが PORTPROMPT: に設定されていることを確認します。 **[ファイルの保存]** ダイアログでは、ダイアログのファイルの種類のオプションとして Xps と OpenXPS が表示され、ファイル拡張子としてそれぞれ .xps または oxps が適用されます。

マニフェストの [ファイルの保存] セクションのその他のオプションの詳細については、「 [V4 ドライバーマニフェスト](v4-driver-manifest.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

[OpenXPS 印刷のアプリサポート](https://docs.microsoft.com/windows/desktop/printdocs/app-support-for-openxps-printing)  

[Open XML Paper Specification](https://www.ecma-international.org/publications/standards/Ecma-388.htm) 

[V4 ドライバーマニフェスト](v4-driver-manifest.md)  
