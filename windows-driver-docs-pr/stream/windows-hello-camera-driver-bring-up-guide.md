---
title: Windows Hello カメラドライバーの導入ガイド
description: このトピックでは、赤外線 (IR) カメラの顔認証を有効にする方法について説明します。これは、相手先ブランド供給メーカー (Oem) および独立系ハードウェアベンダー (Ihv) を対象としています。
ms.assetid: 5CE619F4-E136-4F8F-8F90-F7F96DE4642E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a846f48b31ebca49ffa050618ee795f6b553d18
ms.sourcegitcommit: eb1f58d23da3b1240385c072837d9118239a8f97
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2020
ms.locfileid: "75883879"
---
# <a name="camera-driver-bring-up-guide"></a>カメラ ドライバー構築ガイド

このトピックでは、赤外線 (IR) カメラの顔認証を有効にする方法について説明します。これは、相手先ブランド供給業者 (Oem) と、デバイスにこの機能を提供する独立系ハードウェアベンダー (Ihv) を対象としています。

## <a name="frameserver"></a>FrameServer

次の図は、FrameServer が新しいドライバースタックでどのように動作するかを示しています。

![windows hello および frameserver](images/windows-hello-device-model.png)

## <a name="face-authentication-ddis"></a>顔認証 DDIs

Windows 10 バージョン1607では、Windows Hello をサポートする2つの新しい face authentication DDI コンストラクトが用意されています。

- **KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FACEAUTH\_モード**

  このプロパティ ID は、次のフラグを使用してドライバーで顔認証を有効にし、構成するために使用されます。

  - **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_無効**

  - **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_代替\_フレーム\_照明**

  - **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_バックグラウンド\_減算**

  このコントロールの詳細と、ビットフラグを使用して顔認証モードを設定する方法の詳細については、「 [**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_FACEAUTH\_mode**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-faceauth-mode) 」を参照してください。

- **MF\_\_メタデータ\_フレーム\_の照明をキャプチャする**

    IR カメラのこのメタデータ属性は、フレームがアクティブな IR 照明を使用していることを指定します。 詳細については、「 [Capture Stats Metadata attributes](mf-capture-metadata.md) 」トピックの「必須メタデータ属性」の表を参照してください。

## <a name="usb-camera-support"></a>USB カメラのサポート

デバイスで赤外線カメラの顔認証を有効にするには、適切に構成された DeviceMFT コンポーネントと USB Video Class (UVC) 拡張機能ユニットを提供する必要があります。

### <a name="configure-the-devicemft-component"></a>DeviceMFT コンポーネントの構成

デバイスでの顔認証をサポートする DeviceMFT コンポーネントを構築するための出発点として、 [sampledevicemft](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/driver-device-transform-sample/)サンプルを使用できます。

ドライバーサンプルを変更するには、サンプルのソースコードを次のように変更します。

1. DeviceMFT コンポーネントでソースの種類の情報を追加する

1. DeviceMFT コンポーネントの照明フラグにタグを付ける

1. DeviceMFT コンポーネントの Iksk コントロールを変換し、次のセクションで作成する UVC 拡張機能ユニットと通信します。

### <a name="build-a-usb-video-class-uvc-extension-unit"></a>USB Video Class (UVC) 拡張機能ユニットを作成する

デバイスの UVC 拡張機能ユニットをビルドするには、「[拡張機能単体サンプルコントロールのビルド](building-the-extension-unit-sample-control.md)」の手順に従います。 このトピックでは、必要なプロジェクトファイルの作成について説明し、次のトピックのサンプルコードへのリンクを示します。

[UVC 拡張単位のサンプルインターフェイス](sample-interface-for-uvc-extension-units.md)(*インターフェイス .idl*を含む)

[サンプル拡張機能単体プラグイン DLL](sample-extension-unit-plug-in-dll.md) ( *xuproxy .H*と*xuproxy*を含む)

[UVC 拡張機能ユニットのサンプルレジストリエントリ](sample-registry-entry-for-uvc-extension-units.md)( *xusample .rgs*を含む))

[UVC 拡張機能ユニットのサンプルアプリケーション](sample-application-for-uvc-extension-units.md)( *TestApp を*含む)

[拡張機能ユニットを使用した自動更新イベントのサポート](supporting-autoupdate-events-with-extension-units.md)

[拡張機能の単位記述子のサンプル](sample-extension-unit-descriptor.md)

[UVC INF ファイルの提供](providing-a-uvc-inf-file.md)

サンプルコードモジュールを連携させる方法の詳細については、[拡張機能単体プラグインアーキテクチャ](extension-unit-plug-in-architecture.md)に関するトピックを参照してください。

## <a name="inf-file-entries"></a>INF ファイルのエントリ

**KSCATEGORY\_センサー\_カメラ**で uvc デバイスを登録するには、センサーカメラの昇格フラグを指定する必要があります。

```INF
HKR,,SensorCameraMode,0x00010001,0x00000001
```

RGB ストリームがないため、このカメラを通常のカメラアプリから非表示にするには、次のように、skip 列挙フラグを使用します。

```INF
HKR,,SkipCameraEnumeration,0x00010001,0x00000001
```

これにより、カメラが**KSCATEGORY\_ビデオ**から削除されます。これにより、通常のカメラアプリによる従来の列挙によって、このカメラが列挙されるのを防ぐことができます。

**SkipCameraEnumeration**と**SensorCameraMode**の両方のエントリは、INF ファイルの**ddinstall. HW**セクションに配置する必要があります。

## <a name="hlk-tests-for-kscategory_sensor_camera-to-assist-driver-testing"></a>ドライバーのテストを支援するための KSCATEGORY\_センサー\_カメラの HLK テスト

ハードウェアロゴキット (HLK) のテストは、IR および RGB カメラモジュールの両方に必要です。 このテストでは、Windows Hello face authentication で使用される RGB および IR カメラの基本機能を確認します。 RGB カメラの要件は、HLK テストスイートで既に指定されています。

IR カメラモジュールを有効にするために渡す必要があるテストは次のとおりです。

1. すべての KS センサーカテゴリカメラを列挙します:

    - IR ストリームをサポートするデバイスは、[センサー\_カメラ] カテゴリの下にある必要があります。

    - RGB ストリームをサポートするデバイスは、[ビデオ\_カメラ] カテゴリの下に表示されます。

    - IR と RGB ストリームをサポートする1つのカメラデバイスの場合にのみ、KSCAMERA カテゴリ (センサー\_カメラとビデオ\_カメラ) の両方にデバイスを登録する必要があります。

1. **MF\_DEVICESTREAM\_attribute\_FACEAUTH\_機能**属性が定義されているストリームを検索します。

    - **MF\_DEVICESTREAM\_attribute\_FACEAUTH\_機能**属性が定義されているストリームがない場合は、テストをスキップします。

    - 複数のストリームに**MF\_DEVICESTREAM\_属性\_FACEAUTH\_機能**属性が定義されている場合は、1つのストリームだけが Windows Hello に対応する必要があるため、テストは失敗します。

    - **MF\_DEVICESTREAM\_属性\_FRAMESOURCE\_types**がこのストリームの IR に設定されていない場合、このストリームには RGB メディアの種類が存在しないため、テストは失敗します。

    - このストリームを選択し、メディアの種類が Windows Hello 対応 (MJPG/L8/NV12) であり、解像度が 320 x 320 ピクセル以上であることを確認します。

        1. Face Authentication プロファイルがサポートされている場合は、プロファイルメディアの種類に対してこのストリームを検証します。

        1. Face Authentication プロファイルがサポートされていない場合は、このストリームの既定のメディアの種類を検証します。

    - 顔認証 DDI では、光/オフまたはアンビエント減算のいずれかのプロパティがサポートされているかどうかを確認します。

    - KS プロパティを、サポートされているものに設定します。

    - ストリーミングの開始

1. 実行時のプロパティを確認します。

    - タイムスタンプの精度を確認します (Meta Data による顔認証のプレビューテスト)。

    - スタートアップが500ミリ秒未満であることを確認します (Meta Data による顔認証のプレビューテスト)。
  
    - 次のパラメーターを使用して、ストリーミングを最小フレームレートで確認します:15 FPS の点灯と 15 FPS のアンビエントまたは 15 fps のアンビエント減算、解像度が 320 x 320 ピクセル以上、メディアの種類の L8/NV12、サンプルの肯定 stride。

        1. "照明" プロパティが有効になっている場合は、フレームのメタデータを確認します (照明された、またはオフになっている、15 FPS のペアのフレーム)。

        1. アンビエント減算プロパティが有効になっている場合は、フレームにメタデータがないかどうかを確認します (15 FPS のアンビエントフレーム)。

1. [ストリーミング停止]

1. KS コントロールの設定を解除します。

1. RGB + IR の同時実行: カメラプロファイルで定義されているかどうかをテストします

上記の HLK テストが渡されない場合、Microsoft は OEM に署名されたドライバーを発行せず、Windows Hello は動作しません。

## <a name="related-topics"></a>関連トピック

[MediaCapture を使った写真とビデオのキャプチャ](https://docs.microsoft.com/windows/uwp/audio-video-camera/capture-photos-and-video-with-mediacapture)  

[Windows. Media. 名前空間](https://docs.microsoft.com/uwp/api/Windows.Media.Capture)  
