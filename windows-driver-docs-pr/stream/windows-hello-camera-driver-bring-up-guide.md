---
title: Windows こんにちはカメラのドライバー ガイドを表示します。
description: このトピックでは、赤外線 (IR) カメラの顔認証を有効にする方法について説明し、相手先ブランド供給 (Oem) および独立系ハードウェア ベンダー (Ihv) のためのものです。
ms.assetid: 5CE619F4-E136-4F8F-8F90-F7F96DE4642E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0842652ef965ac39a694619d4640ec1648b88cc8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539014"
---
# <a name="camera-driver-bring-up-guide"></a>カメラのドライバー ガイドを表示します。

このトピックでは、赤外線 (IR) カメラの場合、顔認証を有効にする方法について説明し、相手先ブランド供給 (Oem) および独立系ハードウェア ベンダー (Ihv) が自分のデバイスでこの機能を提供するものです。

## <a name="frameserver"></a>FrameServer

次の図は、FrameServer を通じて新しいドライバー スタックでの顔認証のしくみを示しています。

![windows こんにちはおよび frameserver](images/windows-hello-device-model.png)

## <a name="face-authentication-ddis"></a>顔認証 Ddi

Windows 10 バージョン 1607 を Windows こんにちはをサポートするために使用できる新しい 2 つの顔認証 DDI コンストラクトは。

-   **KSPROPERTY\_CAMERACONTROL\_拡張\_FACEAUTH\_モード**

    このプロパティ ID は有効にして、次のフラグを使用して、ドライバーでの顔認証の構成を使用します。

    -   **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_無効になっています。**

    -   **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_MODE\_ALTERNATIVE\_FRAME\_ILLUMINATION**

    -   **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_バック グラウンド\_減算**

    このコントロールは、ビット フラグを使用して、顔の認証モードを設定する方法の詳細については、次を参照してください、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_FACEAUTH\_モード。** ](https://msdn.microsoft.com/library/windows/hardware/mt742028)トピック。

-   **MF\_CAPTURE\_METADATA\_FRAME\_ILLUMINATION**

    IR のカメラの場合は、このメタデータ属性では、フレームがアクティブな IR 照明を使用していることを指定します。 詳細については、次を参照してください。、**必須のメタデータ属性**テーブルに、[フォト キャプチャ フィードバック](standardized-extended-controls-.md#photo-capture-feedback-applied-device-settings)のセクション、[カメラ コントロールを拡張](standardized-extended-controls-.md)トピック。

## <a name="usb-camera-support"></a>USB カメラのサポート

赤外線デバイスでカメラの場合、顔認証を有効にするには、USB ビデオ クラス (UVC) 拡張機能の単位を DeviceMFT コンポーネントが正しく構成されているを提供する必要があります。

### <a name="configure-the-devicemft-component"></a>DeviceMFT コンポーネントを構成します。

開始点としてお使いのデバイスで顔認証をサポートしている DeviceMFT コンポーネントを構築することができますを使用する、 [sampledevicemft](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/sampledevicemft)サンプル、 [Windows ドライバー サンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリGitHub します。

ドライバーのサンプルを変更するには、ダウンロードして抽出[Windows ドライバーのサンプル-master.zip](https://github.com/Microsoft/Windows-driver-samples/archive/master.zip)、または、開発用コンピューターに Windows ドライバーのサンプル リポジトリを複製する git を使用します。 移動し、 **sampledevicemft**サンプル、 **avstream**ソース コードのフォルダーと、次のサンプルに変更を行います。

1.  DeviceMFT コンポーネントのソースの種類の情報を追加します。

2.  タグ DeviceMFT コンポーネントで照明フラグ

3.  次のセクションで作成 UVC 拡張ユニットとの通信に DeviceMFT コンポーネントで IKSControl を変換します。

### <a name="build-a-usb-video-class-uvc-extension-unit"></a>USB ビデオ クラス (UVC) 拡張機能ユニットを作成します。

デバイスの UVC 拡張ユニットをビルドする手順については、[単位の拡張機能サンプル コントロールを作成](building-the-extension-unit-sample-control.md)です。 このトピックでは、必要なプロジェクト ファイルを作成する方法について説明し、サンプル コードで、次のトピックへのリンクを提供します。

[UVC 拡張機能のユニットのインターフェイスのサンプル](sample-interface-for-uvc-extension-units.md)(が含まれています*Interface.idl*)

[サンプル拡張ユニット プラグイン DLL](sample-extension-unit-plug-in-dll.md) (が含まれています*Xuproxy.h*と*Xuproxy.cpp*)

[UVC 拡張機能の単位用のレジストリ エントリのサンプル](sample-registry-entry-for-uvc-extension-units.md)(が含まれています*Xusample.rgs*)

[サンプル アプリケーション UVC 拡張ユニット](sample-application-for-uvc-extension-units.md)(が含まれています*TestApp.cpp*)

[拡張機能単位にイベントを自動更新をサポートしています。](supporting-autoupdate-events-with-extension-units.md)

[サンプル拡張機能ユニット記述子](sample-extension-unit-descriptor.md)

[UVC INF ファイルを提供します。](providing-a-uvc-inf-file.md)

参照してください、[拡張ユニット プラグイン アーキテクチャ](extension-unit-plug-in-architecture.md)サンプル コードのモジュールの動作の詳細についてはトピック。

## <a name="inf-file-entries"></a>INF ファイルのエントリ


UVC デバイスを登録する**KSCATEGORY\_センサー\_カメラ**センサーのカメラの昇格フラグを指定する必要があります。

```INF
HKR,,SensorCameraMode,0x00010001,0x00000001
```

RGB ストリームがあるないため、このカメラ通常のカメラ アプリからを非表示には、ようスキップ列挙型のフラグを使用します。

```INF
HKR,,SkipCameraEnumeration,0x00010001,0x00000001
```

これにより、カメラから**KSCATEGORY\_ビデオ**、従来の列挙体を通常のカメラ アプリで列挙されてから、ブロックされます。

両方の**SkipCameraEnumeration**と**SensorCameraMode**でエントリを配置する必要があります、 **DDInstall.HW** INF ファイルのセクション。

## <a name="hlk-tests-for-kscategorysensorcamera-to-assist-driver-testing"></a>KSCATEGORY HLK テスト\_センサー\_ドライバーのテストを支援するためにカメラ


ハードウェア ロゴ キット (HLK) のテストは、IR および RGB の両方のカメラ モジュールに必要です。 このテストは、Windows こんにちは顔認証に使用される RGB と IR のカメラの基本的な機能を確認します。 RGB カメラの要件は HLK テスト スイートで既に指定されています。

これらは、IR カメラ モジュールを有効にするのに渡す必要があるテストです。

1.  KS センサー カテゴリのすべてのカメラを列挙します。

    -   IR のストリームをサポートするデバイスがセンサーの下にする必要がある\_カメラのカテゴリ。

    -   RGB のストリームをサポートするデバイスは、ビデオの下に移動して\_カメラのカテゴリ。

    -   IR および RGB のストリームをサポートする、1 つのカメラ デバイスに対してのみ両方 KSCAMERA カテゴリの下のデバイスを登録する必要があります。センサー\_カメラおよびビデオ\_カメラ。

2.  検索のストリームが、 **MF\_DEVICESTREAM\_属性\_FACEAUTH\_機能**属性が定義されています。

    -   ストリームが存在しない場合、 **MF\_DEVICESTREAM\_属性\_FACEAUTH\_機能**属性が定義されている場合、このテストをスキップします。

    -   複数のストリームがある場合、 **MF\_DEVICESTREAM\_属性\_FACEAUTH\_機能**属性が定義されている場合、1 つだけストリームする必要があります Windows こんにちは対応として、テストは失敗します。

    -   場合**MF\_DEVICESTREAM\_属性\_FRAMESOURCE\_型**されませんが設定されている IR をこのストリームのテストに失敗がこのストリームで RGB メディアの種類を指定できますできません。

    -   このストリームを選択し、メディアの種類が Windows こんにちは対応 (MJPG/L8/NV12) と解像度が 320 x 320 ピクセル以上のことを検証します。

        1.  顔認証プロファイルがサポートされている場合は、プロファイルのメディアの種類には、このストリームを検証します。

        2.  顔認証プロファイルがサポートされていない場合は、このストリームの既定のメディアの種類を検証します。

    -   顔認証 DDI 内のプロパティの 1 つに対するサポートを確認します。照らさ/未適用 illuminated またはアンビエント減算します。

    -   サポートされている 1 つに、KS プロパティを設定します。

    -   ストリーミングを開始します。

3.  実行時のプロパティを確認します。

    -   タイムスタンプの有効桁数 (メタ データでの顔認証のプレビューのテスト) を確認します。

    -   起動がより小さい 500 ミリ秒 (メタ データでの顔認証のプレビューのテスト) であることを確認します。

    -   次のパラメーターを持つ最小のフレーム レートでのストリーミングを確認します。明るいと 15 15 FPS アンビエント FPS アンビエントまたは 15 FPS 減算、メディア、320 x 320 ピクセル以上の解像度は、サンプルに L8/NV12、正のストライドを入力します。

        1.  明るいプロパティが有効になっている場合は、フレーム (15 FPS で点灯/非-照らさペア フレーム) のメタデータを確認します。

        2.  減算のアンビエント プロパティが有効になっている場合は、フレーム (15 fps アンビエント フレーム) でメタデータを確認します。

4.  [ストリーミング停止]

5.  Unset KS コントロール

6.  RGB + IR の同時実行制御: カメラ プロファイルで定義されている場合は、テスト

上に示した HLK テストが渡されないと、Microsoft は、OEM に署名されたドライバーを発行しませんし、Windows こんにちはは動作しません。

## <a name="related-topics"></a>関連トピック

[MediaCapture を使った写真とビデオのキャプチャ](https://msdn.microsoft.com/windows/uwp/audio-video-camera/capture-photos-and-video-with-mediacapture)  

[Windows.Media.Capture 名前空間](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.aspx)  
