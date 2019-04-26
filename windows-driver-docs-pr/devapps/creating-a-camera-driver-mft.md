---
title: UWP アプリのデバイスのカメラ driver MFT の作成
description: UWP デバイス アプリでは、デバイス メーカーがカメラ driver MFT (メディア ファンデーション変換) でのカメラのビデオ ストリームのカスタム設定と特殊効果を適用することができます。
ms.assetid: 079CB01E-D16C-4597-8F08-BD75F1D02427
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 842c15524c0e3517c15a666666719fcfb67f8954
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339763"
---
# <a name="creating-a-camera-driver-mft-for-a-uwp-device-app"></a>UWP アプリのデバイスのカメラ driver MFT の作成

> [!IMPORTANT]
> このトピックでは非推奨とされました。 参照してください、[デバイス MFT 設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/dmft-design)のガイダンスを更新します。

UWP デバイス アプリでは、デバイス メーカーがカメラ driver MFT (メディア ファンデーション変換) でのカメラのビデオ ストリームのカスタム設定と特殊効果を適用することができます。 このトピックでは、ドライバーの仕様を紹介しを使用して、 [Driver MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプルを作成する方法について説明します。 一般に UWP デバイス アプリの詳細について、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

## <a name="the-driver-mft"></a>Driver MFT

このセクションでは、Media Foundation 変換 (MFT) カメラからメディア キャプチャのストリームに効果を適用するために作成するについて説明します。 これは、色の効果、スキーム モード、および他のユーザーから本当にカメラを識別する顔の追跡の効果の変換を提供する方法。 Driver MFT と呼ばれるこの MFT は、まず、UWP アプリ ビデオ キャプチャの開始時に、カメラのドライバーからの接続されているビデオ ストリームに適用されます。 そのアプリを呼び出すときに、**カメラ オプション**UI、Windows に自動的にドライバーを提供するインターフェイスへのアクセス、MFT がそのカスタム効果を制御するために実装します。

![カメラの driver mft により、windows ストア デバイス アプリがカスタム効果を提供します。](images/372783-camera-drivermft-overview.png)

Driver MFT は UWP アプリのデバイスは必要ありません。 デバイスの製造元は、ドライバー、差別化されたユーザー インターフェイス含むブランド、ハードウェアのビデオ ストリームへのカスタム設定と特殊効果を適用せずに単純に、MFT せず UWP デバイス アプリの実装を選択できます。

### <a name="how-a-driver-mft-is-used"></a>Driver MFT の使用方法

カメラ用 UWP デバイス アプリを Microsoft Store アプリからそれを呼び出すとは異なるプロセスで実行、 [CameraCaptureUI](https://go.microsoft.com/fwlink/p/?LinkId=317985) API。 Driver MFT を制御するための Microsoft Store デバイス アプリでは、複数の異なるプロセス空間のイベントの特定のシーケンスが発生する必要があります。

1. 呼び出すために、写真をキャプチャする必要がある UWP アプリ、 [CaptureFileAsync](https://go.microsoft.com/fwlink/p/?LinkId=317986)メソッド
2. Windows は、driver MFT のポインターとカメラのデバイス ID を要求します。
3. Driver MFT のポインターは、設定のホストに渡される
4. ホスト (デバイス メタデータ) ごとのカメラに関連付けられている Microsoft Store のデバイスのアプリのアプリ ID のデバイスのプロパティを照会します。
5. 既定のフライアウトが、キャプチャ エンジンと対話 UWP デバイス アプリが検出されない場合
6. UWP デバイスのアプリが見つかった場合アクティブ化されて、設定、ホスト ドライバー MFT ポインターに
7. Driver MFT ポインターを通じて公開されるインターフェイスを使用してを制御する UWP デバイスのアプリ

![windows ストア デバイス アプリを呼び出すためのプロセス対話。](images/372798-cameradrivermft-internals.png)

### <a name="avstream-driver-model-requirement"></a>AvStream ドライバー モデルの要件

カメラのドライバーは AvStream ドライバー モデルを使用する必要があります。 AVStream ドライバー モデルに関する詳細については、次を参照してください。 [AVStream ミニドライバー設計ガイド](https://go.microsoft.com/fwlink/p/?LinkID=228585)します。

### <a name="how-the-driver-mft-is-exposed-to-apps"></a>Driver MFT をアプリに公開する方法

MFT として登録されて Windows COM インターフェイスを実装して変換できるようにドライバーは、カメラなどの特定のデバイスからメディア ストリームに適用できます。

**注**MFT を使用して登録するべきではないドライバー、`MFTRegister`関数がある特定のデバイスと汎用 MFT しないためです。 レジストリ キーについては、次を参照してください。、[のインストールと登録 driver MFT](#installing-and-registering-the-driver-mft)このトピックで後述します。

アプリでは、ビデオのキャプチャを開始するときに、ビデオ ストリームを提供する Media Foundation のソースのリーダーがインスタンス化されます。 このメディア ソースは、デバイスのレジストリ キーからレジストリ値を読み取ります。 Driver MFT の COM クラスの CLSID のレジストリ値が見つかった場合、ソース リーダーは、driver MFT をインスタンス化して、メディア パイプラインに挿入します。

UWP デバイスのアプリだけでなく、driver MFT 機能に関連付けられているデバイスを使用して、次の Api を使用してビデオをキャプチャするときにアクセスできます。

- HTML5&lt;ビデオ&gt;HTML を使用して UWP アプリでのタグ。 MFT が有効になっているドライバーのビデオを使用して再生中に影響する変換、&lt;ビデオ&gt;要素は、次のコード例のように。

    ```cpp
    var video = document.getElementById('myvideo');
        video.src = URL.createObjectURL(fileItem);
        video.play();
    ```

- Windows ランタイムを使用して UWP アプリで Windows.Media.MediaCapture API。 この API の使用方法の詳細については、次を参照してください。、[メディアのキャプチャ](https://go.microsoft.com/fwlink/p/?LinkId=243997)サンプル。

- メディア ファンデーションのメディア データを処理するアプリのソース リーダー。 MFT として公開されるアプリケーションに最初の (0 番目) MFT を呼び出すときに、ドライバー`IMFSourceReaderEx::GetTransformForStream`します。 返されるカテゴリが`MFT_CATEGORY_VIDEO_EFFECT`します。

    ![メディアのキャプチャのソース リーダーのロール。](images/372842-cameracaptureengine.png)

### <a name="multi-pin-cameras"></a>複数ピン カメラ

3-pin またはその他の複数ピン カメラがあればを参照してください。[複数ピン カメラのドライバー仕様に関する考慮事項](driver-mfts-on-multi-pin-cameras.md)します。

## <a name="driver-mft-implementation"></a>Driver MFT の実装

このセクションでは、driver MFT の実装についてを説明します。 Driver MFT UWP デバイスのアプリと連動する、完全な例を参照してください、 [Driver MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプル。

### <a name="development-tools"></a>開発ツール

Microsoft Visual Studio Professional または Microsoft Visual Studio Ultimate が必要です。

### <a name="driver-mft-characteristics"></a>Driver MFT の特性

Driver MFT は、ストリームごとにインスタンス化されます。 各ストリーム、カメラがサポート、MFT のインスタンスがインスタンス化され、それに接続します。 Driver MFT は、1 つの入力ストリームと 1 つの出力ストリームがあると想定されます。 Driver MFT MFT を同期または非同期の MFT 場合があります。

### <a name="communication-between-the-camera-and-the-driver-mft"></a>カメラと driver MFT 間の通信

メディア ソースと driver MFT 間の双方向通信を有効にするソース ストリームの属性ストアへのポインターは driver MFT の入力ストリームの属性ストアの設定として`MFT_CONNECTED_STREAM_ATTRIBUTE`します。 公開することで有効にするとのハンドシェイク プロセスを通してこの`MFT_ENUM_HARDWARE_URL_Attribute`で次の例のように、ドライバー、MFT:

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

この例で、`MFT_CONNECTED_STREAM_ATTRIBUTE`デバイス ソース ストリームの属性ストアをポイントする driver MFT の属性ストアに設定されます。 参照してください[ハードウェア ハンドシェイク シーケンス](https://go.microsoft.com/fwlink/p/?LinkId=320139)カメラと MFT 間の通信の設定方法の詳細についてはします。

### <a name="how-to-access-device-source-information"></a>デバイス ソースの情報にアクセスする方法

次のコード例では、driver MFT を取得する方法、ポインター、送信元の変換を入力属性ストアからを示します。 Driver MFT は、デバイス ソースの情報を取得するのに、元のポインターを使用できます。

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

### <a name="how-to-implement-passthrough-mode"></a>パススルー モードを実装する方法

Driver MFT をパススルー モードには、入力と出力ストリームの同じメディアの種類を指定します。 `ProcessInput` `ProcessOutput` MFT の呼び出しが行われます。 Driver MFT 実装パススルー モードで処理が発生したかどうかを判断するまでそのままです。

### <a name="header-files-to-include"></a>ヘッダー ファイルを含める

ヘッダー ファイルをインクルードする必要があります、`IInspectable`と`IMFTransform`メソッド driver MFT を実装する必要があります。 追加するヘッダー ファイルの一覧は、次を参照してください。 **stdafx.h**で、 **SampleMFT0**のディレクトリ、[カメラ用の UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)サンプル。

```cpp
// required for IInspectable
#include <inspectable.h>
```

### <a name="how-to-implement-iinspectable"></a>IInspectable を実装する方法

Driver MFT のメソッドを実装する必要があります、カメラの UWP デバイス アプリからの使用を目的とした`IInspectable`driver MFT の起動時にへのポインターを Microsoft Store のデバイス アプリがアクセスできるようにします。 メソッドを実装する必要があります、driver MFT`IInspectable`次のようにします。

- **IInspectable::GetIids**で null を返す必要があります、 *iid* out パラメーター、およびでは 0 を返す、 *iidCount* out パラメーター。

- **IInspectable::GetRuntimeClassName**は out パラメーターで null を返します。

- **IInspectable::GetRuntiGetTrustLevel**返す必要があります`TrustLevel::BaseTrust`で out パラメーター。

次のコード例に示す方法、`IInspectable`サンプル driver MFT メソッドを実装します。 このコードが記載されて、 **Mft0.cpp**ファイルに、 **SampleMFT0**サンプルのディレクトリ。

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

### <a name="com-implementation"></a>COM の実装

各インターフェイス MFT を実装するには、ドライバーが実装し、から派生`IUnknown`カメラの UWP デバイス アプリに正しくマーシャ リングするためにします。 例を次に **.idl** driver MFT これを実証するファイル。

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

**注**driver MFT は通常の COM クラスを使用して作成できる`CoCreateInstance`します。 使用しないようにする、`MFTRegister`汎用 MFT ではないために登録する関数。

### <a name="creating-a-proxy"></a>プロキシの作成

Driver MFT は、アウト プロセス サーバーです。 UWP デバイス アプリでこれを使用するには、プロキシでのマーシャ リングのサポートを提供して、driver MFT インターフェイスを使用すると、プロセス境界をまたいでようにする必要があります。 この例を見つけることができます、 [Driver MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプル。 サンプルでは、MIDL コンパイラを使用して、スタブレス プロキシを生成します。

### <a name="exposing-the-driver-mft-to-apps"></a>アプリに driver MFT を公開します。

UWP デバイス アプリを作成するC#driver MFT と対話する JavaScript の場合は、Microsoft Store デバイス アプリの Microsoft Visual Studio プロジェクトで、追加のコンポーネントを作成する必要があります。 このコンポーネントは、Microsoft Store のデバイスのアプリに表示されている Windows ランタイム コンポーネントで driver MFT インターフェイスを公開するラッパーです。

ラッパーのサブプロジェクト、[カメラ用の UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)サンプルで実装された UWP デバイス アプリから使用できるように、ドライバーを Windows ランタイム MFT を公開する方法の例は、C#または JavaScript。 組み合わせて動作するものです、 [Driver MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプル。 参照してください、 [Driver MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)インストール、実行、およびサンプルをテストするためのステップ バイ ステップ ガイドのサンプル ページ。

## <a name="installing-and-registering-the-driver-mft"></a>インストールと driver MFT の登録

このセクションでは、driver MFT をインストールするための手順を示します。

1. Driver MFT DLL は、次の場所にサブディレクトリにインストールする必要があります。
    - %Systemdrive%\\プログラム ファイル\\
2. カメラのインストーラーを呼び出して driver MFT を登録します**regsvr32** driver MFT DLL、またはドライバーに登録のインストーラーを使用して DLL 用のマニフェスト (.man) ファイルを指定しています。
3. 設定、`CameraPostProcessingPluginCLSID`カメラのレジストリ キーの値。 INF ファイルには設定して、デバイスのデバイス クラスのレジストリ キーで Driver MFT の CLSID を指定する必要があります、 `CameraPostProcessingPluginCLSID` driver MFT クラスの CLSID guid 値。 カメラのレジストリ キーを設定する INF ファイルのエントリから例を次に示します。

    ```cpp
    KSCATEGORY_VIDEO_CAMERA:

    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{E5323777-F976-4f5b-9B55-B94699C46E44}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{E5323777-F976-4f5b-9B55-B94699C46E44}\#GLOBAL\Device Parameters]
    "CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
    "FriendlyName"="USB Video Device"
    "RTCFlags"=dword:00000010
    "CameraPostProcessingPluginCLSID"="{3456A71B-ECD7-11D0-B908-00A0C9223196}" 



KSCATEGORY_CAPTURE:

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{ 65E8773D-8F56-11D0-A3B9-00A0C9223196}\##?#USB#VID_045E&PID_075D&MI_00#8&23C3DB65&0&0000#{65E8773D-8F56-11D0-A3B9-00A0C9223196}\#GLOBAL\Device Parameters]
"CLSID"="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
"FriendlyName"="USB Video Device"
"RTCFlags"=dword:00000010
"CameraPostProcessingPluginCLSID"="{3456A71B-ECD7-11D0-B908-00A0C9223196}"
```

**注**`KSCATEGORY_VIDEO_CAMERA`カメラをお勧めします。 通常は、デバイスの登録方法に応じて、レジストリ キーの 1 つだけです。


## <a name="associate-your-app-with-the-camera"></a>カメラ アプリを関連付ける

このセクションでは、Windows レジストリとデバイスのメタデータでカメラを識別するために必要な手順についてを説明します。 このメタデータは、UWP デバイス アプリをペアリングすることができ、ダウンロードすることできますシームレスに初めて、カメラが接続されているように、アプリを識別します。

### <a name="updates"></a>更新プログラム

アプリの最初のインストール後に場合は、ユーザーは、アプリの更新バージョンをダウンロードし、更新プログラムに自動的に統合されますカメラ キャプチャのエクスペリエンス。 ただし、更新プログラムが自動的にダウンロードされません。 ユーザーは、アプリがために、Microsoft Store からの他のアプリの更新プログラムをダウンロードする必要があります[自動的にインストールされている](auto-install-for-uwp-device-apps.md)最初にのみ接続します。 UWP デバイス アプリのメイン ページには、更新プログラムを利用し、更新プログラムをダウンロードするリンクを提供の通知を提供できます。

**重要な**更新されたアプリは、Windows Update を通じて更新されたドライバーを使用する必要があります。

### <a name="multiple-cameras"></a>複数のカメラ

複数のカメラ モデルは、同じデバイスで UWP アプリ、デバイス メタデータを宣言できます。 システムに 1 つ以上の埋め込みを内部的にカメラがある場合、カメラは、同じ UWP デバイス アプリを共有する必要があります。 アプリには、どのカメラが使用中であり、各カメラでさまざまな UI を表示することができますを決定するためのロジックが含まれています。 その**より多くのオプション**が発生します。 そのエクスペリエンスをカスタマイズする方法の詳細については、次を参照してください。[カメラ オプションをカスタマイズする方法について](how-to-customize-camera-options.md)します。

### <a name="internal-cameras"></a>内蔵カメラ

内蔵カメラ用の UWP デバイス アプリは、の対象[自動インストール](auto-install-for-uwp-device-apps.md)から Microsoft Store が、最もシームレスなユーザー エクスペリエンスの事前インストールされていることをお勧めします。 内蔵カメラのサポートし、UWP デバイスのアプリに関連付けるに必要な追加手順があります。 詳細については、次を参照してください。[内蔵カメラの位置を識別する](identifying-the-location-of-internal-cameras.md)します。

### <a name="creating-the-device-metadata-package"></a>デバイス メタデータ パッケージを作成します。

内部および外部の両方のカメラでは、デバイス メタデータ パッケージを作成する必要があります。 ときに Microsoft Store にカメラの UWP デバイス アプリを送信する (またはプレインストール内蔵カメラの場合、OPK を使用して)、アプリ自体に加え、次が含まれるメタデータを提供する必要があります。

- アプリケーションの発行元の名前
- アプリケーション パッケージの名前
- アプリケーションの要素の識別子
- デバイス エクスペリエンスの識別子

デバイスのメタデータを使用してアプリをデバイスに関連付ける方法の詳細については、次を参照してください。[構築 UWP デバイス アプリ](the-workflow.md)します。

## <a name="related-topics"></a>関連トピック

[UWP デバイス アプリをビルドします。](the-workflow.md)

[UWP デバイス アプリの自動インストール](auto-install-for-uwp-device-apps.md)

[ハードウェアのハンドシェイクのシーケンス (ハードウェアの仕様)](https://go.microsoft.com/fwlink/p/?LinkId=320139)

[AVStream ミニドライバー設計ガイド](https://go.microsoft.com/fwlink/p/?LinkID=228585)

[カメラのサンプルについては、UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)

[Driver MFT サンプル](https://go.microsoft.com/fwlink/p/?LinkID=251566)





