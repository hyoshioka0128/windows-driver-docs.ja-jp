---
title: Windows Hello カメラドライバーの導入ガイド
description: このトピックでは、赤外線 (IR) カメラの顔認証を有効にする方法について説明します。これは、相手先ブランド供給メーカー (Oem) および独立系ハードウェアベンダー (Ihv) を対象としています。
ms.assetid: 5CE619F4-E136-4F8F-8F90-F7F96DE4642E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a573ed83a4e40ba1d4d1dee059fcd8a31901035
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565690"
---
# <a name="camera-driver-bring-up-guide"></a>カメラ ドライバー構築ガイド

このトピックでは、赤外線 (IR) カメラの顔認証を有効にする方法について説明します。これは、相手先ブランド供給業者 (Oem) と、デバイスにこの機能を提供する独立系ハードウェアベンダー (Ihv) を対象としています。

## <a name="frameserver"></a>FrameServer

次の図は、FrameServer が新しいドライバースタックでどのように動作するかを示しています。

![windows hello および frameserver](images/windows-hello-device-model.png)

## <a name="face-authentication-ddis"></a>顔認証 DDIs

Windows 10 バージョン1607では、Windows Hello をサポートする2つの新しい face authentication DDI コンストラクトが用意されています。

-   **KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FACEAUTHモード\_**

    このプロパティ ID は、次のフラグを使用してドライバーで顔認証を有効にし、構成するために使用されます。

    -   **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_が無効になりました**

    -   **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モードの代替\_フレーム照明\_\_**

    -   **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_MODEバックグラウンド\_減算\_**

    このコントロールの詳細と、ビットフラグを使用して顔認証モードを設定する方法の詳細については、「 [**ksk プロパティ\_CAMERACONTROL\_\_EXTENDED FACEAUTH\_mode**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-faceauth-mode) 」を参照してください。

-   **MF\_キャプチャ\_メタデータ\_フレーム\_の照明**

    IR カメラのこのメタデータ属性は、フレームがアクティブな IR 照明を使用していることを指定します。 詳細については、「 [Capture Stats Metadata attributes](mf-capture-metadata.md) 」トピックの「必須メタデータ属性」の表を参照してください。

## <a name="usb-camera-support"></a>USB カメラのサポート

デバイスで赤外線カメラの顔認証を有効にするには、適切に構成された DeviceMFT コンポーネントと USB Video Class (UVC) 拡張機能ユニットを提供する必要があります。

### <a name="configure-the-devicemft-component"></a>DeviceMFT コンポーネントの構成

デバイスで顔認証をサポートする DeviceMFT コンポーネントを構築するための出発点として、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリにある[sampledevicemft](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/sampledevicemft)サンプルを使用できます。

ドライバーサンプルを変更するには、 [Windows-driver-samples-master](https://github.com/Microsoft/Windows-driver-samples/archive/master.zip)をダウンロードして抽出するか、git を使用して Windows ドライバーサンプルリポジトリを開発用コンピューターに複製します。 **Avstream**フォルダーにある**sampledevicemft**サンプルに移動し、サンプルソースコードに次の変更を加えます。

1.  DeviceMFT コンポーネントでソースの種類の情報を追加する

2.  DeviceMFT コンポーネントの照明フラグにタグを付ける

3.  DeviceMFT コンポーネントの Iksk コントロールを変換し、次のセクションで作成する UVC 拡張機能ユニットと通信します。

### <a name="build-a-usb-video-class-uvc-extension-unit"></a>USB Video Class (UVC) 拡張機能ユニットを作成する

デバイスの UVC 拡張機能ユニットをビルドするには、「[拡張機能単体サンプルコントロールのビルド](building-the-extension-unit-sample-control.md)」の手順に従います。 このトピックでは、必要なプロジェクトファイルの作成について説明し、次のトピックのサンプルコードへのリンクを示します。

[UVC 拡張機能ユニットのサンプルインターフェイス](sample-interface-for-uvc-extension-units.md)( *.idl を*含む)

[サンプル拡張機能単体プラグイン DLL](sample-extension-unit-plug-in-dll.md)( *xuproxy .h*と*xuproxy .cpp*を含む)

[UVC 拡張機能ユニットのサンプルレジストリエントリ](sample-registry-entry-for-uvc-extension-units.md)( *Xusample .rgs を*含む))

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

これにより、カメラ**が\_KSCATEGORY ビデオ**から削除されます。これにより、通常のカメラアプリによる従来の列挙によって、このカメラが列挙されるのを防ぐことができます。

**SkipCameraEnumeration**と**SensorCameraMode**の両方のエントリは、INF ファイルの**ddinstall. HW**セクションに配置する必要があります。

## <a name="hlk-tests-for-kscategory_sensor_camera-to-assist-driver-testing"></a>ドライバーのテストを\_支援\_する KSCATEGORY センサーカメラの HLK テスト


ハードウェアロゴキット (HLK) のテストは、IR および RGB カメラモジュールの両方に必要です。 このテストでは、Windows Hello face authentication で使用される RGB および IR カメラの基本機能を確認します。 RGB カメラの要件は、HLK テストスイートで既に指定されています。

IR カメラモジュールを有効にするために渡す必要があるテストは次のとおりです。

1.  すべての KS センサーカテゴリカメラを列挙します:

    -   IR ストリームをサポートするデバイスは、[センサー\_カメラ] カテゴリの下にある必要があります。

    -   RGB ストリームをサポートするデバイスは、[\_ビデオカメラ] カテゴリの下に表示されます。

    -   IR と RGB ストリームをサポートする1つのカメラデバイスに対してのみ、デバイスを両方の KSCAMERA カテゴリに登録する必要があります。センサー\_カメラとビデオ\_カメラ。

2.  次のように、 **MF\_devicestream\_attribute\_FACEAUTH\_機能**属性が定義されているストリームを検索します。

    -   どのストリームにも、 **MF\_devicestream\_attribute\_FACEAUTH\_機能**属性が定義されていない場合は、テストをスキップします。

    -   複数のストリームで、 **MF\_devicestream\_attribute\_FACEAUTH\_機能**属性が定義されている場合、テストは失敗します。これは、Windows Hello 対応のストリームが1つだけであるためです。

    -   このストリームに対して、 **\_MF\_devicestream\_\_属性の framesource の種類**が IR に設定されていない場合、このストリームには RGB メディアの種類が存在しないため、テストは失敗します。

    -   このストリームを選択し、メディアの種類が Windows Hello 対応 (MJPG/L8/NV12) であり、解像度が 320 x 320 ピクセル以上であることを確認します。

        1.  Face Authentication プロファイルがサポートされている場合は、プロファイルメディアの種類に対してこのストリームを検証します。

        2.  Face Authentication プロファイルがサポートされていない場合は、このストリームの既定のメディアの種類を検証します。

    -   Face authentication DDI で、次のいずれかのプロパティがサポートされていることを確認します。照明/非光またはアンビエント減算。

    -   KS プロパティを、サポートされているものに設定します。

    -   ストリーミングの開始

3.  実行時のプロパティを確認します。

    -   タイムスタンプの精度を確認します (Meta Data による顔認証のプレビューテスト)。

    -   スタートアップが500ミリ秒未満であることを確認します (Meta Data による顔認証のプレビューテスト)。

    -   次のパラメーターを使用して、ストリーミングを最小フレームレートで検証します。15 FPS の点灯と 15 FPS のアンビエントまたは 15 fps のアンビエント減算、解像度が 320 x 320 ピクセル以上、メディアの種類 L8/NV12、サンプルの肯定 stride。

        1.  "照明" プロパティが有効になっている場合は、フレームのメタデータを確認します (照明された、またはオフになっている、15 FPS のペアのフレーム)。

        2.  アンビエント減算プロパティが有効になっている場合は、フレームにメタデータがないかどうかを確認します (15 FPS のアンビエントフレーム)。

4.  [ストリーミング停止]

5.  KS コントロールの設定を解除します。

6.  RGB + IR の同時実行: カメラプロファイルで定義されているかどうかをテストします

上記の HLK テストが渡されない場合、Microsoft は OEM に署名されたドライバーを発行せず、Windows Hello は動作しません。

## <a name="related-topics"></a>関連トピック

[MediaCapture を使った写真とビデオのキャプチャ](https://docs.microsoft.com/windows/uwp/audio-video-camera/capture-photos-and-video-with-mediacapture)  

[Windows. Media. 名前空間](https://docs.microsoft.com/uwp/api/Windows.Media.Capture)  
