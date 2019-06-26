---
title: XPS ラスタライズ サービスの使用
description: XPS ラスタライズ サービスの使用
ms.assetid: a6a3746a-3638-464b-bca0-60003f37af76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da7407f12498ea2e84f31d1c28538eb7f2cdb4d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362725"
---
# <a name="using-the-xps-rasterization-service"></a>XPS ラスタライズ サービスの使用


XPS ラスタライズ サービスは、ビットマップを XPS ドキュメントのページを固定に変換する XPS ラスタライザー オブジェクトを実装します。 このサービスは、一連のビットマップ イメージとして XPS ドキュメントをレンダリングする XPSDrv フィルターの設計を簡略化します。 フィルターは、固定ページで、軸に沿った、四角形領域のビットマップ イメージを作成する XPS ラスタライザー オブジェクトに指示できます。

たとえば、プリンターを XPSDrv フィルターは、一連の水平または垂直のバンドとしてプリンターに送信する固定ページを必要があります。 この場合、フィルターはラスタライズする XPS ラスタライザー オブジェクトを別のビットマップとしてで各バンドに通知します。 また、プリンターに十分なメモリがある場合は、フィルターはページ全体のビットマップ イメージを作成するラスタライザーを調べることができます。

XPS ラスタライズ サービスは、システム ファイル Xpsrasterservice.dll に実装されます。 ただし、XPSDrv フィルターは直接アクセスしませんこの DLL 内のエントリ ポイント。 フィルターによって XPS ラスタライズ サービスのインターフェイスにアクセスする代わりに、 [**印刷パイプラインのプロパティ バッグ**](https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag)印刷フィルター パイプライン マネージャーから、フィルターを受信します。

XPSDrv フィルターによって使用できるように、XPS ラスタライズ サービスで指定する必要があります、[フィルター パイプライン構成ファイル](filter-pipeline-configuration-file.md)印刷フィルター パイプライン内のフィルターをについて説明します。 具体的には、構成ファイルを含める必要があります、 **FilterServiceProvider**を持つ要素を**dll**属性は、次の XML の例で示すように、サービスの DLL 名に設定します。

```xml
  <FilterServiceProvider dll = "XpsRasterService.dll" />
```

**FilterServiceProvider**要素の子である、**フィルター**パイプライン内のフィルターを一覧表示する要素。 パイプラインの初期化中に印刷フィルター パイプライン マネージャーは XPS ラスタライズ サービスを読み込むし、プロパティ バッグからサービスをフィルターにアクセスできるようにします。 XPS ラスタライズ サービスを読み込むフィルター パイプライン構成ファイルの例は、WDK の XpsRasFilter サンプルを参照してください。 このサンプルは、Src にある\\印刷\\の WDK インストール Xpsrasfilter フォルダー。

### <a name="obtaining-an-xps-rasterization-factory"></a>XPS ラスタライズのファクトリを取得します。

XPS ドキュメント、ラスタライズする前に XPSDrv フィルターは、印刷のパイプラインのプロパティ バッグからラスタライズのファクトリ オブジェクトへの参照を取得する必要があります。 その後、フィルターは、表示するために必要な各固定ページのファクトリから新しい XPS ラスタライザー オブジェクトを取得します。

印刷フィルター パイプライン マネージャーがフィルターを呼び出し、XPSDrv フィルターを初期化する[ **IPrintPipelineFilter::InitializeFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nf-filterpipeline-iprintpipelinefilter-initializefilter)メソッドをプロパティ バッグの渡します[IPrintPipelinePropertyBag](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nn-filterpipeline-iprintpipelinepropertybag)インターフェイスは、入力パラメーターとしてメソッドにします。

XPSDrv を XPS ラスタライズ ファクトリ オブジェクトへのポインターを取得するには、呼び出しをフィルター処理、 [ **IPrintPipelinePropertyBag::GetProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nf-filterpipeline-iprintpipelinepropertybag-getproperty)メソッド。 プロパティ名"MS\_IXpsRasterizationFactory"ラスタライズのファクトリ オブジェクトを識別します。 このプロパティの値が取得した**GetProperty**ラスタライズ ファクトリ オブジェクトへの参照は、 **IUnknown**インターフェイス。 このインターフェイスを取得した後、フィルターを呼び出す必要があります、 [iunknown::queryinterface](https://go.microsoft.com/fwlink/p/?linkid=119700)メソッドは、オブジェクトへの参照を取得する[IXpsRasterizationFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory)インターフェイス。 その後、フィルターを呼び出すことができます、 [ **IXpsRasterizationFactory::CreateRasterizer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nf-xpsrassvc-ixpsrasterizationfactory-createrasterizer) XPS ラスタライザー オブジェクトを作成するメソッド。

フィルターが呼び出すことによってオブジェクトを解放する必要があります、ファクトリ オブジェクトを不要になったとき、[リリース](https://go.microsoft.com/fwlink/p/?linkid=98433)オブジェクトのメソッド**IXpsRasterizationFactory**インターフェイス。

次のコード例は、取得する方法を示します、 **IXpsRasterizationFactory**インターフェイスのインスタンスから、 **IPrintPipelinePropertyBag**インターフェイス インスタンス。

```cpp
//
// Retrieve a reference to the XPS rasterization factory
// from the print pipeline property bag.
//
HRESULT CreateRasterizationFactory(
 IPrintPipelinePropertyBag *pPropertyBag,
 IXpsRasterizationFactory **ppXPSRasFactory)
{
    if (ppXPSRasFactory != NULL)
    {
        *ppXPSRasFactory = NULL;
    }

    if (pPropertyBag == NULL || ppXPSRasFactory == NULL)
    {
        return E_POINTER;
    }

    HRESULT hr;
    VARIANT var;
 IXpsRasterizationFactory *pXPSRasFactory;

    //
    // Retrieve the factory object from the property bag.
    //
 VariantInit(&var);
    hr = pPropertyBag->GetProperty(L"MS_IXpsRasterizationFactory",
                                   &var);
    if (SUCCEEDED(hr))
    {
        assert(var.vt == VT_UNKNOWN && var.punkVal != NULL);

        //
        // Get the factory object's IXpsRasterizationFactory interface.
        //
 IUnknown *pUnknown = var.punkVal;

        hr = pUnknown->QueryInterface(__uuidof(IXpsRasterizationFactory),
 reinterpret_cast<void**>(&pXPSRasFactory));
    }

    if (SUCCEEDED(hr))
    {
        //
        // Give the caller our reference to the IXpsRasterizationFactory interface.
        //
        *ppXPSRasFactory = pXPSRasFactory;
    }

 VariantClear(&var);
    return hr;
}
```

### <a name="creating-an-xps-object-model-of-a-fixed-page"></a>固定ページの XPS オブジェクト モデルの作成

XPS ラスタライズ ファクトリを作成した後、XPSDrv フィルターは XPS ラスタライザー オブジェクトを作成するのにファクトリを使用できます。 XPS ラスタライザー オブジェクトが、 [IXpsRasterizer](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nn-xpsrassvc-ixpsrasterizer)インターフェイス。 XPS ドキュメントの特定の固定ページ XPS ラスタライザーの各オブジェクトは専用です。 XPS ラスタライザー オブジェクトを作成するには、ファクトリには、固定ページの XPS オブジェクト モデル (OM) が必要です。 (固定ページ) の XPS OM を持つオブジェクトに含まれている、 **IXpsOMPage**インターフェイス。 XPS ラスタライザー オブジェクトは、固定ページのコンテンツにアクセスするのにこのインターフェイスを使用します。 詳細については、 **IXpsOMPage**インターフェイス、Windows SDK のドキュメントを参照してください。

XPSDrv フィルターでは、XPS ラスタライザー オブジェクトを作成する次の手順に従います。

-   フィルターが使用して、固定ページ オブジェクトを読み取り、 [IFixedPage](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nn-filterpipeline-ifixedpage)入力ストリームからのインターフェイス。

-   フィルターで XPS OM オブジェクトを作成する、 **IXpsOMPage**固定ページの内容を保持するインターフェイス。 XPS ラスタライザーは、固定ページのコンテンツにアクセスするのにこのインターフェイスを使用して後でします。

-   XPS ラスタライザーのオブジェクトを作成するには、フィルターは XPS OM オブジェクトを渡します。 **IXpsOMPage** XPS ラスタライズ ファクトリのインターフェイス**IXpsRasterizationFactory::CreateRasterizer**メソッド。

フィルターが呼び出すことによって、オブジェクトを解放する必要があります XPS ラスタライザーのオブジェクトを不要になったとき、**リリース**オブジェクトのメソッド**IXpsRasterizer**インターフェイス。 XPS ラスタライズ サービスを使用した XPSDrv フィルターの実装例については、WDK の XpsRasFilter ドライバーのサンプルを参照してください。

XPS ラスタライズ サービスを使用するには、キャンバスと固定ページ内でビジュアル ブラシは 64 レベルの上限がネストできます。 キャンバスとビジュアル ブラシの詳細については、ダウンロード、 [XML Paper Specification](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)します。

### <a name="bitmap-resolution-and-pixel-format"></a>解像度とピクセル形式をビットマップします。

固定ページの XPS ラスタライザー オブジェクトには、ページのレンダリング位置解像度を知る必要があります。 XPSDrv フィルターへの呼び出しで入力パラメーターとしてドット/インチ (DPI) で、この解像度を指定する**IXpsRasterizationFactory::CreateRasterizer** XPS ラスタライザー オブジェクトを作成します。 たとえば、ディスプレイ デバイスは、600 DPI の解像度を備え、固定ページには、標準のレター サイズのページがについて説明する場合、は、ページ全体のビットマップ イメージは、次のディメンションには。

幅 = (8.5 インチ) x(600 DPI) 5100 ドットを =

高さ = (11 インチ) x(600 DPI) 6600 ドットを =

固定ページの四角形領域のビットマップ イメージを作成するには XPSDrv フィルターを呼び出し XPS ラスタライザー オブジェクトの呼び出し[ **IXpsRasterizer::RasterizeRect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nf-xpsrassvc-ixpsrasterizer-rasterizerect)メソッド。 このメソッドは、常に 32 ビットのピクセル サイズのビットマップを生成します。 ピクセル形式が GUID 値で指定された**GUID\_WICPixelFormat32bppPBGRA**、ヘッダー ファイル Wincodec.h で定義されています。 形式には、8 ビットの赤、緑、および青のコンポーネントが含まれています。 とは、標準 (sRGB) の色領域。 さらに、形式には、8 ビットのアルファ コンポーネントが含まれています。 アルファ コンポーネントによってピクセルの各値の色要素が事前乗算されます。 この形式の詳細については、次を参照してください。[ピクセルのネイティブ形式の概要](https://docs.microsoft.com/windows/desktop/wic/-wic-codec-native-pixel-formats)します。

XPSDrv フィルターによっては、XPS ラスタライザー オブジェクトによって生成されるビットマップの追加の処理を実行します。 たとえば、カラー プリンター用のフィルターは、ビットマップをプリンターのページ記述言語で、ビットマップをラップし、プリンターに送信する前に CMYK ピクセル形式に変換可能性があります。

XPS ラスタライズ サービスを XPSDrv フィルターとの通信に使用するインターフェイスの詳細については、次を参照してください。 [XPS ラスタライズ サービス参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)します。

### <a name="xpsras-and-high-precision-pixel-formats"></a>XPSRas と高精度のピクセル形式

-   Windows 8、XPS ラスタライズ サービスが、新しいインターフェイスを公開します。 [IXpsRasterizationFactory1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory1)、の新しいバージョンである[IXpsRasterizationFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory)します。 **IXpsRasterizationFactory1** 、新しいメソッドを公開する[ **IXpsRasterizationFactory1::CreateRasterizer1**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))、つまり、Windows 7 バージョンと同じです ([ **IXpsRasterizationFactory::CreateRasterizer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nf-xpsrassvc-ixpsrasterizationfactory-createrasterizer)) 出力ピクセル形式の 1 つの新しいパラメーターを受け取る点を除いて、します。
-   この機能を新しい列挙型を公開する[ **XPSRAS\_ピクセル\_形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/ne-xpsrassvc-__midl___midl_itf_xpsrassvc_0000_0003_0001)、呼び出し元を使用するピクセル形式を選択できるようにする、 [IWICBitmap](https://docs.microsoft.com/windows/desktop/api/wincodec/nn-wincodec-iwicbitmap)IXpsRasterizer::RasterizeRect メソッドによって返されるインターフェイス。

### <a name="xpsras-and-the-gpu"></a>XPSRas と GPU

WDDM 1.2 ディスプレイ ドライバーでは、Windows 8 を実行するコンピューターがある場合とで示すように、すべての条件、 [XPSRas GPU 利用デシジョン ツリー](xpsras-usage-decision-tree.md)が満たされると、GPU ハードウェア アクセラレーションが常に使用します。 これは、開発者は、されませんが、GPU のパフォーマンスの向上を享受するための手順を実行することを意味します。 ただし、さらに、システムのグラフィックス パフォーマンスを最適化する、次の手順を考慮する必要があります。

-   呼び出す、 [ **RasterizeRect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nf-xpsrassvc-ixpsrasterizer-rasterizerect)一貫性のある四角形の大きさを持つメソッド。 それができない場合は、提供する最適な**RasterizeRect**のために必要な最初の呼び出し時に四角形のサイズが大きいものと、後続の呼び出しでより小さな四角形のサイズを求めます。
-   絶対に必要な場合にのみ、アンチ エイリアスを使用します。 エイリアス化テキストとベクトルように見えますが、アンチ エイリアスの対応するを DPI 値を指定した場合、 [ **IXpsRasterizationFactory::CreateRasterizer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nf-xpsrassvc-ixpsrasterizationfactory-createrasterizer)メソッドがかなり高いです。 たとえば、200 DPI 以上の DPI 値が高いと見なされます。 エイリアス化テキストと高 DPI とベクトルを使用する場合、指定されたデバイスの出力の品質が十分であることを確認するテストを行う必要があります。
-   ラスタライズする前に、ドキュメントを操作することができますし、フォントのサブセットおよびいくつかのページで繰り返される要素のリソース ディクショナリを使用して、IXpsOMPage が XPSRas パフォーマンスを向上します。
