---
title: Windows 10 UVC カメラ実装ガイド
description: 受信トレイのドライバーを使ってアプリケーションに準拠しているカメラを USB ビデオ クラスの特定の機能を公開する方法について説明します。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: e8cc222509880498f2c4a78bfa9492a563c00b34
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363268"
---
# <a name="windows-10-uvc-camera-implementation-guide"></a>Windows 10 UVC カメラ実装ガイド

Windows 10 がデバイスを USB ビデオ クラス (バージョン 1.0 ~ 1.5) の仕様に準拠するには、受信トレイの USB ビデオ クラス (UVC) ドライバーを提供します。 このドライバーは、色とセンサーの種類のカメラをサポートします。 このドキュメントでは、受信トレイのドライバーを使ってアプリケーションに UVC 準拠しているカメラの特定の機能を公開する方法について説明します。

## <a name="terminology"></a>用語

| Keyword              | 説明                                                                  |
|----------------------|------------------------------------------------------------------------------|
| UVC                  | USB ビデオ クラス                                                              |
| UVC ドライバー           | OS に付属する USBVideo.sys ドライバー                                   |
| IR                   | 赤外線                                                                     |
| カメラの色         | 色のストリーム (カメラの RGB または YUV など) を出力するカメラ      |
| カメラのセンサー        | 色以外のストリーム (IR または深さカメラなど) を出力するカメラ |
| BOS                  | バイナリ デバイス オブジェクト ストア                                                   |
| MS OS 2.0 記述子 | Microsoft のプラットフォーム固有 BOS デバイス機能記述子                 |

## <a name="sensor-cameras"></a>カメラのセンサー

Windows では、カメラの 2 つのカテゴリをサポートします。 1 は色のカメラで、もう 1 つは色以外のセンサー カメラです。 RGB または YUV カメラがカメラの色およびグレースケールのように色以外カメラとして分類された、IR と深さのカメラがカメラのセンサーとして分類されます。 UVC ドライバーでは、両方の種類のカメラをサポートします。 カメラのファームウェア値ベースを UVC ドライバーは、いずれかでカメラを登録またはサポートされている両方のカテゴリを指定することをお勧めします。

KSCATEGORY 色形式のみをサポートしているカメラを登録する必要があります\_ビデオ\_カメラ。 IR をサポートしているカメラまたは KSCATEGORY で型を登録する必要がある深さ専用形式\_センサー\_カメラ。 KSCATEGORY 色および色以外の形式の両方をサポートしているカメラを登録する必要があります\_ビデオ\_カメラと KSCATEGORY\_センサー\_カメラ。 この分類は、アプリケーションを使用するカメラを選択することができます。

UVC カメラは、属性をそのカテゴリの基本設定を指定できます**SensorCameraMode**と**SkipCameraEnumeration**でその BOS [MS OS 2.0 記述子](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)」で詳しく説明次のセクションでします。

属性**SensorCameraMode** 1 または 2 の値を取得します。

KSCATEGORY 下のデバイスを登録する、値 1、\_センサー\_カメラ。 これだけでなく、値の 1 を指定**SkipCameraEnumeration**カメラをアプリケーションがカメラのセンサーのみを探して使用できるようにします。 カメラ センサー カメラ メディアの種類のみを公開するには、この値を使用する必要があります。

値の 2 **SensorCameraMode**、KSCATEGORY でデバイスを登録\_センサー\_カメラ & KSCATEGORY\_ビデオ\_カメラ。 これにより、カメラ、センサーと色のいずれかのカメラを探してアプリケーションで利用できます。 カメラ センサー カメラと両方の色カメラ メディアの種類を公開するには、この値を使用する必要があります。

BOS 記述子を使用して、上記のレジストリ値を指定することをお勧めします。 参照してください、[例複合デバイス](#example-composite-device)プラットフォーム固有の MS OS 2.0 記述子を使用してサンプル BOS 記述子のセクションを示しています。

前述のようにデバイスのファームウェアを更新することはできません、カスタム INF を使用し、カメラの値を指定することでセンサー カメラとして登録する必要がありますを指定することができます**SensorCameraMode**と**SkipCameraEnumeration**次のようにします。

(受信トレイ UVC ドライバーに基づく) カスタム INF ファイルには、次の AddReg エントリを含める必要があります。

**SensorCameraMode**:REG\_DWORD:1 (センサー カメラとして登録) する

**SkipCameraEnumeration**:REG\_DWORD:1 (使用できるように IR アプリケーションに対してのみ)

カスタムの INF セクションの例は次のとおりです。

```INF
[USBVideo.NT.HW]
AddReg=USBVideo.HW.AddReg

[USBVideo.HW.AddReg]
HKR,, SensorCameraMode, 0x00010001,1      ; places the value under device HW
                                          ; Registry key

HKR,, SkipCameraEnumeration, 0x00010001,1 ; This makes the camera available
                                          ; only for application looking for
                                          ; IR cameras
```

場合、 **SensorCameraMode**と**SkipCameraEnumeration**属性は、ファームウェア、または、INF で指定されていない場合、カメラは、色のカメラとして登録されます色カメラの認識にのみ表示されますアプリケーション。

## <a name="ir-stream"></a>IR ストリーム

Windows の受信トレイの USB ビデオ クラス (UVC) ドライバーでは、YUV 形式でシーンを取り込んで、圧縮されていない YUV、または圧縮の MJPEG フレームとして USB 経由でピクセル データを送信するカメラをサポートします。

形式の種類の Guid は、WDK ksmedia.h ヘッダー ファイルで定義されている stream ビデオの形式の記述子で指定する必要があります。

| 種類 | 説明 |
| --- | --- |
| KSDATAFORMAT\_サブタイプ\_L8\_IR |  非圧縮 8 ビット ルミナンス平面。 この型にマップされます[MFVideoFormat\_L8](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)します。 |
| KSDATAFORMAT\_サブタイプ\_L16\_IR | 輝度および平面の 16 ビットの圧縮されていません。 この型にマップされます[MFVideoFormat\_L16](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)します。 |
| KSDATAFORMAT\_サブタイプ\_MJPG\_IR | 圧縮の MJPEG フレームです。 メディア ファンデーションは、これを NV12 圧縮されていないフレームに変換され、ルミナンス平面のみを使用します。 |

この形式の種類の Guid を指定するにはフレーム記述子の guidFormat フィールドで、メディア ファンデーションのキャプチャのパイプラインは、IR ストリームとしてストリームをマークします。 Media Foundation FrameReader API で記述されたアプリケーションは、IR ストリームを使用できるようにします。 IR のストリームのパイプラインによってスケーリングや IR フレームの変換はサポートされません。

IR の種類の形式を公開するストリームでは、RGB または深さ形式の型を公開する必要がありますできません。

```cpp
// Example Format Descriptor for UVC 1.1 frame based format

typedef struct _VIDEO_FORMAT_FRAME
{
    UCHAR bLength;
    UCHAR bDescriptorType;
    UCHAR bDescriptorSubtype;
    UCHAR bFormatIndex;
    UCHAR bNumFrameDescriptors;
    GUID  guidFormat;  // this field should contain the IR subtype GUID
    UCHAR bBitsPerPixel;
    UCHAR bDefaultFrameIndex;
    UCHAR bAspectRatioX;
    UCHAR bAspectRatioY;
    UCHAR bmInterlaceFlags;
    UCHAR bCopyProtect;
    UCHAR bVariableSize;
} VIDEO_FORMAT_FRAME, *PVIDEO_FORMAT_FRAME;
```

> [!NOTE]
> IR ストリームは、正規表現キャプチャ DShow ストリームとして表示されます。

## <a name="depth-stream"></a>深さのストリーム

Windows の受信トレイの USB ビデオ クラス ドライバーでは、深さのストリームを生成するカメラをサポートします。 これらのカメラはシーンの深度の情報 (たとえば、フライトの時刻) をキャプチャし、USB 経由で圧縮されていない YUV フレームとして深度の情報を送信します。 形式の種類の GUID は、WDK ksmedia.h ヘッダー ファイルで定義されている stream ビデオの形式の記述子で指定する必要があります。

| 種類 | 説明 |
| --- | --- |
| KSDATAFORMAT\_サブタイプ\_D16 |  16 ビット深度のマップの値。 この型が同じ[MFVideoFormat\_D16](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)します。 値は、ミリメートル単位。 |

GUID 形式の種類を指定するには、フレームの記述子の guidFormat メンバーでは、メディア ファンデーションのキャプチャのパイプラインは、深さのストリームとして、ストリームをマークします。 FrameReader API で記述されたアプリケーションは、深さのストリームを使用できるようにします。 深さのストリームのパイプラインによってスケーリングや深度のフレームの変換はサポートされません。

深さの種類の形式を公開するストリームでは、RGB または IR 形式の型を公開する必要がありますできません。

```cpp
// Example Format Descriptor for UVC 1.1 frame based format
typedef struct _VIDEO_FORMAT_FRAME
{
    UCHAR bLength;
    UCHAR bDescriptorType;
    UCHAR bDescriptorSubtype;
    UCHAR bFormatIndex;
    UCHAR bNumFrameDescriptors;
    GUID guidFormat; // this field should contain the IR subtype GUID
    UCHAR bBitsPerPixel;
    UCHAR bDefaultFrameIndex;
    UCHAR bAspectRatioX;
    UCHAR bAspectRatioY;
    UCHAR bmInterlaceFlags;
    UCHAR bCopyProtect;
    UCHAR bVariableSize;
} VIDEO_FORMAT_FRAME, *PVIDEO_FORMAT_FRAME;
```

> [!NOTE]
> 深さのストリームは DShow で正規のキャプチャのストリームとして表示されます。

## <a name="grouping-cameras"></a>カメラをグループ化

Windows では、カメラ関連のカメラでアプリケーションの作業を支援するために、コンテナー ID に基づいてグループ化をサポートします。 など、IR カメラと同じ物理デバイス上に存在する色カメラとして公開できます OS に関連するカメラ。 これにより、Windows こんにちはなどのアプリケーションを自分のシナリオの関連のカメラを使用します。

ファームウェアでカメラの BOS 記述子では、カメラの機能間の関係を指定する可能性があります。 UVC ドライバーは、この情報を使用し、これらと関連するカメラの機能を公開になります。 これにより、OS、カメラのスタックを関連するアプリケーションにカメラのグループとして公開します。

カメラのファームウェアを指定する必要があります、 *UVC FSSensorGroupID*、波かっこを使用した文字列形式の GUID であります。 同じであるカメラ*UVC FSSensorGroupID*一緒にグループ化されます。

センサーのグループ名前を指定できますを指定することによって*UVC FSSensorGroupName*ファームウェアでの Unicode 文字列。

説明を指定する BOS 例については以下の例の複合デバイス セクションを参照*UVC FSSensorGroupID*と*UVC FSSensorGroupName*します。

前述のようにデバイスのファームウェアを更新することはできない場合、カスタム INF を使用して、センサーのグループ ID を指定して、カメラがセンサーのグループの一部であることを指定し次のように名前し、ことができます。 (受信トレイ UVC ドライバーに基づく)、カスタムの INF ファイルには、次の AddReg エントリを含める必要があります。

**FSSensorGroupID**:REG_SZ:「{センサーが ID の GUID をグループ化}」

**FSSensorGroupName**:REG_SZ:「、センサー グループ表示名」

カスタムの INF セクションの例のとおりようになります

```INF
[USBVideo.NT.Interfaces]
AddInterface=%KSCATEGORY_CAPTURE%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER_EXT%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO_CAMERA%,GLOBAL,USBVideo.Interface

[USBVideo.Interface]
AddReg=USBVideo.Interface.AddReg

[USBVideo.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%USBVideo.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
HKR,, FSSensorGroupID,0x00000000,%FSSensorGroupID%
HKR,, FSSensorGroupName,0x00000000,%FSSensorGroupName%
```

> [!NOTE]
> センサーのグループは DShow キャプチャ パイプラインではサポートされていません。

## <a name="method-2-or-method-3-still-capture-support"></a>キャプチャのサポートはまだメソッドの 2 または 3 のメソッド

UVC 仕様では、ビデオ ストリーミング インターフェイス サポート メソッドの 1/2/3 かどうかでもイメージのキャプチャを入力するかを指定するためのメカニズムを提供します。 OS のデバイスのメソッド 2/3 静止画像キャプチャ サポート利用、UVC のドライバーを使用するには、デバイスのファームウェアは BOS 記述子で値を指定できます。

方法 2/3 静止イメージのキャプチャを有効にするを指定する値がという名前の DWORD *UVC EnableDependentStillPinCapture*します。 BOS 記述子を使用してその値を指定します。 [例複合デバイス](#example-composite-device)以下は引き続き例の BOS 記述子を使用してイメージのキャプチャの有効化を示しています。

前述のようにデバイスのファームウェアを更新することはできない場合、は、カメラは、メソッドの 2 をサポートします。 または方法 3 キャプチャ メソッドのことを指定するカスタム INF を使用できます。

(カスタム UVC ドライバーまたは受信トレイ UVC ドライバーのいずれかに基づく)、カスタムの INF ファイルには、次の AddReg エントリを含める必要があります。

**EnableDependentStillPinCapture**:REG_DWORD:(有効) 0x1 0x0 (無効)

このエントリが有効 (0x1) に設定されている場合、キャプチャ パイプラインはイメージのキャプチャ (ファームウェアも UVC 仕様で指定したとおりの方法 2/3 のサポートをアドバタイズを想定) まだメソッド 2/3 を活用します。

カスタムの INF セクションの例は次のとおりです。

```INF
[USBVideo.NT.Interfaces]
AddInterface=%KSCATEGORY_CAPTURE%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER_EXT%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO_CAMERA%,GLOBAL,USBVideo.Interface

[USBVideo.Interface]
AddReg=USBVideo.Interface.AddReg

[USBVideo.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%USBVideo.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
HKR,,EnableDependentStillPinCapture,0x00010001,0x00000001
```

## <a name="device-mft-chaining"></a>デバイス MFT チェーン

デバイス MFT は、Windows 上のカメラ機能を拡張するには、Ihv と Oem に推奨されるユーザー モード プラグイン メカニズムです。 Windows 10 バージョン 1703 では、前に、カメラのパイプラインには、DMFT 拡張機能の 1 つだけのプラグインがサポートされています。 Windows 10 バージョン 1703 以降 Windows カメラのパイプラインは、最大 3 つ DMFTs DMFTs のオプションのチェーンをサポートします。 Oem の柔軟性は、これを提供する Ihv の付加価値やカメラのストリームを処理する post の形式でします。 たとえば、デバイスは、IHV DMFT と、OEM DMFT PDMFT を使用できます。 次の図は、DMFTs のチェーンに関連するアーキテクチャを示しています。

![DMFT チェーン](images/dmft-chain.png)

カメラのドライバーから DevProxy へのサンプルのフローをキャプチャし、DMFT チェーンを順に移動します。 チェーン内のすべての DMFT では、サンプルを処理する機会があります。 場合は、サンプルの処理、DMFT しない、機能ように、パススルー DMFT を次に、サンプルを渡すだけです。

KsProperty などのコントロール、呼び出しがストリームを参照してください: チェーンの最後の DMFT が呼び出しをまず取得、呼び出しが処理できるまたはチェーン内の前の DMFT に渡されました。

エラーはからに反映させる DMFT DTM し、アプリケーションにします。 IHV と OEM DMFTs、インスタンス化する、DMFT 失敗のいずれかの DTM の致命的なエラーになります。

DMFTs の要件:

- 入力ピンの数、DMFT が以前 DMFT の出力ピンの数と一致する必要があります、DTM は初期化中に失敗するそれ以外の場合。 ただし、同じ DMFT の入力と出力ピンの数が一致する必要はありません。

- DMFT がインターフェイス - IMFDeviceTransform、IMFShutdown、IMFRealTimeClientEx、IKsControl および IMFMediaEventGenerator; をサポートする必要があります。IMFTransform が MFT0 構成がある場合にサポートする必要があります。 またはチェーン内の次の DMFT IMFTransform サポートが必要です。

- フレーム サーバーの 32 ビットと 64 ビットの両方 DMFTs を登録する必要がありますを使用しないで 64 ビット システム。 USB カメラは、"external"(または付属していない) の USB カメラの任意のシステムに接続されている取得可能性がありますが、USB カメラの製造元は DMFTs の 32 ビットと 64 ビットの両方を指定します。

## <a name="configuring-the-dmft-chain"></a>DMFT チェーンを構成します。

カメラ デバイスは、必要に応じて USBVideo.INF 受信トレイのセクションを使用するカスタムの INF ファイルを使用して DLL で DMFT COM オブジェクトを指定できます。

カスタム。INF ファイルの"インターフェイス AddReg セクションで、次のレジストリ エントリを追加して、DMFT Clsid を指定します。

**CameraDeviceMftCLSIDChain** (REG\_マルチ\_SZ) %dmft0 します。CLSID %、%dmft します。CLSID %、%dmft2 します。CLSID %

サンプル INF 次の設定 (%dmft0 を置き換えますで示すように。CLSID % と %dmft1.clsid%、DMFTs を使用する実際の CLSID 文字列を含む) は、Windows 10 バージョン 1703 で許可されている 2 つの Clsid の最大、および 1 つは DevProxy に最も近いおよび、最後の 1 つは、チェーン内の最後の DMFT します。

プラットフォーム DMFT CLSID は、{3D096DDE-8971-4AD5-98F9-C74F56492630} です。

例をいくつか**CameraDeviceMftCLSIDChain**設定。

- *IHV と OEM DMFT 支払ったりプラットフォーム DMFT*

  - CameraDeviceMftCLSIDChain =""(またはこのレジストリ エントリを指定する必要はありません)

- *IHV/OEM DMFT*

  - CameraDeviceMftCLSIDChain %dmft を = です。CLSID %

- *プラットフォーム DMFT &lt; - &gt; IHV と OEM DMFT*

  - CameraDeviceMftCLSIDChain ="{3D096DDE-8971-4AD5-98F9-C74F56492630}"%dmft します。CLSID %

  - プラットフォーム DMFT とチェーン内には、(GUID {0} D671BE6C-FDB8-424F-81D7-03F5B1CE2CC7}) を持つ DMFT USB カメラの場合、結果のレジストリ キーのスクリーン ショットを次に示します。

![レジストリ エディター DMFT チェーン](images/dmft-registry-editor.png)

- *IHV と OEM DMFT0 &lt; - &gt; IHV と OEM DMFT1*

  - CameraDeviceMftCLSIDChain %dmft0 を = です。CLSID %、%dmft1 します。CLSID の %

> [!NOTE]
> **CameraDeviceMftCLSIDChain** Clsid の最大 2 であることができます。

場合**CameraDeviceMftCLSIDChain**が構成されているレガシ CameraDeviceMftCLSID 設定は DTM によってスキップされます。

場合**CameraDeviceMftCLSIDChain**が構成されていないレガシ CameraDeviceMftCLSID が構成されているし、チェーンのようになります (場合、USB カメラ DMFT プラットフォームでサポートされているし、プラットフォーム DMFT が有効になっている) DevProxy &lt;–&gt;プラットフォーム DMFT &lt;–&gt; OEM/IHV DMFT または (カメラが DMFT のプラットフォームでサポートされていないまたはプラットフォーム DMFT が無効のかどうか) DevProxy &lt; - &gt; OEM/IHV DMFT します。

例 INF ファイルの設定:

```INF
[USBVideo.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%USBVideo.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
HKR,,EnablePlatformDmft,0x00010001,0x00000001
HKR,,DisablePlatformDmftFeatures,0x00010001,0x00000001
HKR,,CameraDeviceMftCLSIDChain, 0x00010000,%Dmft0.CLSID%,%Dmft1.CLSID%
```

## <a name="platform-device-mft"></a>プラットフォームのデバイス MFT

Windows で Windows 10 バージョン 1703 以降、オプトインごとに既知のプラットフォームとして DMFT (PDMFT) UVC カメラ用受信トレイ デバイス MFT を提供します。 この DMFT は Ihv および Oem が提供される Windows post 処理アルゴリズムを利用できます。

| プラットフォーム DMFT でサポートされる機能 | Windows のリリース |
|-------------------------------------|-----------------|
| 顔に基づく地域の関心 (ROI) ROI 対応 USB カメラで 3A の調整を有効にします。 | Windows 10 Version 1703 |

> [!NOTE]
> かどうか、カメラはベースの ROI し、PDMFT は読み込まれません場合でも、デバイスが使用して、PDMFT にオプトイン UVC 1.5 をサポートしません。

UVC カメラでしたオプトイン BOS 記述子を通じて EnablePlatformDmft を指定することによってプラットフォーム DMFT を使用します。

プラットフォーム DMFT を有効にするを指定する値は名前で DWORD *UVC EnablePlatformDmft* BOS 記述子を使用して値を指定します。 [例複合デバイス](#example-composite-device)例 BOS 記述子を含んでいるプラットフォーム DMFT を有効にすると以下のセクションを示しています。

前述のように、デバイスのファームウェアを更新できない場合は、デバイスのプラットフォーム DMFT を有効にするカスタムの INF ファイルを使用できます。

(カスタム UVC ドライバーまたは受信トレイ UVC ドライバーのいずれかに基づく)、カスタムの INF ファイルには、次の AddReg エントリを含める必要があります。

**EnablePlatformDmft**:REG_DWORD:(有効) 0x1 0x0 (無効)

このエントリが有効 (0x1) に設定されている場合、キャプチャ パイプラインは、デバイスのプラットフォーム DMFT 受信トレイを使用します。 このカスタムの INF セクションの例を次に示します。

```INF
[USBVideo.NT.Interfaces]
AddInterface=%KSCATEGORY_CAPTURE%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER_EXT%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO_CAMERA%,GLOBAL,USBVideo.Interface

[USBVideo.Interface]
AddReg=USBVideo.Interface.AddReg

[USBVideo.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%USBVideo.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
HKR,,EnablePlatformDmft,0x00010001,0x00000001
```

Windows 10 バージョン 1703 で PDMFT を使用するデバイスがオプトインし、PDMFT でサポートされているすべての機能が有効である (デバイスの機能に基づく)。 PDMFT 機能の詳細な構成がサポートされていません。

## <a name="bos-and-ms-os-20-descriptor"></a>BOS と MS OS 2.0 記述子

UVC 対応のカメラは、ファームウェアでは、プラットフォーム機能 BOS 記述子で Windows の特定のデバイスの構成値を指定できます。 ドキュメントを参照してください[MS OS 2.0 記述子](https://docs.microsoft.com/previous-versions/dn385747(v=msdn.10))os デバイスの構成を表す有効な BOS 記述子を指定する方法について説明します。 ファームウェアで有効な MS OS 2.0 記述子を指定すると、USB スタックは、デバイス ハードウェア レジストリ キー show 以下に、構成値をコピーします。

```Registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USB\<Device ID>\<Instance ID>\Device Parameters
```

UVC ドライバーでは、デバイス ハードウェアのレジストリ キーから構成値を読み取るし、それに応じて OS でデバイスを構成します。 たとえば、ファームウェアでは、構成値を使用してセンサー カメラとして登録されているデバイスを指定します、UVC ドライバーはそのカテゴリのすぐ下のデバイスを登録します。

UVC をプラットフォーム BOS 記述子を使用してデバイスを構成するには、Windows 10 バージョン 1703 UVC デバイスのベンダーが Windows OS 上の INF ファイルの必要としないデバイスを構成するために有効にしていたメカニズムです。

カスタム INF を通じて UVC デバイスの構成は引き続きサポートされますしを BOS 記述子ベースのメカニズムよりも優先します。 INF を使用してデバイス プロパティを指定するときに「UVC-」プレフィックスを追加する必要はありません。 このプレフィックスは BOS 記述子を使用して指定して、特定のインターフェイス インスタンスごとにあるデバイスのプロパティにのみ必要です。 デバイスが DMFT などのユーザー モードのプラグインが必要な場合は、DMFT をインストールするため、INF を指定する必要があります。 それは、ファームウェアを使用して構成することはできません。

## <a name="currently-supported-configuration-values-through-bos-descriptor"></a>現在サポートされている BOS 記述子経由の構成値

| 構成名 | 種類 | 説明 |
| --- | --- | --- |
| SensorCameraMode                              | REG\_DWORD | 特定のカテゴリの下のカメラを登録します。  |
| UVC FSSensorGroupID<br>UVC FSSensorGroupName  | REG\_SZ    | 同じの UVC FSSensorGroupID でグループ カメラ |
| UVC EnableDependentStillPinCapture            | REG\_DWORD | まだメソッド 2/3 のキャプチャを有効にするには              |
| UVC EnablePlatformDmft                        | REG\_DWORD | プラットフォーム DMFT を有効にするには                         |

UVC ドライバーでは、「UVC-」プレフィックスを持つレジストリ値を見て、デバイスのカテゴリ インターフェイス インスタンスのレジストリ キー、プレフィックスなしの同じ値に設定します。 ドライバーでは、ファームウェアで指定された任意の変数の上に挙げたものだけでなく、

```Registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{e5323777-f976-4f5b-9b55-b94699c46e44}\<Device Symbolic Link>\Device Parameters
```

させる os BOS プラットフォームのデバイスの機能と MS OS 2.0 記述子を使用して、デバイスの記述子が 0x0210 する bcdUSB バージョンを指定する必要がありますまたはそれ以上。

## <a name="example-composite-device"></a>複合デバイスの例

ここでは、BOS 記述子と MS OS 2.0 記述子を 2 つのカメラの機能に複合デバイスの例です。 1 つの関数は UVC 色のカメラと 2 番目の関数は UVC IR カメラ。

サンプルの記述子は次のとおりです。

1. KSCATEGORY 色のカメラ関数を登録する\_ビデオ\_カメラ

1. KSCATEGORY IR カメラ関数を登録する\_センサー\_カメラ

1. 色カメラ関数もイメージのキャプチャを有効にします。

1. グループとして、色と IR カメラの機能を関連付けます

デバイスの列挙時に、USB スタックは、デバイスから BOS 記述子を取得します。 次の BOS 記述子は、プラットフォーム特定のデバイス機能です。

```cpp
#include <usbspec.h>

const BYTE USBVideoBOSDescriptor[0x21] =
{
    /* BOS Descriptor */
    0x05,                       // Descriptor size
    USB_BOS_DESCRIPTOR_TYPE,    // Device descriptor type BOS
    0x21, 0x00,                 // Length 0x21 (33) this and all sub descriptors
    0x01,                       // Number of device capability descriptors

    /* Platform Device Capability Descriptor */
    0x1C,                                   // 28 bytes bLength
    USB_DEVICE_CAPABILITY_DESCRIPTOR_TYPE,  // Platform Descriptor type
    USB_DEVICE_CAPABILITY_PLATFORM,         // bDevCapabilityType PLATFORM
    0,                                      // bReserved
    0xDF, 0x60, 0xDD, 0xD8,                 // PlatformCapabilityUUID
    0x89, 0x45,                             // MS OS2.0 Descriptor
    0xC7, 0x4C,                             // D8DD60DF-4589-4CC7-9CD2-659D9E648A9F
    0x9C, 0xD2, 0x65, 0x9D, 0x9E, 0x64, 0x8A, 0x9F,
                                            // CapabilityData
    0x00, 0x00, 0x00, 0x0A,                 // dwWindowsVersion for Windows 10 and later
    0xC8, 0x02,                             // wLength 0x2C8 (712)
    0x01,                                   // bMS_VendorCode - any value. e.g. 0x01
    0x00                                    // bAltEnumCmd 0
};
```

BOS プラットフォームの機能の記述子を指定します。

1. MS OS 2.0 記述子プラットフォーム機能 GUID

1. 仕入先のコントロールのコード bMS\_VendorCode (ここでは 1 に設定します。 任意の値が、ベンダーが推奨時間がかかることができます)、MS OS 2.0 記述子を取得します。

1. この BOS 記述子は、OS バージョンの Windows 10 の該当する以降です。

USB スタック BOS 記述子を確認するには、後に、ベンダーを発行する MS OS 2.0 記述子を取得するための特定のコントロール要求。

MS OS 2.0 ベンダー固有の記述子を取得するためのコントロール要求の形式:

| bmRequestType | bRequest            | wValue | wIndex | wLength | データ                                   |
|---------------|---------------------|--------|--------|---------|----------------------------------------|
| 1100 0000B    | **bMS\_VendorCode** | 0x00   | 0x07   | 長さ  | MS OS 2.0 記述子の設定の返された blob |

_**bmRequestType**_

- データ転送の方向をホストするデバイス

- 仕入先の種類:

- 受信側のデバイス

_**bRequest**_

**BMS\_VendorCode**記述子セット情報構造体の値が返されます。

_**wValue**_

0x00 に設定します。

_**wIndex**_

MS の 0x7\_OS\_20\_記述子\_インデックス。

_**wLength**_

BOS 記述子に返される、MS OS 2.0 記述子の長さを設定します。 この例では 0x25C (604)。

デバイスは、USBVideoMSOS20DescriptorSet で指定されているように、MS OS 2.0 記述子を返すと想定されます。

USBVideoMSOS20DescriptorSet では、色と IR 関数について説明します。 次の MS OS 2.0 記述子の値を指定します。

1. ヘッダーを設定します。

1. 構成のサブセットのヘッダー

1. 色カメラ関数のサブセットのヘッダー

1. センサーのグループ ID のレジストリ値機能記述子

1. センサーのグループ名のレジストリ値機能記述子

1. まだイメージのキャプチャを有効にするためのレジストリ値機能記述子

1. プラットフォーム DMFT を有効にするためのレジストリ値機能記述子

1. IR カメラ関数のサブセットのヘッダー

1. センサーのグループ ID のレジストリ値機能記述子

1. センサーのグループ名のレジストリ値機能記述子

1. センサー カメラとして、カメラを登録するためのレジストリ値機能記述子

ファームウェアでは、このセクションの冒頭に示した虚数部のデバイスの次の MS OS 2.0 記述子を返す仕入先の要求のハンドラーがあります。

```cpp
UCHAR USBVideoMSOS20DescriptorSet[0x2C8] =
{
    /* Microsoft OS 2.0 Descriptor Set Header */
    0x0A, 0x00,             // wLength of MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00,             // wDescriptorType == MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x00, 0x0A, // dwWindowsVersion – 0x10000000 for Windows 10
    0xC8, 0x02,             // wTotalLength - Total length 0x2C8 (712)

    /* Microsoft OS 2.0 Configuration Subset Header */
    0x08, 0x00,             // wLength of MSOS20_SUBSET_HEADER_CONFIGURATION
    0x01, 0x00,             // wDescriptorType == MSOS20_SUBSET_HEADER_CONFIGURATION
    0x00,                   // bConfigurationValue set to the first configuration
    0x00,                   // bReserved set to 0.
    0xBE, 0x02,             // wTotalLength - Total length 0x2BE (702)

    /****************Color Camera Function******************/

    /* Microsoft OS 2.0 Function Subset Header */
    0x08, 0x00,             // wLength of MSOS20_SUBSET_HEADER_FUNCTION
    0x02, 0x00,             // wDescriptorType == MSOS20_SUBSET_HEADER_FUNCTION
    0x00,                   // bFirstInterface field of the first IAD
    0x00,                   // bReserved set to 0.
    0x6E, 0x01,             // wSubsetLength - Length 0x16E (366)

    /****************Register the Color Camera in a sensor group******************/

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x80, 0x00,             // wLength 0x80 (128) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x01, 0x00,             // wPropertyDataType - REG_SZ
    0x28, 0x00,             // wPropertyNameLength – 0x28 (40) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-FSSensorGroupID"
    'C', 0x00, '-', 0x00,
    'F', 0x00, 'S', 0x00,
    'S', 0x00, 'e', 0x00,
    'n', 0x00, 's', 0x00,
    'o', 0x00, 'r', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 'I', 0x00,
    'D', 0x00, 0x00, 0x00,
    0x4E, 0x00,             // wPropertyDataLength – 0x4E (78) bytes
                            // FSSensorGroupID GUID in string format:
                            // "{20C94C5C-F402-4F1F-B324-0C1CF0257870}"
    '{', 0x00, '2', 0x00,   // This is just an example GUID.
    '0', 0x00, 'C', 0x00,   // You need to generate and use your
    '9', 0x00, '4', 0x00,   // own GUID for the sensor group ID
    'C', 0x00, '5', 0x00,
    'C', 0x00, '-', 0x00,
    'F', 0x00, '4', 0x00,
    '0', 0x00, '2', 0x00,
    '-', 0x00, '4', 0x00,
    'F', 0x00, '1', 0x00,
    'F', 0x00, '-', 0x00,
    'B', 0x00, '3', 0x00,
    '2', 0x00, '4', 0x00,
    '-', 0x00, '0', 0x00,
    'C', 0x00, '1', 0x00,
    'C', 0x00, 'F', 0x00,
    '0', 0x00, '2', 0x00,
    '5', 0x00, '7', 0x00,
    '8', 0x00, '7', 0x00,
    '0', 0x00, '}', 0x00,
    0x00, 0x00,

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x56, 0x00,             // wLength 0x56 (86) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x01, 0x00,             // wPropertyDataType - REG_SZ
    0x2C, 0x00,             // wPropertyNameLength – 0x2C (44) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-FSSensorGroupName"
    'C', 0x00, '-', 0x00,
    'F', 0x00, 'S', 0x00,
    'S', 0x00, 'e', 0x00,
    'n', 0x00, 's', 0x00,
    'o', 0x00, 'r', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 'N', 0x00,
    'a', 0x00, 'm', 0x00,
    'e', 0x00, 0x00, 0x00,
    0x20, 0x00,             // wPropertyDataLength – 0x20 (32) bytes
                            // FSSensorGroupName "YourCameraGroup"
    'Y', 0x00, 'o', 0x00,
    'u', 0x00, 'r', 0x00,
    'C', 0x00, 'a', 0x00,
    'm', 0x00, 'e', 0x00,
    'r', 0x00, 'a', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 0x00, 0x00,

    /****************Enable Still Image Capture for Color Camera************/

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x54, 0x00,             // wLength 0x54 (84) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x04, 0x00,             // wPropertyDataType - REG_DWORD
    0x46, 0x00,             // wPropertyNameLength – 0x46 (70) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-EnableDependentStillPinCapture"
    'C', 0x00, '-', 0x00,
    'E', 0x00, 'n', 0x00,
    'a', 0x00, 'b', 0x00,
    'l', 0x00, 'e', 0x00,
    'D', 0x00, 'e', 0x00,
    'p', 0x00, 'e', 0x00,
    'n', 0x00, 'd', 0x00,
    'e', 0x00, 'n', 0x00,
    't', 0x00, 'S', 0x00,
    't', 0x00, 'i', 0x00,
    'l', 0x00, 'l', 0x00,
    'P', 0x00, 'i', 0x00,
    'n', 0x00, 'C', 0x00,
    'a', 0x00, 'p', 0x00,
    't', 0x00, 'u', 0x00,
    'r', 0x00, 'e', 0x00,
    0x00, 0x00,
    0x04, 0x00,              // wPropertyDataLength – 4 bytes
    0x01, 0x00, 0x00, 0x00,   // Enable still pin capture using Method 2 or Method 3

    /****************Enable Platform DMFT for ROI-capable USB Camera************/

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x3C, 0x00,             // wLength 0x3C (60) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x04, 0x00,             // wPropertyDataType - REG_DWORD
    0x2E, 0x00,             // wPropertyNameLength – 0x2E (46) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-EnablePlatformDmft"
    'C', 0x00, '-', 0x00,
    'E', 0x00, 'n', 0x00,
    'a', 0x00, 'b', 0x00,
    'l', 0x00, 'e', 0x00,
    'P', 0x00, 'l', 0x00,
    'a', 0x00, 't', 0x00,
    'f', 0x00, 'o', 0x00,
    'r', 0x00, 'm', 0x00,
    'D', 0x00, 'm', 0x00,
    'f', 0x00, 't', 0x00,
    0x00, 0x00,
    0x04, 0x00,              // wPropertyDataLength – 4 bytes
    0x01, 0x00, 0x00, 0x00,  // Enable Platform DMFT

    /****************IR Camera Function*********************************************/

    /* Microsoft OS 2.0 Function Subset Header */
    0x08, 0x00,             // wLength of MSOS20_SUBSET_HEADER_FUNCTION
    0x02, 0x00,             // wDescriptorType == MSOS20_SUBSET_HEADER_FUNCTION
    0x01,                   // bFirstInterface set of the second function
    0x00,                   // bReserved set to 0.
    0x48, 0x01,             // wSubsetLength - Length 0x148 (328)

    /********Register the IR Camera to the same sensor group as the Color Camera*****/

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x80, 0x00,             // wLength 0x80 (128) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x01, 0x00,             // wPropertyDataType - REG_SZ
    0x28, 0x00,             // wPropertyNameLength – 0x28 (40) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-FSSensorGroupID"
    'C', 0x00, '-', 0x00,
    'F', 0x00, 'S', 0x00,
    'S', 0x00, 'e', 0x00,
    'n', 0x00, 's', 0x00,
    'o', 0x00, 'r', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 'I', 0x00,
    'D', 0x00, 0x00, 0x00,
    0x4E, 0x00,             // wPropertyDataLength – 78 bytes
                            // FSSensorGroupID GUID in string format:
                            // "{20C94C5C-F402-4F1F-B324-0C1CF0257870}"
    '{', 0x00, '2', 0x00,
    '0', 0x00, 'C', 0x00,
    '9', 0x00, '4', 0x00,
    'C', 0x00, '5', 0x00,
    'C', 0x00, '-', 0x00,
    'F', 0x00, '4', 0x00,
    '0', 0x00, '2', 0x00,
    '-', 0x00, '4', 0x00,
    'F', 0x00, '1', 0x00,
    'F', 0x00, '-', 0x00,
    'B', 0x00, '3', 0x00,
    '2', 0x00, '4', 0x00,
    '-', 0x00, '0', 0x00,
    'C', 0x00, '1', 0x00,
    'C', 0x00, 'F', 0x00,
    '0', 0x00, '2', 0x00,
    '5', 0x00, '7', 0x00,
    '8', 0x00, '7', 0x00,
    '0', 0x00, '}', 0x00,
    0x00, 0x00,

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x56, 0x00,             // wLength 0x56 (86) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x01, 0x00,             // wPropertyDataType - REG_SZ
    0x2C, 0x00,             // wPropertyNameLength – 0x2C (44) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-FSSensorGroupName"
    'C', 0x00, '-', 0x00,
    'F', 0x00, 'S', 0x00,
    'S', 0x00, 'e', 0x00,
    'n', 0x00, 's', 0x00,
    'o', 0x00, 'r', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 'N', 0x00,
    'a', 0x00, 'm', 0x00,
    'e', 0x00, 0x00, 0x00,
    0x20, 0x00,             // wPropertyDataLength – 32 bytes
                            // FSSensorGroupName "YourCameraGroup"
    'Y', 0x00, 'o', 0x00,
    'u', 0x00, 'r', 0x00,
    'C', 0x00, 'a', 0x00,
    'm', 0x00, 'e', 0x00,
    'r', 0x00, 'a', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 0x00, 0x00,

    /****************Make IR camera visible to applications*********************/

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x30, 0x00,             // wLength 0x30 (48) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x04, 0x00,             // wPropertyDataType - REG_DWORD
    0x22, 0x00,             // wPropertyNameLength – 0x22 (34) bytes
    'S', 0x00, 'e', 0x00,
    'n', 0x00, 's', 0x00,
    'o', 0x00, 'r', 0x00,
    'C', 0x00, 'a', 0x00,
    'm', 0x00, 'e', 0x00,
    'r', 0x00, 'a', 0x00,
    'M', 0x00, 'o', 0x00,
    'd', 0x00, 'e', 0x00,
    0x00, 0x00,
    0x04, 0x00,              // wPropertyDataLength – 4 bytes
    0x01, 0x00, 0x00, 0x00, // This exposes the camera to OS as an IR only camera
                            // i.e. KSCATEGORY_SENSOR_CAMERA

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x3A, 0x00,             // wLength 0x3A (58) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x04, 0x00,             // wPropertyDataType - REG_DWORD
    0x2C, 0x00,             // wPropertyNameLength – 0x2C (44) bytes
    'S', 0x00, 'k', 0x00,
    'i', 0x00, 'p', 0x00,
    'C', 0x00, 'a', 0x00,
    'm', 0x00, 'e', 0x00,
    'r', 0x00, 'a', 0x00,
    'E', 0x00, 'n', 0x00,
    'u', 0x00, 'm', 0x00,
    'e', 0x00, 'r', 0x00,
    'a', 0x00, 't', 0x00,
    'i', 0x00, 'o', 0x00,
    'n', 0x00, 0x00, 0x00,
    0x04, 0x00,             // wPropertyDataLength – 4 bytes
    0x01, 0x00, 0x00, 0x00  // This exposes the camera to applications looking for IR only cameras
};  
```
