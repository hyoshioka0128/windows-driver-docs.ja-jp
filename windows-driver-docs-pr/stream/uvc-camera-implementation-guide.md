---
title: Windows 10 UVC カメラ実装ガイド
description: 受信トレイドライバーを使用して、USB ビデオクラスに準拠しているカメラの特定の機能をアプリケーションに公開する方法について説明します。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: adf4a34ee7657e20f9d905082b134db7be0e45fd
ms.sourcegitcommit: 3aee55397dda48607258697da14e11c183557603
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702176"
---
# <a name="windows-10-uvc-camera-implementation-guide"></a>Windows 10 UVC カメラ実装ガイド

Windows 10 は、USB ビデオクラス仕様 (バージョン1.0 から 1.5) に準拠しているデバイス用の受信トレイ USB ビデオクラス (UVC) ドライバーを提供します。 このドライバーは、色とセンサーの種類のカメラをサポートしています。 このドキュメントでは、受信トレイドライバーを使用して UVC 準拠カメラの特定の機能をアプリケーションに公開する方法について説明します。

## <a name="terminology"></a>用語

| Keyword              | 説明                                                                  |
|----------------------|------------------------------------------------------------------------------|
| UVC                  | USB ビデオクラス                                                              |
| UVC ドライバー           | OS に付属している USBVideo ドライバー                                   |
| ―                   | 赤外線                                                                     |
| カラーカメラ         | カラーストリームを出力するカメラ (RGB や YUV カメラなど)      |
| センサーカメラ        | 非カラーストリームを出力するカメラ (IR カメラや深度カメラなど) |
| BO                  | バイナリデバイスオブジェクトストア                                                   |
| MS OS 2.0 記述子 | Microsoft プラットフォーム固有の BOS デバイス機能記述子                 |

## <a name="sensor-cameras"></a>センサーカメラ

Windows では、2つのカテゴリのカメラがサポートされています。 1つはカラーカメラで、もう1つはカラーセンサー以外のカメラです。 RGB または YUV カメラは、カラーカメラと、グレースケール、IR、および深度カメラなどの非カラーカメラとして分類され、センサーカメラとして分類されます。 UVC ドライバーでは、両方の種類のカメラがサポートされています。 カメラのファームウェアでは、UVC ドライバーがサポートされているカテゴリのいずれかまたは両方にカメラを登録するかに基づいて値を指定することをお勧めします。

色のみの形式の種類をサポートするカメラは、KSCATEGORY\_VIDEO\_カメラで登録する必要があります。 IR または深度専用の形式の種類をサポートするカメラは、KSCATEGORY\_センサー\_カメラで登録する必要があります。 色と非カラーの両方の形式の種類をサポートするカメラは、KSCATEGORY\_VIDEO\_カメラと KSCATEGORY\_センサー\_カメラで登録する必要があります。 この分類により、アプリケーションは、使用するカメラを選択できます。

UVC カメラは、次のセクションで詳しく説明されている BOS [MS OS 2.0 記述子](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)の**SensorCameraMode**および**SkipCameraEnumeration**属性を使用して、カテゴリの基本設定を指定できます。

属性**SensorCameraMode**は1または2の値を取ります。

値が1の場合、デバイスは KSCATEGORY\_センサー\_カメラに登録されます。 これに加えて、 **SkipCameraEnumeration**には1を指定します。これにより、センサーカメラだけを対象とするアプリケーションでカメラを使用できるようになります。 センサーカメラのメディアの種類のみを公開するカメラでは、この値を使用する必要があります。

**SensorCameraMode**の\_値が2の場合、デバイスは KSCATEGORY センサー\_カメラ & KSCATEGORY\_VIDEO\_カメラに登録されます。 これにより、センサーとカラーカメラを検索するアプリケーションでカメラを使用できるようになります。 センサーカメラとカラーカメラメディアタイプの両方を公開するカメラでは、この値を使用する必要があります。

前述のレジストリ値は、BOS 記述子を使用して指定することをお勧めします。 プラットフォーム固有の MS OS 2.0 記述子を含む BOS 記述子のサンプルについては、後述の「[複合デバイスの例](#example-composite-device)」を参照してください。

前述のようにデバイスのファームウェアを更新できない場合は、カスタムの INF を使用し、次のように**SensorCameraMode**と**SkipCameraEnumeration**の値を指定して、カメラをセンサーカメラとして登録する必要があることを指定できます。

(受信トレイ UVC ドライバーに基づく) カスタム INF ファイルには、次の AddReg エントリが含まれている必要があります。

**SensorCameraMode**:REG\_DWORD:1 (センサーカメラとして登録する場合)

**SkipCameraEnumeration**:REG\_DWORD:1 (IR アプリケーションでのみ使用できるようにする)

カスタム INF セクションの例を次に示します。

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

ファームウェアまたは INF で**SensorCameraMode**属性と**SkipCameraEnumeration**属性が指定されていない場合、カメラはカラーカメラとして登録され、カラーカメラ対応アプリケーションに対してのみ表示されます。

## <a name="ir-stream"></a>IR ストリーム

Windows 受信トレイ USB ビデオクラス (UVC) ドライバーは、YUV 形式でシーンをキャプチャし、非圧縮 YUV または圧縮された MJPEG フレームとしてピクセルデータを USB 経由で送信するカメラをサポートしています。

次の形式の種類の Guid は、WDK ksmedia .h ヘッダーファイルで定義されているストリームビデオ形式記述子で指定する必要があります。

| 種類 | 説明 |
| --- | --- |
| KSDATAFORMAT\_サブ\_タイプL8\_IR |  非圧縮8ビットのルミナンス平面。 この型は、 [mfvideoformat\_L8](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)にマップされます。 |
| KSDATAFORMAT\_SUBTYPE\_L16IR\_ | 16ビットの非圧縮平面。 この型は、 [mfvideoformat\_L16](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)にマップされます。 |
| KSDATAFORMAT\_サブ\_タイプ MJPG\_IR | 圧縮された MJPEG フレーム。 メディアファンデーションは、これを NV12 圧縮されていないフレームに変換し、ルミナンス平面のみを使用します。 |

これらの形式の種類の Guid がフレーム記述子の guidFormat フィールドに指定されている場合、メディアファンデーションキャプチャパイプラインはストリームを IR ストリームとしてマークします。 メディアファンデーション FrameReader API で記述されたアプリケーションは、IR ストリームを使用できます。 Ir ストリームのパイプラインでは、IR フレームのスケーリングや変換はサポートされていません。

IR 形式の型を公開するストリームでは、RGB または深度の形式の種類を公開できません。

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
> IR ストリームは、通常のキャプチャストリームとして出力されます。

## <a name="depth-stream"></a>深度ストリーム

Windows 受信トレイ USB ビデオクラスドライバーは、深度ストリームを生成するカメラをサポートしています。 これらのカメラは、シーンの深度情報 (たとえば、フライト時間) をキャプチャし、その深度マップを非圧縮の YUV フレームとして USB 上に送信します。 次の形式の種類の GUID は、WDK ksmedia .h ヘッダーファイルで定義されているストリームビデオ形式記述子で指定する必要があります。

| 種類 | 説明 |
| --- | --- |
| KSDATAFORMAT\_SUBTYPE\_D16 |  16ビット深度マップの値。 この型は、 [mfvideoformat\_D16](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)と同じです。 値はミリメートル単位です。 |

フレーム記述子の guidFormat メンバーで形式の種類 GUID が指定されている場合、メディアファンデーションキャプチャパイプラインはストリームを深度ストリームとしてマークします。 FrameReader API で記述されたアプリケーションは、深度ストリームを使用できます。 深度ストリームのスケーリングや変換は、パイプラインによってサポートされていません。

深度形式の型を公開するストリームでは、RGB または IR 形式の種類を公開できません。

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
> 深度ストリームは、通常のキャプチャストリームとして出力されます。

## <a name="grouping-cameras"></a>カメラのグループ化

Windows では、コンテナー ID に基づくカメラのグループ化がサポートされているため、アプリケーションは関連カメラで動作します。 たとえば、同じ物理デバイス上にある IR カメラとカラーカメラは、関連するカメラとして OS に公開できます。 これにより、Windows Hello などのアプリケーションがシナリオに関連するカメラを使用できるようになります。

カメラの機能間の関係は、ファームウェアのカメラの BOS 記述子で指定できます。 UVC ドライバーはこの情報を利用し、これらのカメラ機能を関連として公開します。 これにより、OS カメラのスタックが、関連するカメラのグループとしてアプリケーションに公開されるようになります。

カメラのファームウェアでは、 *Uvc-FSSensorGroupID*を指定する必要があります。これは、文字列形式の中かっこで構成される GUID です。 同じ*Uvc-FSSensorGroupID*を持つカメラがグループ化されます。

センサーグループに名前を付けるには、ファームウェアで*Uvc-FSSensorGroupName*(Unicode 文字列) を指定します。

*Uvc-FSSensorGroupID*と*Uvc-Fssensorgroupid*を指定する例については、以下の「複合デバイスの例」を参照してください。

前述のようにデバイスのファームウェアを更新できない場合は、カスタムの INF を使用し、次のようにセンサーグループの ID と名前を指定することによって、カメラがセンサーグループの一部であることを指定できます。 (受信トレイ UVC ドライバーに基づく) カスタム INF ファイルには、次の AddReg エントリが含まれている必要があります。

**Fssensorgroupid**:REG_SZ: "{自分のセンサーグループ ID GUID}"

**Fssensorgroupname**:REG_SZ: "センサーグループのフレンドリ名"

カスタム INF セクションの例を次に示します。

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
> センサーグループは、双方のキャプチャパイプラインではサポートされていません。

## <a name="method-2-or-method-3-still-capture-support"></a>メソッド2またはメソッド3は引き続きキャプチャのサポートを行います

UVC 仕様には、ビデオストリーミングインターフェイスが、イメージキャプチャのメソッド1/2/3 型をサポートするかどうかを指定するメカニズムが用意されています。 UVC ドライバーを使用して、イメージキャプチャのサポートがデバイスのメソッド2/3 を OS で利用できるようにするには、デバイスのファームウェアで BOS 記述子の値を指定します。

メソッド2/3 を有効にするために指定する値は、イメージキャプチャは*Uvc-EnableDependentStillPinCapture*という名前の DWORD です。 BOS 記述子を使用して値を指定します。 次の[複合デバイスの例](#example-composite-device)では、BOS 記述子の例を使用して静止イメージキャプチャを有効にする方法を示しています。

前に説明したようにデバイスのファームウェアを更新できない場合は、カスタム INF を使用して、カメラがメソッド2またはメソッド3のキャプチャ方法をサポートしていることを指定できます。

カスタム INF ファイル (カスタム UVC ドライバーまたは受信トレイ UVC ドライバーに基づく) には、次の AddReg エントリが含まれている必要があります。

**EnableDependentStillPinCapture**:REG_DWORD:0x0 (無効) から 0x1 (有効)

このエントリが有効 (0x1) に設定されている場合、キャプチャパイプラインは引き続きイメージキャプチャのためにメソッド2/3 を利用します (ファームウェアが UVC 仕様で指定されているように、メソッド2/3 のサポートをアドバタイズしていることを前提とします)。

カスタム INF セクションの例を次に示します。

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

## <a name="device-mft-chaining"></a>デバイスの MFT チェーン

デバイス MFT は、Ihv および Oem が Windows 上のカメラ機能を拡張するために推奨されるユーザーモードプラグインメカニズムです。 Windows 10 バージョン1703より前では、カメラパイプラインでサポートされる DMFT 拡張プラグインは1つだけでした。 Windows 10 バージョン1703以降では、Windows カメラパイプラインは、最大3つの DMFTs を持つオプションの一連の DMFTs をサポートしています。 これにより、Oem および Ihv はより柔軟に、処理後のカメラストリームの形式で付加価値を提供できます。 たとえば、デバイスは、IHV DMFT および OEM DMFT と共に PDMFT を使用できます。 次の図は、一連の DMFTs を含むアーキテクチャを示しています。

![DMFT チェーン](images/dmft-chain.png)

カメラドライバーから DevProxy にサンプルフローをキャプチャし、DMFT チェーンを実行します。 チェーン内のすべての DMFT がサンプルを処理する機会があります。 DMFT がサンプルを処理したくない場合は、サンプルを次の DMFT に渡すだけで、パススルーとして機能することができます。

Ksk プロパティのようなコントロールの場合、呼び出しはストリームを開始します。チェーン内の最後の DMFT は最初に呼び出しを取得し、その呼び出しを処理するか、チェーン内の前の DMFT に渡すことができます。

エラーは、DMFT から DTM に、次にアプリケーションに反映されます。 IHV/OEM DMFTs の場合、いずれかの DMFTS がインスタンス化に失敗すると、DTM で致命的なエラーが発生します。

DMFTs の要件:

- DMFT の入力ピンカウントは、前の DMFT の出力ピン数と一致している必要があります。それ以外の場合は、初期化中に DTM が失敗します。 ただし、同じ DMFT の入力ピンと出力ピンの数は一致する必要はありません。

- DMFT はインターフェイスをサポートする必要があります。 IMFDeviceTransform、IMFShutdown、IMFRealTimeClientEx、IKsControl、IMFMediaEventGenerator;MFT0 が構成されているか、チェーン内の次の DMFT で IMFTransform のサポートが必要な場合は、IMFTransform をサポートする必要がある場合があります。

- フレームサーバーを使用しない64ビットシステムでは、32ビットと64ビットの両方の DMFTs が登録されている必要があります。 Usb カメラが任意のシステムに接続される可能性があるため、"外部" (または受信トレイ以外) の USB カメラの場合、USB カメラのベンダは32ビットと64ビットの両方の DMFTs を提供する必要があります。

## <a name="configuring-the-dmft-chain"></a>DMFT チェーンの構成

カメラデバイスでは、必要に応じて、受信トレイ USBVideo .INF のセクションを使用するカスタム INF ファイルを使用して、DLL 内に DMFT COM オブジェクトを指定できます。

カスタム。INF ファイルの "Interface AddReg" セクションで、次のレジストリエントリを追加して、DMFT の Clsid を指定します。

**CameraDeviceMftCLSIDChain**(REG\_マルチ\_SZ)% Dmft0。CLSID%、% Dmft。CLSID%、% Dmft2。CLSID

次のサンプルの INF 設定に示されているように、% Dmft0 を置き換えます。CLSID% と% Dmft1% は、お使いの DMFTs に使用している実際の CLSID 文字列と共に、最大2つの Clsid が Windows 10 バージョン1703で許可されています。最初の clsid は DevProxy に最も近いもので、最後の文字列はチェーン内の最後の DMFTS です。

Platform DMFT CLSID は {3D096DDE8971-4AD5-98f9 c74f56492630} です。

**CameraDeviceMftCLSIDChain**設定の例を次に示します。

- *IHV/OEM DMFT または Platform DMFT がない*

  - CameraDeviceMftCLSIDChain = "" (またはこのレジストリエントリを指定する必要はありません)

- *IHV/OEM DMFT*

  - CameraDeviceMftCLSIDChain =% Dmft。CLSID

- *プラットフォーム dmft &lt; -IHV/OEM dmft&gt;*

  - CameraDeviceMftCLSIDChain = "{3D096DDE8971-4AD5-98f9 c74f56492630}",% Dmft.CLSID

  - 次に示すのは、プラットフォーム DMFT がある USB カメラとチェーン内の DMFT (GUID {D671BE6C-FDB8-424F-81D7-03F5B1CE2CC7}) の結果レジストリキーのスクリーンショットです。

![レジストリエディターの DMFT チェーン](images/dmft-registry-editor.png)

- *IHV/OEM DMFT0 &lt; - &gt; IHV/OEM DMFT1*

  - CameraDeviceMftCLSIDChain =% Dmft0.CLSID%、% Dmft1。CLSID%、

> [!NOTE]
> **CameraDeviceMftCLSIDChain**は、最大2つの clsid を持つことができます。

**CameraDeviceMftCLSIDChain**が構成されている場合、従来の CameraDeviceMftCLSID 設定は dtm によってスキップされます。

**CameraDeviceMftCLSIDChain**が構成されておらず、レガシ CameraDeviceMftCLSID が構成されている場合、チェーンは次のようになります (USB カメラがあり、platform dmft と platform &lt;dmft が有効になっている場合)。&gt;Platform dmft &lt;–&gt; OEM/ihv dmft または (カメラが platform dmft でサポートされていないか、platform dmft が&lt;無効になっている場合) devproxy - &gt; OEM/ihv dmft。

INF ファイルの設定例:

```INF
[USBVideo.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%USBVideo.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
HKR,,EnablePlatformDmft,0x00010001,0x00000001
HKR,,DisablePlatformDmftFeatures,0x00010001,0x00000001
HKR,,CameraDeviceMftCLSIDChain, 0x00010000,%Dmft0.CLSID%,%Dmft1.CLSID%
```

## <a name="platform-device-mft"></a>プラットフォームデバイスの MFT

Windows 10 バージョン1703以降では、Windows には、オプトインでプラットフォーム DMFT (PDMFT) と呼ばれる UVC カメラ用の受信トレイデバイス MFT が用意されています。 この DMFT を使用すると、Ihv および Oem は Windows が提供する後処理アルゴリズムを利用できます。

| Platform DMFT でサポートされる機能 | Windows リリース |
|-------------------------------------|-----------------|
| ROI 対応の USB カメラで3A 調整を行うために、面ベースの領域 (ROI) を有効にします。 | Windows 10 Version 1703 |

> [!NOTE]
> カメラで UVC 1.5 ベースの ROI がサポートされていない場合、PDMFT を使用するデバイスが選択されていても、PDMFT は読み込まれません。

UVC カメラでは、EnablePlatformDmft から BOS 記述子を指定することによって、platform DMFT を使用することがオプトインされている場合があります。

Platform DMFT を有効にするために指定する値は、名前が*Uvc-EnablePlatformDmft*である DWORD で、BOS 記述子を使用してその値を指定します。 次の「[複合デバイスの例](#example-composite-device)」セクションでは、BOS 記述子の例を使用したプラットフォーム dmft の有効化について説明します。

前述のようにデバイスのファームウェアを更新できない場合は、カスタムの INF ファイルを使用して、デバイスのプラットフォーム DMFT を有効にすることができます。

カスタム INF ファイル (カスタム UVC ドライバーまたは受信トレイ UVC ドライバーに基づく) には、次の AddReg エントリが含まれている必要があります。

**Enableplatformdmft**:REG_DWORD:0x0 (無効) から 0x1 (有効)

このエントリが有効 (0x1) に設定されている場合、キャプチャパイプラインはデバイスに受信トレイプラットフォーム DMFT を使用します。 このカスタム INF セクションの例を次に示します。

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

Windows 10 バージョン1703では、デバイスが PDMFT を使用することを選択すると、PDMFT でサポートされているすべての機能が有効になります (デバイスの機能に基づいています)。 PDMFT 機能の詳細な構成はサポートされていません。

## <a name="face-auth-profile-via-ms-os-descriptors"></a>MS OS 記述子を使用した顔認証プロファイル

Windows 10 RS5 では、Windows Hello サポートを使用するすべてのカメラに対して Face Auth Profile V2 要件が適用されるようになりました。 カスタムカメラドライバースタックがある MIPI ベースのシステムでは、このサポートは、INF (または拡張機能 INF) を使用するか、ユーザーモードのプラグイン (デバイス MFT) を使用して公開できます。

ただし、USB ビデオデバイスの場合、UVC ベースのカメラを使用した制約として、Windows 10 19H1 ではカスタムカメラドライバーを使用できません。 すべての UVC ベースのカメラは、受信トレイの USB ビデオクラスドライバーを使用する必要があります。また、ベンダの拡張機能は、デバイスの MFT 形式で実装する必要があります。

多くの OEM/Odm の場合、カメラモジュールには、Microsoft OS 記述子を通じて、モジュールのファームウェア内に多くの機能を実装することをお勧めします。

次のカメラは、MSOS 記述子 (BOS 記述子とも呼ばれます) を使用した publish Face Auth プロファイルでサポートされています。

- 別の IR カメラでセンサーグループで使用される、RGB のみのカメラ。
- 別の RGB カメラのセンサーグループで使用される IR のみのカメラ。
- 個別の IR ピンと RGB ピンを持つ RGB + IR カメラ。

> **注:** カメラのファームウェアが上記の3つの要件のいずれかを満たしていない場合、ODM/OEM は、カメラプロファイル V2 を宣言するために拡張機能 INF を使用する必要があります。

### <a name="example-microsoft-os-descriptor-layout"></a>Microsoft OS 記述子のレイアウトの例

次の仕様について、以下に例を示します。

- Microsoft OS 拡張記述子仕様1.0
- Microsoft OS 2.0 記述子の仕様

### <a name="microsoft-os-extended-descriptor-10-specification"></a>Microsoft OS 拡張記述子1.0 仕様

拡張プロパティの OS 記述子には2つのコンポーネントがあります

- 固定長ヘッダーセクション
- ヘッダーセクションの後に続く1つ以上の可変長カスタムプロパティセクション

#### <a name="microsoft-os-10-descriptor-header-section"></a>Microsoft OS 1.0 記述子ヘッダーセクション

ヘッダーセクションでは、1つのカスタムプロパティ (Face Auth Profile) について説明します。

| Offset | フィールド      | サイズ (バイト) | [値]  | 説明                     |
| ------ | ---------- | ------------ | ------ | ------------------------------- |
| 0      | dwLength   | 4            | \<\>   |                                 |
| 4      | bcdVersion | 2            | 0x0100 | バージョン 1.0                     |
| 6      | wIndex     | 2            | 0x0005 | 拡張プロパティの OS 記述子 |
| 8      | wCount     | 2            | 0x0001 | 1つのカスタムプロパティ             |

#### <a name="microsoft-os-10-descriptor-custom-property-section"></a>Microsoft OS 1.0 記述子カスタムプロパティセクション

| Offset | フィールド                | サイズ (バイト) | [値]                 | 説明                                |
| ------ | -------------------- | ------------ | --------------------- | ------------------------------------------ |
| 0      | dwSize               | 4            | 0x00000036 (54)       | このプロパティの合計サイズ (バイト単位)。   |
| 4      | dwPropertyDataType   | 4            | 0x00000004            | REG\_DWORD\_リトル\_エンディアン                 |
| 8      | wPropertyNameLength  | 2            | 0x00000024 (36)       | プロパティ名のサイズ (バイト単位)。      |
| 10     | bPropertyName        | 36           | UVC-CPV2FaceAuth      | Unicode の "UVC-CPV2FaceAuth" 文字列。      |
| 46     | dwPropertyDataLength | 4            | 0x00000004            | プロパティデータ (sizeof (DWORD)) の場合は4バイト。 |
| 50     | bPropertyData        | 4            | 以下のデータスキーマをご覧ください。 | 以下のデータスキーマを参照してください。                     |

##### <a name="payload-schema"></a>ペイロードスキーマ

UVC CPV2FaceAuth データペイロードは、32ビットの符号なし整数です。 上位16ビットは、RGB pin によって公開されるメディアの種類の一覧の0から始まるインデックスを表します。 下位16ビットは、IR pin によって公開されるメディアの種類の一覧の0から始まるインデックスを表します。

たとえば、次のメディアの種類を、RGB pin から宣言された順序で公開するタイプ3のカメラです。

- YUY2640x480@30fps
- MJPG、1280x720@30fps
- MJPG、800x600@30fps
- MJPG、1920x1080@30fps

IR のメディアの種類は次のとおりです。

- L8480x480@30fps
- L8480x480@15fps
- L8480x480@10fps

ペイロード値が0x00010000 の場合、次のような顔認証プロファイルが発行されます。

Pin0: (RES = = 1280, 720;FRT = = 30, 1;SUT = = MJPG)//2 番目のメディアの種類 (0x0001)  
Pin1: (RES = = 480480;FRT = = 30, 1;SUT = = L8)//最初のメディアの種類 (0x0000)

> **注意**:このドキュメントの執筆時点では、Windows Hello では、RGB 480x480@7.5fpsストリームと340x340@15fps IR ストリームについて最小要件があります。 顔認証プロファイルを有効にするときに、この要件を満たすメディアの種類を選択するには、IHV/Oem が必要です。

##### <a name="type-1-camera-sample"></a>Type 1 カメラのサンプル

Type 1 カメラの場合は、IR pin がないため (センサーグループ内のコンピューターの type 2 カメラとペアリングされることを見込んで)、RGB メディアタイプのインデックスのみが発行されます。 赤外線メディアの種類のインデックスでは、ペイロードの下位16ビット値を0xFFFF に設定する必要があります。

たとえば、タイプ1のカメラで次のメディアの種類の一覧が公開されているとします。

- YUY2640x480@30fps
- MJPG、1280x720@30fps
- MJPG、800x600@30fps
- MJPG、1920x1080@30fps

Mjpg、 1280x720@30fpsメディアの種類を使用して CPV2FaceAuth を発行するには、ペイロードを0x0001ffff に設定する必要があります。

##### <a name="type-2-camera-sample"></a>Type 2 カメラのサンプル

Type 2 カメラの場合、上位16ビットを0xFFFF に設定する必要があります。この場合、使用する IR メディアの種類を示す下位16ビットを使用します。

たとえば、次の種類のメディアを含む Type 2 カメラの場合は、次のようになります。

- L8480x480@30fps
- L8480x480@15fps
- L8480x480@10fps

最初のメディアの種類が顔認証に使用される場合、値は次のようにする必要があります。0xFFFF0000。

### <a name="microsoft-os-extended-descriptor-20-specification"></a>Microsoft OS 拡張記述子2.0 仕様

MSOS Profile サポートを追加するレジストリ値を定義するには、MSOS 拡張記述子2.0 を使用します。 これを行うには、 [MICROSOFT OS 2.0 のレジストリプロパティ記述子](#microsoft-os-20-registry-property-descriptor)を使用します。

UVC-CPV2FaceAuth レジストリエントリの場合、次の例では、MSOS 2.0 記述子セットが使用されています。

```cpp
UCHAR Example2_MSOS20DescriptorSet_UVCFaceAuthForFutureWindows[0x3C] =
{
    //
    // Microsoft OS 2.0 Descriptor Set Header
    //
    0x0A, 0x00,               // wLength - 10 bytes
    0x00, 0x00,               // MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x0?, 0x06,   // dwWindowsVersion – 0x060?0000 for future Windows version
    0x3C, 0x00,               // wTotalLength – 60 bytes

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x32, 0x00,               // wLength - 50 bytes
    0x04, 0x00,               // wDescriptorType – 4 for Registry Property
    0x04, 0x00,               // wPropertyDataType - 4 for REG_DWORD_LITTLE_ENDIAN
    0x30, 0x00,               // wPropertyNameLength – 36 bytes
    0x55, 0x00, 0x56, 0x00,   // Property Name - "UVC-CPV2FaceAuth"
    0x43, 0x00, 0x2D, 0x00,
    0x43, 0x00, 0x50, 0x00,
    0x56, 0x00, 0x32, 0x00,
    0x46, 0x00, 0x61, 0x00,
    0x63, 0x00, 0x65, 0x00,
    0x41, 0x00, 0x75, 0x00,
    0x74, 0x00, 0x68, 0x00,
    0x00, 0x00, 0x00, 0x00,
    0x04, 0x00,               // wPropertyDataLength – 4 bytes
    0x00, 0x00, 0x01, 0x00    // PropertyData – 0x00010000 (see Payload Schema)
}
```

UVC-CPV2FaceAuth レジストリエントリを追加すると、デバイスは、このドキュメント https://docs.microsoft.com/en-us/windows-hardware/drivers/stream/dshow-bridge-implementation-guidance-for-usb-video-class-devices で説明されているように、enabledshowredirection レジストリエントリを発行する必要はありません。

ただし、デバイスベンダーが古いバージョンの Windows をサポートする必要がある場合や、フレームサーバー内で MJPEG の圧縮解除を有効にする必要がある場合は、EnableDshowRedirection レジストリエントリを追加する必要があります。

### <a name="sensor-group-generation"></a>センサーグループの生成

Oem は、Type 1 と Type 2 のカメラを使用して Windows Hello サポート用の RGB ストリームと IR ストリームの両方を提供する場合、2つのカメラを合成センサーグループの一部として宣言する必要があります。

これを行うには、拡張機能 INF の FSSensorGroupId タグと Fssensorgroupid タグを、各カメラの [デバイスインターフェイス] プロパティで作成するように宣言します。

ただし、拡張機能の INF が指定されていない場合、Odm は同じ MSOS 記述子を使用して FSSensorGroupId 値と Fssensorgroupid 値を公開することがあります。 受信トレイ Windows 10 USB ビデオクラスドライバーは、ペイロード名にプレフィックス "UVC-" が付いている MSOS 記述子を自動的に受け取り、タグをデバイスインターフェイスプロパティストア ("UVC" プレフィックスを削除) に移行します。

そのため、次のものを発行する Type 1 と Type 2 のカメラを使用すると、OS はカメラを複数のデバイスのセンサーグループに合成して、Windows Hello で使用できます。

> UVC-FSSensorGroupId  
> UVC-FSSensorGroupName

各タグのペイロードは、Unicode 文字列である必要があります。 UVC-FSSensorGroupId ペイロードは、次の形式の GUID 文字列である必要があります。

> {XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX} ({XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX})

GUID の値は、Type 1 と Type 2 カメラの間で同じである必要があり、両方のカメラを同じ物理シャーシに追加する必要があります。 組み込みカメラの場合、物理シャーシはコンピューター自体です。 外部カメラの場合は、Type 1 と Type 2 の両方のカメラモジュールを、コンピューターに接続されているのと同じ物理デバイスに組み込む必要があります。 

## <a name="custom-device-interface-categories-for-sensor-groups"></a>センサーグループのカスタムデバイスインターフェイスカテゴリ

19H1 以降では、Windows は IHV/OEM が指定した拡張メカニズムを提供して、合成されたセンサーグループをカスタムまたは事前定義されたカテゴリに発行できるようにします。 センサーグループの世代は、カスタム INF でセンサーグループ ID キーを提供する IHV/Oem によって定義されます。

> FSSensorGroupId: {カスタム GUID}  
> FSSensorGroupName:\<センサーグループに使用されるフレンドリ名\>

INF の上記の2つの AddReg エントリに加えて、カスタムカテゴリに対して新しい AddReg エントリが定義されています。

> Fssensorgroupカテゴリの一覧: {GUID};{GUID};...;GUID

複数のカテゴリは、セミコロン (;) を使用して定義します。区切られた GUID の一覧。

一致する FSSensorGroupId を宣言する各デバイスは、同じ Fssensorgroupカテゴリリストを宣言する必要があります。 一覧が一致しない場合は、すべてのリストが無視され、カスタムカテゴリが定義されて\_い\_ない場合と同じように、既定では、センサーグループが KSCATEGORY センサーグループに発行されます。

## <a name="camera-rotation"></a>カメラの回転

コンピューティングデバイスがさまざまな形式で導入されているため、物理的な制約の一部ではカメラセンサーが従来の向きではなくマウントされます。 このため、生成されたビデオを適切にレンダリングまたは記録できるように、OS とアプリケーションを正しく記述し、センサーがどのようにマウントされるかを適切に説明する必要があります。

### <a name="architectural-overview"></a>アーキテクチャの概要

Redstone から、カメラが*Windows シャーシの要件*に従ってマウントされているかどうかに関係なく、カメラの向きを明示的に指定するためにすべてのカメラドライバーが必要になります。 具体的には、カメラドライバーは、キャプチャデバイスインターフェイスに 関連付けられて\_いる ACPI pld 構造体に新しく導入されたフィールドであるローテーションを設定する必要があります。

```cpp
typedef struct _ACPI_PLD_V2_BUFFER {

    UINT32 Revision:7;
    UINT32 IgnoreColor:1;
    UINT32 Color:24;
    // …
    UINT32 Panel:3;         // Already supported by camera.
    // …
    UINT32 CardCageNumber:8;
    UINT32 Reference:1;
    UINT32 Rotation:4;      // New field, enum values:
                            // 0 – Rotate by 0° clockwise
                            // 1 – Rotate by 45° clockwise (N/A to camera)
                            // 2 – Rotate by 90° clockwise
                            // 3 – Rotate by 135° clockwise (N/A to camera)
                            // 4 – Rotate by 180° clockwise
                            // 5 – Rotate by 225° clockwise (N/A to camera)
                            // 6 – Rotate by 270° clockwise
    UINT32 Order:5;
    UINT32 Reserved:4;

    //
    // _PLD v2 definition fields.
    //

    USHORT VerticalOffset;
    USHORT HorizontalOffset;
} ACPI_PLD_V2_BUFFER, *PACPI_PLD_V2_BUFFER;
```

回転フィールドの定義は、次のように定義されます。

カメラの場合、ACPI \_pld 構造の回転フィールドは、角度 (0 °の場合は ' 0 '、90°の場合は ' 2 '、180の場合は ' 4 '、270の場合は ' 6 ') を指定します。キャプチャされたフレームは、画面を基準にして回転します。

### <a name="rotation-values"></a>回転値

回転角度の定義については、次に、ACPI の PLD データ構造を使用して説明します。

カメラとディスプレイが同じハウジング (または*エンクロージャ*/の*大文字と小文字*) を共有しているデバイスについては、これらの周辺機器を別の表面にマウントし、それぞれを固定した状態で回転させることができます。それぞれの面で。 そのため、アプリケーションには、キャプチャされたフレームを正しい向きでレンダリングサーフェイスに転置できるように、2つの周辺機器間の空間リレーションシップを記述するメカニズムが必要です。

この問題を解決する方法の1つとし\_て、既に*surface*と*回転角度*の概念が定義されている ACPI pld 構造体を使用する方法があります。 たとえば、 \_pld 構造体には既に、周辺機器が存在するサーフェイスを指定する*panel*フィールドがあります。

![ACPI \_pld パネルのフィールド定義](./images/acpi-pld-panel.png)

![デスクトップ pld パネル定義](./images/pld-panel-definitions-desktop.png)
![たたみ込み pld パネル定義](./images/pld-panel-definitions-foldable.png)

実際、ACPI の "panel" の概念は、次のような Windows によって既に採用されています。

カメラデバイスインターフェイスは、キャプチャデバイスが\_固定された場所に静的にマウントされている場合に、それに応じてパネルフィールドが設定される pld 構造に関連付けられています。

アプリケーションでは、 [EnclosureLocation](https://msdn.microsoft.com/en-us/library/windows/apps/windows.devices.enumeration.enclosurelocation.panel.aspx)プロパティを呼び出すことによって、キャプチャデバイスが存在するパネルを取得できます。

ACPI \_pld 構造体には、次のように定義されている回転フィールドもあります。

![ACPI \_pld の回転フィールドの定義](./images/acpi-pld-rotation.png)

上記の定義を "その他" として使用する代わりに、あいまいさを避けるためにさらに改良します。

カメラの場合、ACPI \_pld 構造の回転フィールドは、角度 (0 °の場合は ' 0 '、90°の場合は ' 2 '、180の場合は ' 4 '、270の場合は ' 6 ') を指定します。キャプチャされたフレームは、画面を基準にして回転します。

Windows では、**横**方向または**縦**方向のどちらかを返すプロパティ[DisplayInformation](https://msdn.microsoft.com/en-us/library/windows/apps/windows.graphics.display.displayinformation.nativeorientation.aspx)を呼び出すことによって、ネイティブの表示方向に対してクエリを実行できます。

![ネイティブの向きのスキャンパターンを表示する](./images/native-scanning-pattern.png)

値がどのよう**に返される**かに関係なく、論理ディスプレイのスキャンパターンは、左から右へ移動する画面の左上隅から開始されます (図5を参照)。 既定の物理的な向きが明示されていないデバイスについては、このプロパティは、ACPI*上*のパネルの場所を意味するだけでなく、カメラの出力バッファーとレンダリングサーフェイスの間の空間リレーションシップも提供します。

カメラとは異なり、"データ**指向**" プロパティは ACPI に基づいていないため、 \_pld 構造はありません。 これは、ディスプレイがデバイスに静的にマウントされている場合でも当てはまります。

上記のように、次の図は、各ハードウェア\_構成の pld 回転フィールドの値を示しています。

#### <a name="rotation-0-degree-clockwise"></a>ローテーション時計回りに0度

![0度回転の図](./images/rotation-0-degrees.png)

上の図では、次のようになります。

- 左側の画像は、キャプチャするシーンを示しています。
- 中央の画像は、左側から上に向かって左から右へ移動する、CMOS センサーによってシーンがどのように表示されるかを示しています。
- 右側の画像は、カメラドライバーの出力を表しています。 この例では、メディアバッファーの内容を直接レンダリングできます。一方、ディスプレイは、追加の回転を必要としないネイティブな方向です。 その結果、ACPI \_pld 回転フィールドの値は0になります。

#### <a name="rotation-90-degrees-clockwise"></a>ローテーション90°時計回り

![90度回転の図](./images/rotation-90-degrees.png)

この場合、元のシーンと比較して、メディアバッファーの内容が時計回りに90°回転します。 その結果、ACPI \_pld の回転フィールドの値は2になります。

#### <a name="rotation-180-degrees-clockwise"></a>ローテーション180°時計回り

![180度回転の図](./images/rotation-180-degrees.png)

この場合、元のシーンと比較して、メディアバッファーの内容が時計回りに180°回転します。 その結果、ACPI \_pld 回転フィールドの値は4になります。

#### <a name="rotation-270-degrees-clockwise"></a>ローテーション270°時計回り

![270度回転の図](./images/rotation-270-degrees.png)

この場合、元のシーンと比較して、メディアバッファーの内容が時計回りに270°回転します。 その結果、ACPI \_pld 回転フィールドの値は6になります。

### <a name="offset-mounting"></a>オフセットマウント

アプリケーションの互換性を維持するために、センサーを0°以外のオフセットでマウントしないようにすることを強くお勧めします。 既存のアプリとレガシアプリの多くでは、ACPI の PLD テーブルを探すことはできません。また、0でない角度オフセットの修正も試行されません。 そのため、このようなアプリでは、結果として得られるビデオが正しくレンダリングされません。

前述のように、IHV/Oem がセンサーを0度でマウントできない場合は、次の対策手順を優先順位でお勧めします。

1. カメラドライバー内で0度以外の向きを修正します (AV ストリームミニポートドライバーを使用したカーネルモード、またはデバイス MFT や MFT0 などのプラグインを使用してユーザーモードで)。結果の出力フレームは、0度の向きになります。
2. カメラのパイプラインがキャプチャされたイメージを修正できるように、FSSensorOrientation タグを使用して0度以外の方向を宣言します。
3. 上記の説明に従って、ACPI の PLD テーブルで0度以外の方向を宣言します。

### <a name="av-stream-miniportdevice-mftmft0"></a>AV ストリームミニポート/デバイス MFT/MFT0

センサーを0度オフセットでマウントできない場合の理想的なシナリオは、AV ストリームミニポートドライバー (または、DMFT または MFT0 のいずれかの形式のユーザーモードプラグイン) で、結果として生成されるフレームを修正して、0度のオフセットでパイプラインに公開することです。

AV ストリームのミニポートまたはデバイスの MFT/MFT0 プラグインからビデオフレームを修正する場合、結果として得られるメディアの種類の宣言は、修正されたフレームに基づいている必要があります。 センサーが90度のオフセットでマウントされ、結果として得られるビデオはセンサーからの9:16 の縦横比ですが、修正されたビデオは16:9 であるため、メディアの種類は16:9 の縦横比を宣言する必要があります。

これには、結果として得られる stride 情報が含まれます。 このことが必要なのは、修正を行うコンポーネントが IHV/OEM によって制御されており、カメラのパイプラインが、修正された後を除き、ビデオフレームを表示できない場合です。

ユーザーモードで修正を実行し、パイプラインとユーザーモードプラグイン間の API コントラクトを従う必要があることを強くお勧めします。 具体的には、dmft または MFT0 のいずれかを使用しているときに、imfdevicetransform::P roて message または imftransform::P\_roが\_、\_MFT メッセージ\_セットの D3D マネージャーメッセージを使用して呼び出された場合、ユーザーモードになります。プラグインは、次のガイドラインに従う必要があります。

- D3D マネージャーが指定されていない場合 (メッセージの ulParam が0の場合)、ユーザーモードプラグインは、ローテーションの修正を処理する GPU 操作を呼び出さないようにする必要があります。 また、結果として得られるフレームは、システムメモリ内に提供される必要があります。
- D3D マネージャーが提供されている場合 (メッセージの ulParam が DXGI マネージャーの IUnknown である場合) は、その DXGI マネージャーを使用して回転を修正する必要があり、結果のフレームは GPU メモリである必要があります。
- ユーザーモードプラグインは、実行時に D3D マネージャーメッセージも処理する必要があります。 MFT\_メッセージ\_セット\_D3Dマネージャーメッセージが発行されたときに、プラグインによって生成される次のフレームは、要求されたメモリの種類(たとえば、DXGIマネージャーが提供された場合はGPU、CPU以外)に対応する必要があります。\_
- AV ストリームドライバー (またはユーザーモードプラグイン) がローテーションの修正を処理するときは、ACPI の PLD 構造体の回転フィールドを0に設定する必要があります。

### <a name="fssensororientation"></a>FSSensorOrientation

```INF
; Defines the sensor mounting orientation offset angle in
; degrees clockwise.
FSSensorOrientation: REG_DWORD: 90, 180, 270
```

FSSensorOrientation レジストリタグを介してセンサーの0度以外の方向を宣言することで、カメラのパイプラインは、キャプチャされたフレームを修正してからアプリケーションに提示することができます。

パイプラインは、ユースケースとアプリの要求/シナリオに基づいて GPU または CPU リソースを活用することで、ローテーションロジックを最適化します。

#### <a name="acpi-pld-rotation"></a>ACPI PLD ローテーション

ACPI PLD 構造体の回転フィールドは0である必要があります。 これは、PLD 情報を使用してフレームを修正する可能性のあるアプリケーションの混乱を避けるためです。

#### <a name="media-type-information"></a>メディアの種類の情報

ドライバーによって提示されるメディアの種類は、修正されていないメディアの種類である必要があります。 FSSensorOrientation エントリを使用して、0度オフセット以外のカメラパイプラインに通知する場合、センサーによって示されるメディアの種類の情報は、修正されていないメディアの種類である必要があります。 たとえば、センサーが90°時計回りのオフセットでマウントされている場合、16:9 の縦横比ではなく、最終的なビデオは9:16 で、9:16 の縦横比のメディアの種類をカメラのパイプラインに表示する必要があります。

これは、パイプラインがカウンターローテーションプロセスを正しく構成できるようにするために必要です。パイプラインには、アプリケーションの入力メディアの種類と必要な出力メディアの種類が必要です。

これには、stride 情報が含まれます。 メディアの種類が修正されていない場合は、stride 情報をカメラパイプラインに提示する必要があります。

#### <a name="registry-subkey"></a>レジストリ サブキー

FSSensorOrientation レジストリエントリは、デバイスインターフェイスノードに発行する必要があります。 カメラドライバーの INF の AddInterface ディレクティブ宣言中に、これを AddReg ディレクティブとして宣言することをお勧めします。

Fssensororientation に表示されるデータは REG\_DWORD である必要があり、有効な値は90、180、および270だけです。 その他の値は0°オフセットとして処理されます (つまり、無視されます)。

各値は、時計回りの角度でセンサーの向きを表します。 カメラパイプラインは、ビデオを同じ量のカウンターで時計回りに回転するカウンターによって、結果として得られるビデオフレームを修正します。つまり、90度時計回りの宣言では、90度に反時計回りの回転が行われ、結果のビデオフレームが0に戻ります。度オフセット。

#### <a name="ms-os-descriptor-10"></a>MS OS 記述子1.0

USB ベースのカメラの場合は、MSOS の記述子を使用して FSSensorOrientation を公開することもできます。

<!-- FIXME: Overview of OS descriptor could be removed -->
MS OS 記述子1.0 には、次の2つのコンポーネントがあります。

- 固定長ヘッダーセクション
- ヘッダーセクションの後に続く1つ以上の可変長カスタムプロパティセクション

##### <a name="ms-os-descriptor-10-header-section"></a>MS OS 記述子1.0 ヘッダーセクション

ヘッダーセクションでは、1つのカスタムプロパティ (Face Auth Profile) について説明します。

| Offset | フィールド      | サイズ (バイト) | 値  | 説明                     |
| ------ | ---------- | ------------ | ------ | ------------------------------- |
| 0      | dwLength   | 4            | \<\>   |                                 |
| 4      | bcdVersion | 2            | 0x0100 | バージョン 1.0                     |
| 6      | wIndex     | 2            | 0x0005 | 拡張プロパティの OS 記述子 |
| 8      | wCount     | 2            | 0x0001 | 1つのカスタムプロパティ             |

##### <a name="custom-ms-os-descriptor-10-property-section"></a>カスタム MS OS 記述子1.0 プロパティセクション

| Offset | フィールド                | サイズ (バイト) | [値]                              | 説明                                  |
| ------ | -------------------- | ------------ | ---------------------------------- | -------------------------------------------- |
| 0      | dwSize               | 4            | 0x00000036 (54)                    | このプロパティの合計サイズ (バイト単位)。     |
| 4      | dwPropertyDataType   | 4            | 0x00000004                         | REG\_DWORD\_リトル\_エンディアン                   |
| 8      | wPropertyNameLength  | 2            | 0x00000024 (36)                    | プロパティ名のサイズ (バイト単位)。        |
| 10     | bPropertyName        | 50           | UVC-FSSensorOrientation            | Unicode での "UVC-FSSensorOrientation" 文字列。 |
| 60     | dwPropertyDataLength | 4            | 0x00000004                         | プロパティデータ (sizeof (DWORD)) の場合は4バイト。   |
| 64     | bPropertyData        | 4            | 時計回りのオフセット角度 (度単位)。 | 有効な値は、90、180、および270です。           |

#### <a name="ms-os-descriptor-20"></a>MS OS 記述子2.0

MSOS 拡張記述子2.0 を使用して、FSSensorOrientation サポートを追加するためのレジストリ値を定義できます。 これを行うには、 [MICROSOFT OS 2.0 のレジストリプロパティ記述子](#microsoft-os-20-registry-property-descriptor)を使用します。

UVC-FSSensorOrientation レジストリエントリの場合、MSOS 2.0 記述子セットの例を次に示します。

```cpp
UCHAR Example2_MSOS20DescriptorSet_UVCFSSensorOrientationForFutureWindows[0x3C] =
{
    //
    // Microsoft OS 2.0 Descriptor Set Header
    //
    0x0A, 0x00,                 // wLength - 10 bytes
    0x00, 0x00,                 // MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x0?, 0x06,     // dwWindowsVersion – 0x060?0000 for future Windows version
    0x4A, 0x00,                 // wTotalLength – 74 bytes

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x40, 0x00,                 // wLength - 64 bytes
    0x04, 0x00,                 // wDescriptorType – 4 for Registry Property
    0x04, 0x00,                 // wPropertyDataType - 4 for REG_DWORD_LITTLE_ENDIAN
    0x32, 0x00,                 // wPropertyNameLength – 50 bytes
    0x55, 0x00, 0x56, 0x00,     // Property Name - "UVC-FSSensorOrientation"
    0x43, 0x00, 0x2D, 0x00,
    0x46, 0x00, 0x53, 0x00,
    0x53, 0x00, 0x65, 0x00,
    0x6E, 0x00, 0x73, 0x00,
    0x6F, 0x00, 0x72, 0x00,
    0x4F, 0x00, 0x72, 0x00,
    0x69, 0x00, 0x65, 0x00,
    0x6E, 0x00, 0x74, 0x00,
    0x61, 0x00, 0x74, 0x00,
    0x69, 0x00, 0x6F, 0x00,
    0x6E, 0x00, 0x00, 0x00,
    0x00, 0x00,
    0x04, 0x00,                 // wPropertyDataLength – 4 bytes
    0x5A, 0x00, 0x00, 0x00      // PropertyData – 0x0000005A (90 degrees offset)
}
```

### <a name="acpi-pld-information"></a>ACPI PLD 情報

最後の手段として、前に説明したように PLD 情報を利用して、レンダリングまたはエンコードする前にビデオフレームを修正する必要があることをアプリケーションに示すことができます。 ただし、既に説明したように、既存のアプリケーションの多くは PLD 情報を使用せず、フレームのローテーションも処理しないため、アプリが結果のビデオを正しく表示できない場合があります。

### <a name="compressedencoded-media-types"></a>圧縮/エンコードされたメディアの種類

圧縮またはエンコードされたメディアの種類 (MJPG、JPEG、H264、HEVC など) の場合は、パイプラインを正しく使用できません。 このため、FSSensorOrientation が0以外の値に設定されている場合、圧縮またはエンコードされたメディアの種類はフィルターで除外されます。

MJPG メディアタイプ (UVC カメラなど) の場合、フレームサーバーパイプラインは、自動デコードされたメディアの種類 (NV12 または YUY2 ベースのアプリケーションの場合は YUY2) を提供します。 自動デコードおよび修正されたメディアの種類が表示されますが、元の MJPG 形式は表示されません。

圧縮またはエンコードされたメディアの種類をアプリケーションに公開する必要がある場合、IHV/Odm は FSSensorOrientation の修正を利用することはできません。 代わりに、カメラドライバー (AV ストリームドライバーを介してカーネルモードにするか、DMFT/MFT0 を使用してユーザーモードで) で修正を行う必要があります。

## <a name="bos-and-ms-os-20-descriptor"></a>BOS および MS OS 2.0 記述子

UVC 準拠カメラは、 [MICROSOFT OS 2.0 の記述子](https://msdn.microsoft.com/en-us/library/windows/hardware/dn385747.aspx)を使用して、ファームウェアのプラットフォーム機能 BOS 記述子に Windows 固有のデバイス構成値を指定できます。 デバイス構成を OS に伝える有効な BOS 記述子を指定する方法については、MS OS 2.0 記述子のドキュメントを参照してください。

### <a name="microsoft-os-20-descriptor-set-header"></a>Microsoft OS 2.0 記述子セットヘッダー

| Offset | フィールド            | サイズ (バイト) | 説明                                                                  |
| ------ | ---------------- | ------------ | ---------------------------------------------------------------------------- |
| 0      | wLength          | 2            | このヘッダーの長さ (バイト単位) は10である必要があります。                                  |
| 2      | W記述子の種類  | 2            | MSOS20\_SET\_ヘッダー記述子\_                                              |
| 4      | dwWindowsVersion | 4            | Windows のバージョン。                                                             |
| 8      | wTotalLength     | 2            | このヘッダーサイズを含む、MS OS 2.0 descrioptor セット全体のサイズ。 |

### <a name="microsoft-os-20-registry-property-descriptor"></a>Microsoft OS 2.0 レジストリプロパティ記述子

| Offset | フィールド               | サイズ (バイト) | 説明                        |
| ------ | ------------------- | ------------ | ---------------------------------- |
| 0      | wLength             | 2            | この記述子の長さ (バイト単位) |
| 2      | W記述子の種類     | 2            | MS\_OS\_20機能\_のREG\_プロパティ\_ |
| 4      | wPropertyDataType   | 2            | 0x04 (REG\_DWORD\_リトル\_エンディアン)  |
| 6      | wPropertyNameLength | 2            | プロパティ名の長さ。   |
| 8      | PropertyName        | 変数     | レジストリプロパティの名前。 |
| 8 + M    | wPropertyDataLength | 2            | プロパティデータの長さ。   |
| 10 + M   | PropertyData        | 変数     | プロパティデータ                      |

ファームウェアに有効な MS OS 2.0 記述子が指定されている場合、USB スタックは、次の表に示すデバイスの HW レジストリキーに構成値をコピーします。

```Registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USB\<Device ID>\<Instance ID>\Device Parameters
```

UVC ドライバーは、デバイスのハードウェアレジストリキーから構成値を読み取り、それに応じて OS 上のデバイスを構成します。 たとえば、ファームウェアで、構成値を使用してセンサーカメラとして登録するデバイスを指定した場合、UVC ドライバーはそのカテゴリの直下にデバイスを登録します。

プラットフォーム BOS 記述子を使用した UVC デバイスの構成は、Windows 10 バージョン1703で有効にされたメカニズムであり、UVC デバイスベンダーが Windows OS で INF ファイルを使用しなくてもデバイスを構成できるようにします。

カスタム INF を使用した UVC デバイスの構成は引き続きサポートされており、これは BOS 記述子ベースのメカニズムよりも優先されます。 INF を使用してデバイスのプロパティを指定するときに、プレフィックス "UVC-" を追加する必要はありません。 このプレフィックスは、BOS 記述子によって指定され、インターフェイスインスタンスごとに固有のデバイスプロパティにのみ必要です。 デバイスに DMFT などのユーザーモードプラグインが必要な場合は、DMFT をインストールするための INF を用意する必要があります。 ファームウェアを使用して構成することはできません。

## <a name="currently-supported-configuration-values-through-bos-descriptor"></a>現在サポートされている構成値 (BOS 記述子を使用)

| 構成名 | 種類 | 説明 |
| --- | --- | --- |
| SensorCameraMode                              | REG\_DWORD | 特定のカテゴリの下にカメラを登録します。  |
| UVC-FSSensorGroupID<br>UVC-FSSensorGroupName  | REG\_SZ    | 同じ UVC-FSSensorGroupID でカメラをグループ化する |
| UVC-EnableDependentStillPinCapture            | REG\_DWORD | 引き続きキャプチャメソッド2/3 を有効にするには              |
| UVC-EnablePlatformDmft                        | REG\_DWORD | Platform DMFT を有効にするには                         |

UVC ドライバーは、プレフィックスが "UVC-" のレジストリ値を認識すると、デバイスのカテゴリインターフェイスインスタンスレジストリキーを、プレフィックスなしの同じ値で設定します。 ドライバーは、上記のように、ファームウェアによって指定された任意の変数に対してこれを実行します。

```Registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{e5323777-f976-4f5b-9b55-b94699c46e44}\<Device Symbolic Link>\Device Parameters
```

OS で BOS Platform Device 機能と MS OS 2.0 記述子を使用するには、デバイス記述子で bcdUSB バージョンを0x0210 以上に指定する必要があります。

## <a name="example-composite-device"></a>複合デバイスの例

このセクションでは、2つのカメラ機能を備えたサンプル複合デバイス用の BOS 記述子と MS OS 2.0 記述子を提供します。 1つの関数は UVC カラーカメラで、2番目の関数は UVC IR カメラです。

サンプル記述子は次のとおりです。

1. カラーカメラ機能を KSCATEGORY\_ビデオ\_カメラに登録する

1. KSCATEGORY\_センサー\_カメラの下に IR カメラ機能を登録する

1. イメージキャプチャのカラーカメラ機能の有効化

1. 色と IR カメラの機能をグループとして関連付けます

デバイスの列挙時に、USB スタックはデバイスから BOS 記述子を取得します。 BOS 記述子の後には、プラットフォーム固有のデバイス機能があります。

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

BOS プラットフォーム機能記述子は次を指定します。

1. MS OS 2.0 記述子プラットフォームの機能 GUID

1. ベンダ制御コード bms\_VendorCode (ここでは1に設定されています)。 MS OS 2.0 記述子を取得するために、ベンダーが推奨する任意の値を使用できます)。

1. この BOS 記述子は、Windows 10 以降の OS バージョンに適用されます。

BOS 記述子が表示された後、USB スタックは、MS OS 2.0 記述子を取得するためにベンダー固有の制御要求を発行します。

MS OS 2.0 ベンダー固有の記述子を取得するためのコントロール要求の形式:

| bmRequestType | BRequest            | wValue | WIndex | wLength | data                                   |
|---------------|---------------------|--------|--------|---------|----------------------------------------|
| 1100 0000B    | **bms\_VendorCode** | 0x00   | 0x07   | 長さ  | MS OS 2.0 記述子セット blob が返されました |

_**bmRequestType**_

- データ転送方向–ホストするデバイス

- 種類–ベンダ

- 受信デバイス

_**bRequest**_

記述子セット情報構造体で返される **\_bms VendorCode**値。

_**wValue**_

を0x00 に設定します。

_**wIndex**_

MS\_OS\_20\_記述子インデックスの0x7。\_

_**wLength**_

BOS 記述子で返される MS OS 2.0 記述子セットの長さ。 この例では、0x25C (604) です。

デバイスは、USBVideoMSOS20DescriptorSet で指定されたものと同様に、MS OS 2.0 記述子を返すことが想定されています。

USBVideoMSOS20DescriptorSet は、色と IR の機能について説明します。 次の MS OS 2.0 記述子の値を指定します。

1. ヘッダーの設定

1. 構成サブセットヘッダー

1. カラーカメラ関数のサブセットヘッダー

1. センサーグループ ID のレジストリ値機能記述子

1. センサーグループ名のレジストリ値機能記述子

1. 静止イメージキャプチャを有効にするためのレジストリ値機能記述子

1. Platform DMFT を有効にするためのレジストリ値機能記述子

1. IR カメラ関数のサブセットヘッダー

1. センサーグループ ID のレジストリ値機能記述子

1. センサーグループ名のレジストリ値機能記述子

1. カメラをセンサーカメラとして登録するためのレジストリ値機能記述子

このファームウェアは、このセクションの冒頭で説明されている架空のデバイスに対して、次の MS OS 2.0 記述子を返すベンダー要求のハンドラーを持っています。

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
