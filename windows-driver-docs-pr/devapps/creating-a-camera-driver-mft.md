---
title: UWP デバイスアプリ用のカメラドライバー MFT の作成
description: UWP デバイスアプリを使用すると、デバイスの製造元はカメラドライバー MFT (media foundation transform) を使用して、カメラのビデオストリームにカスタム設定や特殊効果を適用できます。
ms.assetid: 079CB01E-D16C-4597-8F08-BD75F1D02427
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 452a5e9f56624f1a14b3be47b50959ecccef8594
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873863"
---
# <a name="creating-a-camera-driver-mft-for-a-uwp-device-app"></a>UWP デバイスアプリ用のカメラドライバー MFT の作成

> [!IMPORTANT]
> このトピックは非推奨とされました。 更新されたガイダンスについては、 [DEVICE MFT 設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/dmft-design)を参照してください。

UWP デバイスアプリを使用すると、デバイスの製造元はカメラドライバー MFT (media foundation transform) を使用して、カメラのビデオストリームにカスタム設定や特殊効果を適用できます。 このトピックでは、ドライバーの MFTs を紹介し、[ドライバーの MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプルを使用して、ドライバーの作成方法を示します。 UWP デバイスアプリ全般の詳細については、 [uwp デバイスアプリの準拠](meet-uwp-device-apps.md)に関するページを参照してください。

## <a name="the-driver-mft"></a>ドライバー MFT

このセクションでは、カメラからのメディアキャプチャストリームに効果を適用するために作成するメディアファンデーション変換 (MFT) について説明します。 これは、カメラを他のユーザーと区別するために、色効果、スキームモード、および顔追跡効果の変換を提供する方法です。 この MFT は driver MFT と呼ばれ、UWP アプリがビデオキャプチャを開始するときに、カメラドライバーからの接続されているビデオストリームに最初に適用されます。 そのアプリが**カメラオプション**UI を呼び出すと、Windows は、ドライバー MFT が実装するインターフェイスに対して、そのカスタム効果を制御するために自動的にアクセスできるようにします。

![カメラドライバーの mft は、windows ストアデバイスアプリがカスタム効果を提供するのに役立ちます。](images/372783-camera-drivermft-overview.png)

UWP デバイスアプリでは、ドライバー MFT は必要ありません。 デバイスの製造元は、ドライバー MFT を使用せずに UWP デバイスアプリを実装することを選択できます。これは、カスタム設定や特殊効果をビデオストリームに適用せずに、ハードウェアのブランド化を含む差別化されたユーザーインターフェイスを提供するためのものです。

### <a name="how-a-driver-mft-is-used"></a>Driver MFT の使用方法

カメラの UWP デバイスアプリは、 [CameraCaptureUI](https://go.microsoft.com/fwlink/p/?LinkId=317985) API から起動する Microsoft Store アプリとは別のプロセスで実行されます。 Microsoft Store デバイスアプリでドライバー MFT を制御するには、さまざまなプロセススペースで特定のイベントシーケンスを実行する必要があります。

1. UWP アプリは写真をキャプチャするため、 [CaptureFileAsync](https://go.microsoft.com/fwlink/p/?LinkId=317986)メソッドを呼び出します。
2. Windows によってドライバー MFT ポインターとカメラのデバイス ID が要求されます。
3. ドライバー MFT ポインターが設定ホストに渡されます。
4. ホストは、カメラに関連付けられている Microsoft Store デバイスアプリのアプリ ID のデバイスプロパティを照会します (デバイスごとのメタデータ)。
5. UWP デバイスアプリが見つからない場合は、既定のフライアウトがキャプチャエンジンと対話します。
6. UWP デバイスアプリが見つかった場合はアクティブ化され、設定ホストはドライバー MFT ポインターをそれに渡します。
7. UWP デバイスアプリは、ポインターを介して公開されるインターフェイスを使用してドライバー MFT を制御します。

![windows ストアデバイスアプリを呼び出すためのプロセス相互作用。](images/372798-cameradrivermft-internals.png)

### <a name="avstream-driver-model-requirement"></a>AvStream ドライバーモデルの要件

カメラのドライバーは AvStream ドライバーモデルを使用する必要があります。 AVStream ドライバーモデルの詳細については、「 [Avstream ミニドライバー Design Guide](https://go.microsoft.com/fwlink/p/?LinkID=228585)」を参照してください。

### <a name="how-the-driver-mft-is-exposed-to-apps"></a>ドライバー MFT がアプリに公開されるしくみ

ドライバー MFT は、Windows に COM インターフェイスとして登録されます。これにより、実装する変換を、カメラなど、特定のデバイスから出てくるメディアストリームに適用できます。

**メモ** ドライバー MFT はデバイス固有であり、汎用の MFT ではないため、この機能を使用して登録することはでき `MFTRegister` ません。 レジストリキーの詳細については、このトピックの後半の「 [DRIVER MFT のインストールと登録](#installing-and-registering-the-driver-mft)」を参照してください。

アプリがビデオキャプチャを開始すると、メディアファンデーションソースリーダーがインスタンス化され、ビデオストリームが提供されます。 このメディアソースは、デバイスのレジストリキーからレジストリ値を読み取ります。 ドライバー MFT の COM クラスの CLSID がレジストリ値で見つかった場合、ソースリーダーはドライバー MFT をインスタンス化してメディアパイプラインに挿入します。

UWP デバイスアプリに加えて、ドライバーの MFT 機能には、関連付けられているデバイスを使用してビデオをキャプチャするときに、次の Api を使用してアクセスできます。

- &lt; &gt; HTML を使用する UWP アプリの HTML5 ビデオタグ。 ドライバー MFT が有効になっている変換は、 &lt; &gt; 次のコード例に示すように、video 要素を使用して再生されているビデオに影響します。

    ```cpp
    var video = document.getElementById('myvideo');
        video.src = URL.createObjectURL(fileItem);
        video.play();
    ```

- Windows ランタイムを使用した UWP アプリの MediaCapture API。 この API の使用方法の詳細については、[メディアキャプチャ](https://go.microsoft.com/fwlink/p/?LinkId=243997)のサンプルを参照してください。

- メディアファンデーションのソースリーダー。メディアデータを処理するアプリを対象としています。 を呼び出すと、ドライバー MFT が最初の (0th) MFT としてアプリケーションに公開され `IMFSourceReaderEx::GetTransformForStream` ます。 返されるカテゴリは `MFT_CATEGORY_VIDEO_EFFECT` です。

    ![メディアキャプチャにおけるソースリーダーのロール。](images/372842-cameracaptureengine.png)

### <a name="multi-pin-cameras"></a>複数ピンカメラ

3ピンまたは他のマルチピンカメラがある場合は、「[マルチピンカメラのドライバー MFTs に関する考慮事項](driver-mfts-on-multi-pin-cameras.md)」を参照してください。

## <a name="driver-mft-implementation"></a>ドライバー MFT の実装

ここでは、ドライバー MFT の実装について説明します。 UWP デバイスアプリと連携するドライバー MFT の完全な例については、ドライバーの[mft](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプルを参照してください。

### <a name="development-tools"></a>開発ツール

Microsoft Visual Studio Professional または Microsoft Visual Studio Ultimate が必要です。

### <a name="driver-mft-characteristics"></a>ドライバー MFT の特性

ドライバー MFT は、ストリームごとにインスタンス化されます。 カメラがサポートするストリームごとに、MFT のインスタンスがインスタンス化され、接続されます。 ドライバー MFT には、1つの入力ストリームと1つの出力ストリームが必要です。 ドライバー MFT は、同期 MFT または非同期の MFT のいずれかです。

### <a name="communication-between-the-camera-and-the-driver-mft"></a>カメラとドライバー MFT 間の通信

メディアソースとドライバー MFT 間の双方向の通信を有効にするために、ソースストリームの属性ストアへのポインターは、ドライバー MFT の入力ストリーム属性ストアにとして設定され `MFT_CONNECTED_STREAM_ATTRIBUTE` ます。 これは、次の例のように、ドライバー MFT でを公開することによって有効にしたハンドシェイクプロセスによって発生し `MFT_ENUM_HARDWARE_URL_Attribute` ます。

```cpp
HRESULT CDriverMft::GetAttributes(IMFAttributes** ppAttributes)
{
    HRESULT hr = S_OK;
    if (NULL == ppAttributes)
    {
       return E_POINTER; 
    };
        if(!m_pGlobalAttributes) {
           MFCreateAttributes(&m_pGlobalAttributes, 1);
           m_pGlobalAttributes-> 
             SetString(MFT_ENUM_HARDWARE_URL_Attribute, L"driverMFT");
        }
        *ppAttributes = m_pGlobalAttributes;
        (*ppAttributes)->AddRef();
        return S_OK;
}
```

この例では、 `MFT_CONNECTED_STREAM_ATTRIBUTE` ドライバー MFT の属性ストアのは、デバイスソースストリームの属性ストアを指すように設定されています。 カメラと MFT 間の通信の設定方法の詳細については、「[ハードウェアハンドシェイクシーケンス](https://go.microsoft.com/fwlink/p/?LinkId=320139)」を参照してください。

### <a name="how-to-access-device-source-information"></a>デバイスソース情報にアクセスする方法

次のコード例は、ドライバー MFT が入力属性ストアからソース変換へのポインターを取得する方法を示しています。 ドライバー MFT は、ソースポインターを使用して、デバイスソース情報を取得できます。

```cpp
if(!m_pSourceTransform && m_pInputAttributes) {

          m_pInputAttributes->
              GetUnknown( MFT_CONNECTED_STREAM_ATTRIBUTE,
              IID_PPV_ARGS(&pSourceAttributes));
          pSourceAttributes-> 
              GetUnknown(
              MF_DEVICESTREAM_EXTENSION_PLUGIN_CONNECTION_POINT,            
              IID_PPV_ARGS(&pUnk)));
          pUnk->QueryInterface(__uuidof(IMFTransform), 
              (void**)&m_pSourceTransform));
      }
      if (m_pSourceTransform) {
         // Put code to get device source information here.         
      }
```

### <a name="how-to-implement-passthrough-mode"></a>パススルーモードを実装する方法

ドライバー MFT をパススルーモードにするには、入力ストリームと出力ストリームに同じメディアの種類を指定します。 `ProcessInput`また、 `ProcessOutput` MFT での呼び出しも行われます。 パススルーモードで処理が行われるかどうかを判断するために、ドライバーの MFT 実装に残されます。

### <a name="header-files-to-include"></a>インクルードするヘッダーファイル

`IInspectable` `IMFTransform` ドライバー MFT で実装する必要があるおよびメソッドのヘッダーファイルを含める必要があります。 インクルードするヘッダーファイルの一覧については、[カメラ用の UWP デバイスアプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)のサンプルの**SampleMFT0**ディレクトリにある**stdafx.h**を参照してください。

```cpp
// required for IInspectable
#include <inspectable.h>
```

### <a name="how-to-implement-iinspectable"></a>IInspectable を実装する方法

カメラの UWP デバイスアプリから使用するためのドライバー MFT は、のメソッドを実装して、 `IInspectable` Microsoft Store デバイスアプリが起動時にドライバー mft へのポインターにアクセスできるようにする必要があります。 Driver MFT では、次のようにのメソッドを実装する必要があり `IInspectable` ます。

- **IInspectable:: GetIids**は、 *iid が*out パラメーターに Null を返し、 *iidcount* out パラメーターに0を返します。

- **IInspectable:: GetRuntimeClassName**は、out パラメーターで null を返す必要があります。

- **IInspectable:: GetRuntiGetTrustLevel**は `TrustLevel::BaseTrust` 、out パラメーターでを返す必要があります。

次のコード例は、 `IInspectable` サンプルのドライバー MFT にメソッドがどのように実装されているかを示しています。 このコードは、サンプルの**SampleMFT0**ディレクトリにある**Mft0**ファイルにあります。

```cpp
// Mft0.cpp
STDMETHODIMP CMft0::GetIids( 
    /* [out] */ __RPC__out ULONG *iidCount,
    /* [size_is][size_is][out] */ __RPC__deref_out_ecount_full_opt(*iidCount) IID **iids)
{
    HRESULT hr = S_OK;
    do {
        CHK_NULL_PTR_BRK(iidCount);
        CHK_NULL_PTR_BRK(iids);
        *iids = NULL;
        *iidCount = 0;
    } while (FALSE);

    return hr;
}

STDMETHODIMP CMft0::GetRuntimeClassName( 
    /* [out] */ __RPC__deref_out_opt HSTRING *className)
{
    HRESULT hr = S_OK;
    do {
        CHK_NULL_PTR_BRK(className);
        *className = NULL;
    } while (FALSE);

    return hr;
}

STDMETHODIMP CMft0::GetTrustLevel( 
    /* [out] */ __RPC__out TrustLevel *trustLevel)
{
    HRESULT hr = S_OK;
    do {
        CHK_NULL_PTR_BRK(trustLevel);
        *trustLevel = TrustLevel::BaseTrust;
    } while (FALSE);

    return hr;
}
```

### <a name="com-implementation"></a>COM 実装

ドライバー MFT が実装する各インターフェイスは `IUnknown` 、カメラの UWP デバイスアプリに正しくマーシャリングされるために、実装してから派生する必要があります。 これを示すドライバー MFT の例を次に示し**ます。**

```cpp
// SampleMft0.idl : IDL source for SampleMft0
//

// This file will be processed by the MIDL tool to
// produce the type library (SampleMft0.tlb) and marshalling code.

import "oaidl.idl";
import "ocidl.idl";
import "Inspectable.idl";
import "mftransform.idl";
[
    object,
    uuid(F5208B72-A37A-457E-A309-AE3060780E21),
    oleautomation,
    nonextensible,
    pointer_default(unique)
]
interface IMft0 : IUnknown{
    [id(1)] HRESULT UpdateDsp([in] UINT32 uiPercentOfScreen);
    [id(2)] HRESULT Enable(void);
    [id(3)] HRESULT Disable(void);
    [id(4)] HRESULT GetDspSetting([out] UINT* puiPercentOfScreen, [out] BOOL* pIsEnabled);
};
[
    uuid(DE05674A-C564-4C0E-9B7C-E1519F7AA767),
    version(1.0),
]
library SampleMft0Lib
{
    importlib("stdole2.tlb");
    [
        uuid(7BB640D9-33A4-4759-B290-F41A31DCF848)      
    ]
    coclass Mft0
    {
        [default] interface IMft0;
        interface IInspectable;
        interface IMFTransform;
    };
};
```

**メモ** ドライバー MFT は、を使用して作成できる通常の COM クラスです `CoCreateInstance` 。 関数は汎用的な `MFTRegister` MFT ではないため、登録には使用しないでください。

### <a name="creating-a-proxy"></a>プロキシの作成

ドライバー MFT はアウトプロセスサーバーです。 UWP デバイスアプリで使用するには、ドライバーの MFT インターフェイスをプロセスの境界を越えて使用できるように、プロキシにマーシャリングサポートを提供する必要があります。 この例については、 [DRIVER MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプルを参照してください。 このサンプルでは、MIDL コンパイラを使用して、スタブレスプロキシを生成します。

### <a name="exposing-the-driver-mft-to-apps"></a>ドライバー MFT をアプリに公開する

ドライバー MFT と対話する UWP デバイスアプリを C# または JavaScript で記述するには、Microsoft Store デバイスアプリの Microsoft Visual Studio プロジェクトに追加のコンポーネントを作成する必要があります。 このコンポーネントは、Microsoft Store デバイスアプリから参照できる Windows ランタイムコンポーネントの driver MFT インターフェイスを公開するラッパーです。

「[カメラ用の uwp デバイスアプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)」サンプルのラッパーサブプロジェクトは、ドライバー MFT を Windows ランタイムに公開して、C# または JavaScript で実装された uwp デバイスアプリから使用できるようにする方法の例を示しています。 [ドライバーの MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプルと連携して動作するように設計されています。 サンプルのインストール、実行、およびテストの手順については、「 [DRIVER MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプル」ページを参照してください。

## <a name="installing-and-registering-the-driver-mft"></a>ドライバー MFT のインストールと登録

このセクションでは、ドライバー MFT をインストールするための手順を示します。

1. ドライバー MFT DLL は、次の場所にあるサブディレクトリにインストールする必要があります。
    - % SystemDrive% \\ プログラムファイル\\
2. カメラのインストーラーは、driver MFT DLL で**regsvr32**を呼び出すか、インストーラーが登録に使用する DLL のドライバーマニフェスト (man) ファイルを指定することによって、driver mft を登録します。
3. `CameraPostProcessingPluginCLSID`カメラのレジストリキーの値を設定します。 INF ファイルでは、 `CameraPostProcessingPluginCLSID` 値を DRIVER mft クラスの CLSID GUID に設定することによって、デバイスのデバイスクラスレジストリキーにドライバー mft の clsid を指定する必要があります。 次に、カメラのレジストリキーを設定する INF ファイルのエントリの例を示します。

```inf
KSCATEGORY_VIDEO_CAMERA:

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{E5323777-F976-4f5b-9B55-B94699C46E44}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{E5323777-F976-4f5b-9B55-B94699C46E44}\#GLOBAL\Device Parameters]
"CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
"FriendlyName"="USB Video Device"
"RTCFlags"=dword:00000010
"CameraPostProcessingPluginCLSID"="{3456A71B-ECD7-11D0-B908-00A0C9223196}" 
```

```inf
KSCATEGORY_CAPTURE:

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{ 65E8773D-8F56-11D0-A3B9-00A0C9223196}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{65E8773D-8F56-11D0-A3B9-00A0C9223196}\#GLOBAL\Device Parameters]
"CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
"FriendlyName"="USB Video Device"
"RTCFlags"=dword:00000010
"CameraPostProcessingPluginCLSID"="{3456A71B-ECD7-11D0-B908-00A0C9223196}"
```

**メモ** `KSCATEGORY_VIDEO_CAMERA`カメラを使用することをお勧めします。   通常は、デバイスの登録方法に応じて、レジストリキーの1つだけが必要になります。


## <a name="associate-your-app-with-the-camera"></a>アプリをカメラに関連付ける

このセクションでは、デバイスメタデータおよび Windows レジストリでカメラを識別するために必要な手順について説明します。 このメタデータを使用すると、UWP デバイスアプリをペアリングしてアプリを識別し、カメラが初めて接続されたときにシームレスにダウンロードできるようになります。

### <a name="updates"></a>更新プログラム

アプリの最初のインストール後、ユーザーが更新されたバージョンのアプリをダウンロードすると、更新プログラムはカメラのキャプチャエクスペリエンスに自動的に統合されます。 ただし、更新プログラムは自動的にはダウンロードされません。 アプリは最初の接続時にのみ[自動的にインストール](auto-install-for-uwp-device-apps.md)されるため、ユーザーは Microsoft Store から追加のアプリの更新プログラムをダウンロードする必要があります。 UWP デバイスアプリのメインページでは、更新プログラムが利用可能であることを通知したり、更新プログラムをダウンロードするためのリンクを提供したりすることができます。

**重要** 更新されたアプリは、Windows Update 経由で配布される更新されたドライバーで動作する必要があります。

### <a name="multiple-cameras"></a>複数のカメラ

複数のカメラモデルで、デバイスメタデータで同じ UWP デバイスアプリを宣言できます。 システムに複数の内部に埋め込まれたカメラがある場合、カメラは同じ UWP デバイスアプリを共有する必要があります。 アプリには、使用中のカメラを判別するためのロジックが含まれており、**さらに多くのオプション**エクスペリエンスで、各カメラに異なる UI を表示できます。 このエクスペリエンスのカスタマイズの詳細については、「[カメラオプションをカスタマイズする方法](how-to-customize-camera-options.md)」を参照してください。

### <a name="internal-cameras"></a>内部カメラ

内部カメラ用の UWP デバイスアプリは、Microsoft Store からの[自動インストール](auto-install-for-uwp-device-apps.md)の対象になりますが、シームレスなユーザーエクスペリエンスを実現するために事前にインストールすることをお勧めします。 内部カメラをサポートし、UWP デバイスアプリをそれらに関連付けるために必要な追加の手順があります。 詳細については、「[内部カメラの場所の特定](identifying-the-location-of-internal-cameras.md)」を参照してください。

### <a name="creating-the-device-metadata-package"></a>デバイスメタデータパッケージの作成

内部カメラと外部カメラの両方で、デバイスメタデータパッケージを作成する必要があります。 カメラの UWP デバイスアプリを Microsoft Store に送信する (または、内部カメラの場合は OPK を使用してプレインストールする) 場合、アプリ自体に加えて、次のものを含むメタデータを提供する必要があります。

- アプリケーションの発行元の名前
- アプリケーションパッケージ名
- アプリケーション要素識別子
- デバイスエクスペリエンス識別子

デバイスメタデータを使用してアプリをデバイスに関連付ける方法の詳細については、「 [UWP デバイスアプリのビルド](the-workflow.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

[UWP デバイス アプリを構築する](the-workflow.md)

[UWP デバイス アプリの自動インストール](auto-install-for-uwp-device-apps.md)

[ハードウェアハンドシェイクシーケンス (ハードウェア MFTs)](https://go.microsoft.com/fwlink/p/?LinkId=320139)

[AVStream ミニドライバー設計ガイド](https://go.microsoft.com/fwlink/p/?LinkID=228585)

[カメラ用 UWP デバイスアプリのサンプル](https://go.microsoft.com/fwlink/p/?LinkID=227865)

[ドライバー MFT のサンプル](https://go.microsoft.com/fwlink/p/?LinkID=251566)





