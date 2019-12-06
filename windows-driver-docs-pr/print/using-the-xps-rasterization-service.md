---
title: XPS ラスタライズ サービスの使用
description: XPS ラスタライズ サービスの使用
ms.assetid: a6a3746a-3638-464b-bca0-60003f37af76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bc60046c38303f8bdb0a3cd7ad0320b4555bd51
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881883"
---
# <a name="using-the-xps-rasterization-service"></a>XPS ラスタライズ サービスの使用

Xps ラスタライズサービスは、xps ドキュメント内の固定ページをビットマップに変換する XPS ラスタライザーオブジェクトを実装します。 このサービスは、XPS ドキュメントを一連のビットマップイメージとしてレンダリングする XPSDrv フィルターの設計を簡略化します。 フィルターでは、XPS ラスタライザーオブジェクトに対して、固定ページ内の軸に沿った四角形の領域のビットマップイメージを作成するように指示できます。

たとえば、プリンターの XPSDrv フィルターでは、水平方向または垂直方向の一連のバンドとして、固定ページをプリンターに送信することが必要になる場合があります。 この場合、フィルターは XPS ラスタライザーオブジェクトに対して、各バンドを個別のビットマップとしてラスタライズするように指示します。 または、プリンターに十分なメモリがある場合は、ページ全体のビットマップイメージを作成するようにラスタライザーに指示することもできます。

XPS ラスタライズサービスは、システムファイル Xpsrasterservice.dll に実装されています。 ただし、XPSDrv フィルターはこの DLL 内のエントリポイントに直接アクセスしません。 フィルターは、フィルターが印刷フィルターパイプラインマネージャーから受信した[**印刷パイプラインプロパティバッグ**](https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag)を介して XPS ラスタライズサービスのインターフェイスにアクセスします。

XPSDrv フィルターで使用できるようにするには、XPS ラスタライズサービスを[フィルターパイプライン構成ファイル](filter-pipeline-configuration-file.md)で指定する必要があります。このファイルは、印刷フィルターパイプラインのフィルターについて説明しています。 具体的には、次の XML の例に示すように、構成ファイルには、 **dll**属性がサービス dll 名に設定された**filterserviceprovider**要素が含まれている必要があります。

```xml
  <FilterServiceProvider dll = "XpsRasterService.dll" />
```

**Filterserviceprovider**要素は、パイプライン内のフィルターを一覧表示する**filters**要素の子です。 パイプラインの初期化中に、印刷フィルターパイプラインマネージャーは XPS ラスタライズサービスを読み込み、プロパティバッグを使用してサービスにフィルターからアクセスできるようにします。 XPS ラスタライズサービスを読み込むフィルターパイプライン構成ファイルの例については、WDK の Xp のサンプルを参照してください。 このサンプルは、WDK インストールの Src\\Print\\Xp フォルダーにあります。

## <a name="obtaining-an-xps-rasterization-factory"></a>XPS ラスタライズファクトリを取得する

XPS ドキュメントをラスタライズする前に、XPSDrv フィルターは、印刷パイプラインプロパティバッグからラスタライズファクトリオブジェクトへの参照を取得する必要があります。 その後、フィルターは、レンダリングする必要がある固定ページごとに、ファクトリから新しい XPS ラスタライザーオブジェクトを取得します。

XPSDrv フィルターを初期化するには、印刷フィルターパイプラインマネージャーがフィルターの[**iprintpipelinefilter:: initializefilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iprintpipelinefilter-initializefilter)メソッドを呼び出し、プロパティバッグの[Iprintpipelinefilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelinepropertybag)インターフェイスを入力パラメーターとしてメソッドに渡します。

XPS ラスタライズファクトリオブジェクトへのポインターを取得するために、XPSDrv フィルターは[**Iprintpipelinepropertybag:: GetProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iprintpipelinepropertybag-getproperty)メソッドを呼び出します。 プロパティ名 "MS\_IXpsRasterizationFactory" は、ラスタライズファクトリオブジェクトを識別します。 このプロパティの場合、 **GetProperty**から取得された値は、ラスタライズファクトリオブジェクトの**IUnknown**インターフェイスへの参照です。 このインターフェイスを取得した後、フィルターは、オブジェクトの[IXpsRasterizationFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory)インターフェイスへの参照を取得するために、 [IUnknown:: QueryInterface](https://go.microsoft.com/fwlink/p/?linkid=119700)メソッドを呼び出す必要があります。 その後、フィルターは[**IXpsRasterizationFactory:: CreateRasterizer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nf-xpsrassvc-ixpsrasterizationfactory-createrasterizer)メソッドを呼び出して XPS ラスタライザーオブジェクトを作成できます。

ファクトリオブジェクトが不要になった場合は、オブジェクトの**IXpsRasterizationFactory**インターフェイスで[release](https://go.microsoft.com/fwlink/p/?linkid=98433)メソッドを呼び出すことによって、オブジェクトを解放する必要があります。

次のコード例は、 **Iprintpipelinepropertybag**インターフェイスインスタンスから**IXpsRasterizationFactory**インターフェイスインスタンスを取得する方法を示しています。

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

## <a name="creating-an-xps-object-model-of-a-fixed-page"></a>固定ページの XPS オブジェクトモデルの作成

XPS ラスタライズファクトリを作成した後、XPSDrv フィルターはファクトリを使用して XPS ラスタライザーオブジェクトを作成できます。 XPS ラスタライザーオブジェクトには、 [Ixpsrasterizer](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nn-xpsrassvc-ixpsrasterizer)インターフェイスがあります。 各 XPS ラスタライザーオブジェクトは、XPS ドキュメントの特定の固定ページ専用です。 XPS ラスタライザーオブジェクトを作成するには、ファクトリに固定ページの XPS オブジェクトモデル (OM) が必要です。 XPS OM (固定ページ) は、 **IXpsOMPage**インターフェイスを持つオブジェクトに含まれています。 XPS ラスタライザーオブジェクトは、このインターフェイスを使用して、固定ページのコンテンツにアクセスします。 **IXpsOMPage**インターフェイスの詳細については、Windows SDK のドキュメントを参照してください。

XPSDrv フィルターは、次の手順に従って XPS ラスタライザーオブジェクトを作成します。

- フィルターは、入力ストリームから[Ifixedpage](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-ifixedpage)インターフェイスを持つ固定ページオブジェクトを読み取ります。

- フィルターは、固定ページの内容を保持するために、 **IXpsOMPage**インターフェイスを持つ XPS OM オブジェクトを作成します。 XPS ラスタライザーは、後でこのインターフェイスを使用して、固定ページのコンテンツにアクセスします。

- Xps ラスタライザーオブジェクトを作成するために、フィルターは xps OM オブジェクトの**IXpsOMPage**インターフェイスを xps ラスタライズファクトリの**IXpsRasterizationFactory:: CreateRasterizer**メソッドに渡します。

XPS ラスタライザーオブジェクトが不要になった場合は、オブジェクトの**Ixpsrasterizer**インターフェイスで**release**メソッドを呼び出して、オブジェクトを解放する必要があります。 XPS ラスタライズサービスを使用する XPSDrv filter の実装例については、WDK の xps Srasfilter サンプルドライバーを参照してください。

XPS ラスタライズサービスで使用する場合、固定ページ内のキャンバスとビジュアルブラシは、最大64レベルまで入れ子にすることができます。 キャンバスとビジュアルブラシの詳細については、「 [XML Paper Specification](https://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)」をダウンロードしてください。

## <a name="bitmap-resolution-and-pixel-format"></a>ビットマップ解像度とピクセル形式

固定ページの XPS ラスタライザーオブジェクトは、ページが表示される解像度を認識している必要があります。 XPSDrv フィルターは、XPS ラスタライザーオブジェクトを作成する**IXpsRasterizationFactory:: CreateRasterizer**の呼び出しで、この解像度をドット/インチ (dpi) で入力パラメーターとして指定します。 たとえば、ディスプレイデバイスの解像度が 600 DPI で、固定ページに標準の文字サイズページが記述されている場合、ページ全体のビットマップイメージの大きさは次のようになります。

width = (8.5 インチ) x (600 DPI) = 5100 ドット

高さ = (11 インチ) x (600 DPI) = 6600 ドット

固定ページの四角形領域のビットマップイメージを作成するために、XPSDrv フィルターは XPS ラスタライザーオブジェクトの[**Ixpsrasterizer:: RasterizeRect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nf-xpsrassvc-ixpsrasterizer-rasterizerect)メソッドを呼び出します。 このメソッドは、常に32ビットのピクセルサイズのビットマップを生成します。 ピクセル形式は、GUID 値**guid\_WICPixelFormat32bppPBGRA**によって指定されます。この guid は、ヘッダーファイル wincodec .h に定義されています。 この形式には、8ビットの赤、緑、および青のコンポーネントが含まれており、標準の (sRGB) 色空間を使用します。 また、この形式には8ビットのアルファコンポーネントが含まれています。 各ピクセル値のカラーコンポーネントは、アルファコンポーネントによって乗算されます。 この形式の詳細については、「[ネイティブピクセル形式の概要](https://docs.microsoft.com/windows/desktop/wic/-wic-codec-native-pixel-formats)」を参照してください。

一部の XPSDrv フィルターでは、XPS ラスタライザーオブジェクトによって生成されるビットマップの追加処理が実行される場合があります。 たとえば、カラープリンターのフィルターでは、ビットマップをプリンターのページ記述言語にラップしてプリンターに送信する前に、ビットマップを CMYK ピクセル形式に変換することができます。

XPS ラスタライズサービスが XPSDrv フィルターとの通信に使用するインターフェイスの詳細については、「 [Xps ラスタライズサービスリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)」を参照してください。

## <a name="xpsras-and-high-precision-pixel-formats"></a>X 形式と高精度のピクセル形式

- Windows 8 では、XPS ラスタライズサービスは新しいインターフェイス[IXpsRasterizationFactory1](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory1)を公開しています。これは、新しいバージョンの[IXpsRasterizationFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory)です。 **IXpsRasterizationFactory1**は、Windows 7 バージョン ([**IXpsRasterizationFactory:: CreateRasterizer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nf-xpsrassvc-ixpsrasterizationfactory-createrasterizer)) と同一の新しいメソッド[**IXpsRasterizationFactory1:: CreateRasterizer1**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))を公開します。ただし、出力ピクセル形式には1つの新しいパラメーターが使用されます。

- この機能は、 [ **\_ピクセル\_形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/ne-xpsrassvc-__midl___midl_itf_xpsrassvc_0000_0003_0001)である新しい列挙体を公開します。これにより、呼び出し元は、IXpsRasterizer:: RasterizeRect メソッドによって返される[IWICBitmap](https://docs.microsoft.com/windows/desktop/api/wincodec/nn-wincodec-iwicbitmap)インターフェイスによって使用されるピクセル形式を選択できます。

## <a name="xpsras-and-the-gpu"></a>と GPU を

Windows 8 を実行しているコンピューターで WDDM 1.2 ディスプレイドライバーを使用していて、[ [Gpu 使用率] デシジョンツリー](xpsras-usage-decision-tree.md)に表示されているすべての条件が満たされている場合は、常に gpu ハードウェアアクセラレータが使用されます。 つまり、開発者は、GPU によって提供されるパフォーマンスの強化を活用するための手順を実行する必要はありません。 ただし、システムのグラフィックスパフォーマンスをさらに最適化するには、次のことを検討する必要があります。

- 四角形の寸法が一貫して[**RasterizeRect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nf-xpsrassvc-ixpsrasterizer-rasterizerect)メソッドを呼び出します。 これが不可能な場合は、最初の呼び出しで必要とされる最大の四角形のサイズを使用して**RasterizeRect**を提供し、後続の呼び出しで小さな四角形のサイズを指定することをお勧めします。

- 必要な場合にのみアンチエイリアシングを使用します。 [**IXpsRasterizationFactory:: CreateRasterizer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/xpsrassvc/nf-xpsrassvc-ixpsrasterizationfactory-createrasterizer)メソッドに指定された DPI 値が非常に高い場合、エイリアスが付けられたテキストとベクターは、対応するアンチエイリアスと同じように見えます。 たとえば、200 DPI を超える DPI 値は高いと見なされます。 テストは、エイリアス化されたテキストとベクトルを高 DPI で使用する場合に、特定のデバイスの出力品質が十分であることを保証するために行う必要があります。

- IXpsOMPage をラスタライズする前にドキュメントを操作できる場合、複数のページで繰り返される要素に対してフォントのサブセットとリソースディクショナリを使用すると、パフォーマンスが向上します。
