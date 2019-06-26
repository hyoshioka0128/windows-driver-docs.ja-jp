---
title: OpenXPS のドライバー サポート
description: OpenXPS とは、ドキュメントの Open XML Paper Specification 形式と Ecma International 標準仕様に基づきます。
ms.assetid: 9BC9787E-A54D-4A11-B256-57BE5D206404
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eacd891d04639d229463d97c4efda6990faa64ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356065"
---
# <a name="driver-support-for-openxps"></a>OpenXPS のドライバー サポート


OpenXPS とは、ドキュメントの Open XML Paper Specification 形式と Ecma International 標準仕様に基づきます。

この仕様に関する最新情報のほとんどで、次を参照してください。 [Open XML Paper Specification](http://www.ecma-international.org/publications/standards/Ecma-388.htm)します。

Windows 8 では、OpenXPS では、既存の Microsoft XPS 形式の継続的なサポートと並行して完全にサポートを提供します。 このトピックでは、v4 ドライバー モデルを使用して OpenXPS サポートについて説明します。 Windows アプリケーション開発者に関連する OpenXPS サポートについては、次を参照してください。 [OpenXPS を印刷するためのアプリのサポート](https://docs.microsoft.com/windows/desktop/printdocs/app-support-for-openxps-printing)します。

## <a name="supported-openxps-scenarios"></a>サポートされている OpenXPS シナリオ


Windows 印刷パスでは、送信された XPS 形式、対象となる印刷ドライバーのサポートされる形式に一致させる開発が完了され、必要に応じて、形式が変換されます。 Windows では、アプリケーション互換性のある要素を提供したり、印刷システム内で、追加の変換を回避できるように、印刷ドライバーでは、クエリを実行するための Api も提供します。

印刷ドライバーでは、Microsoft XPS、Open XPS、または両方の形式をサポートするかどうかを示す、自らのマニフェストを使用できます。 いずれか印刷フィルター パイプライン内のフィルターには、Microsoft XPS または OpenXPS を提示すること、(OM) インターフェイス – 新しいインターフェイスは必要ありませんドライバーで OpenXPS をサポートするために既存のストリームとオブジェクト モデルを使用します。 フィルターに提示される形式は、ドライバーでサポートされている形式、またはアプリケーションによって提供される形式に依存します。

任意の Windows デスクトップ アプリケーションから Microsoft XPS または OpenXPS のいずれかを出力する MXDW を許可する、Microsoft XPS ドキュメント ライター (MXDW) が更新されました。 同様に、Microsoft XPS ビューアーと Windows 8 のリーダー アプリでは、両方の XPS 形式を開くことができます。 必要な場合、ユーザーが印刷できる XPS ビューアーから MXDW を形式に変換するためにします。

## <a name="unsupported-openxps-scenarios"></a>OpenXPS サポートされていないシナリオ


一部のレガシ機能がサポートされていないか、または OpenXPS と併用すると、ダウン グレードされたエクスペリエンスを提供します。

*サポートされていない*:OpenXPS ファイル (XPS 印刷 API をバイパスする)、スプーラーを直接送信は、サポートされていないシナリオです。 これを行うと、次の機能の問題が生成されます。

-   XPS スプール ファイルが、スプーラーに直接送信は MSXPS として扱われ、それに応じて処理します。
-   スプーラーに直接、OpenXPS ファイルを送信の結果は未定義とは、印刷ジョブが失敗が発生する可能性があります。

**注**  このシナリオのサポートを提供する予定はありません。

 

*使用しないで*:送信、OpenXPS ストリーム XPS 印刷 API に直接アプリケーションからが推奨される方法です。 など、OpenXPS ストリームを StartXPSPrintJob メソッドに直接送信しないでください。 これを行うと、結果として得られるフレーバーを 1 つからの変換 XPS ストリームとして別にはパフォーマンスに非常に高価なできます。

代わりに、IPrintDocumentPackageTarget を使用して、パフォーマンスの低下を回避するために、XPS OM として印刷ジョブを送信する必要があります。

*使用しないで*:スプーラーに直接 XPS スプール ファイルを送信します。 これを行う場合、印刷システムはしない印刷パス Api によって追加された必要なメタデータが見つかりません、OpenXPS への変換を試みます。 形式は MSXPS を想定しています。 OpenXPS 形式のファイル、スプール ファイル スプーラーに直接送信された場合は、印刷フィルター パイプラインで OpenXPS に 'convert' しよう、結果は未定義がされます。 スプーラーに送信されたファイルが MSXPS 形式のファイルと、ドライバーは、OpenXPS 専用ドライバー場合、は、印刷フィルター パイプラインで OpenXPS への変換が成功になります。 この遅延の段階の変換と、印刷システムのパフォーマンスが大幅に低下します。

## <a name="impact-on-app-developers"></a>アプリ開発者への影響


OpenXPS for Windows 8 のサポートに関して、アプリ開発者の影響の詳細については、次を参照してください。 [OpenXPS を印刷するためのアプリのサポート](https://docs.microsoft.com/windows/desktop/printdocs/app-support-for-openxps-printing)します。

## <a name="impact-on-driver-developers"></a>ドライバー開発者への影響


以下は、v4 印刷ドライバーで OpenXPS を有効にするための基本的な手順です。

-   ドライバー マニフェスト:ドライバーの表示セクションには、"OpenXPS"を追加します。
-   ドライバー マニフェスト:該当する場合は、FileSave セクションに"oxps"を追加します。
-   フィルター パイプライン:OpenXPS 要素を処理する印刷フィルターを更新します。

指定されたストリームと、適切なオブジェクトのインターフェイスでは、クライアントは、印刷フィルター パイプライン内のフィルターのデータを転送するのに OpenXPS 形式を使用できます。 クライアントが、IID を使用するには、データ ストリームを転送するには、\_IPrintReadStream と IID\_IPrintWriteStream インターフェイス。 クライアントが、IID を使用するには、OM コンポーネントにデータを転送する\_IXpsDocumentProvider と IID\_IXpsDocumentConsumer インターフェイス。 OpenXPS のサポートを宣言するドライバーを提供する印刷フィルター処理できるように正しく OpenXPS 形式この形式は、パイプライン マネージャーから受信したときにする必要があります。

**ドライバー マニフェスト:DriverRender セクション**します。 ドライバーのインストール中には、セットアップ プロセスは、XpsFormat エントリ OpenXPS が含まれているかどうかに、マニフェストの DriverRender セクションを確認します。 XpsFormat エントリには、デュアル サポートを示すために、(Microsoft XPS) の XPS および OpenXPS の両方を含めることができます。 XpsFormat エントリで 2 つの形式が表示される順序は、ドライバーの優先形式を決定します。

DriverRender セクションを更新する方法の例をいくつかを示します。

OpenXPS のみのサポートを示します。

```Manifest
[DriverRender]
XpsFormat = OpenXPS
```

MSXPS のみのサポートを示します。

```Manifest
[DriverRender]
XpsFormat = XPS
```

OpenXPS の基本設定で、両方の形式のサポートを示します。

```Manifest
[DriverRender]
XpsFormat = OpenXPS,XPS
```

MSXPS の基本設定で、両方の形式のサポートを示します。

```Manifest
[DriverRender]
XpsFormat = XPS,OpenXPS
```

ドライバー開発者は、V4 印刷ドライバーの優先形式を決定し、この決定は、ドライバーが提供する設計されている機能に基づきます。 たとえば、高品質な画像を JPEG XR サポートを提供する印刷ドライバーを開発する可能性があります。

印刷システムでは、マニフェストの DriverRender 情報に基づいてさまざまな決定を行います。 これらの決定のいくつかの例を次に示します。

-   V4 ドライバーに送信される GDI ベースの印刷ジョブ

    Microsoft XPS ドキュメント コンバーター (MXDC) は、GDI 印刷ジョブの入力を受け取り、XPS スプール ファイルにジョブを変換します。 その操作のスプール ファイルの形式には、マニフェストの DriverRender セクションで示される、XPS 形式は一致します。

-   XPS 印刷 API の形式の変換

    XPS 印刷 API では、ターゲットのドライバーのサポートされている XPS 形式を照会します。 ドライバーは、両方の形式をサポートする場合、XPS 印刷 API は XPS の印刷ジョブをアプリケーションで AS 送信スプーラーに渡します。 変換は実行されません。

    のみ、ターゲットのドライバーは、いずれかまたはその他の形式をサポートする場合、ジョブはスプールする前に、正しい形式に変換されます。

    マニフェストに XpsFormat が指定されていない場合、動作は既定 MSXPS のみ。 OpenXPS 入力を MSXPS に変換されます。 この動作は、ドライバーの最も強力な下位互換性を提供します。

-   スプーラーに直接送信される XPS ファイル

    スプーラーに直接送信される XPS ファイルは、既定では、MSXPS です。 OpenXPS は、スプーラーに直接送信することはサポートされていません。 ただし、.NET 4.5 以降の前に、独自の MSXPS をシリアル化され、スプーラーに直接ジョブを送信します。 XPS 印刷 API (xpsprint.dll) の導入前に、この動作が実装されました。

    これらの .NET アプリケーションの旧バージョンとの互換性を提供するには、印刷フィルター パイプライン マネージャーは、スプール ファイルがあるかどうかを直接とスプーラーを受信したを確認されます。 そうである場合は MSXPS にすると想定します。 印刷フィルター パイプライン マネージャーがあれば、その時点で、ドライバーの XPS 形式がクエリを実行します。 ドライバーは、MSXPS をサポートする場合は、変換は実行されません。 ドライバーは、OpenXPS のみをサポートする場合、印刷フィルター パイプライン マネージャーは、ファイルの変換を実行します。 ジョブの変換をこの時点ではパフォーマンスが高価です。ただし、従来の .NET アプリが新しい v4 OpenXPS ドライバーを印刷できることになります。

**ドライバー マニフェスト:FileSave セクション**します。 V4 印刷ドライバー マニフェストの FileSave セクションの拡張機能を提供する、**ファイルの保存の**PORTPROMPT によって使用されるダイアログ ボックス: ポート。 (PORTPROMPT: ファイルの代わりに使用する必要があります: で Windows 8.1、ため PORTPROMPT: ユーザーを権限を持っている、権限の低いモードでアプリケーションが実行されている場合でもすべてのファイルの場所にアクセスを許可します)。FileSave セクションのエントリは、インデックスを使用して DriverRender セクションのエントリに関連付けられます。

以下に例を示します。

```Manifest
[FileSave]
xps=0
oxps=0

[DriverRender]
XpsFormat=XPS,OpenXPS
```

これにより、ユーザーは、このドライバーでは、印刷ジョブを送信ポートが PORTPROMPT に設定されている場合:、**ファイルの保存の**ダイアログが表示されます XPS と OpenXPS ファイルとしては、ダイアログ ボックスで、オプションを入力し、.xps または .oxps をそれぞれ、ファイルに適用拡張機能。

マニフェストのファイルの保存のセクションの他のオプションの詳細については、次を参照してください。 [V4 ドライバー マニフェスト](v4-driver-manifest.md)します。

## <a name="related-topics"></a>関連トピック

[OpenXPS 印刷用のアプリのサポート](https://docs.microsoft.com/windows/desktop/printdocs/app-support-for-openxps-printing)  

[Open XML Paper Specification](http://www.ecma-international.org/publications/standards/Ecma-388.htm) 

[V4 ドライバー マニフェスト](v4-driver-manifest.md)  
