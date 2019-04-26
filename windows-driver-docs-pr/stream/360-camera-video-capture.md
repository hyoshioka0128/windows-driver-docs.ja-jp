---
title: 360 カメラのビデオ キャプチャ
description: 360 のカメラのビデオ キャプチャについてを説明します。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: d8bf634a005b626a64df5a3d394b10bd293199ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357278"
---
# <a name="360-camera-video-capture"></a>360 カメラのビデオ キャプチャ

Windows 10、バージョン 1803 360 のカメラのプレビュー、キャプチャ、および既存の MediaCapture Api を使用したレコードのサポートを提供します。 これにより、検出および 360 キャプチャ エクスペリエンスを提供するためも 360 のカメラのビデオ ストリームを処理するアプリを有効にする球のフレームのソース (たとえば、正距円筒図法フレーム) を公開するプラットフォームです。

> [!NOTE]
> [Cam360](https://github.com/Microsoft/Windows-Camera/tree/master/Tools/Cam360)サンプルを GitHub で入手できるプレビュー、ビデオ録画は、Windows 上の 360 カメラで写真キャプチャ シナリオをサポートする方法を示します。

## <a name="overview"></a>概要

各ストリームの球の形式を公開する DMFT プラグイン (またはカスタム UVC ドライバーがない) とメディアの種類をプロセス カメラ ドライバーの出力と同様に、球のフレームを出力し、正距円筒図法フレームを提供する 360 カメラ IHV を提供できます。適切な属性とメタデータ。

ほとんどの 360 カメラ バックツー バックの 2 つのセンサーが付属し、一部重複してに 360 FoV を説明します。 IHV は、通常されます unwarp し、し、正距円筒図法フレームを出力する DMFT 内のフレームをつなぎ合わせる fisheye の 2 つのセンサー、同期的にキャプチャします。

これらの正距円筒図法フレームを取得し、360、ビデオのプレビュー エクスペリエンスをパン、球に射影するには、MediaCapture および MediaPlayer Api 経由でのアプリで使用されます。 DMFT 経由で提供されるメタデータは、MP4 形式、ビデオを記録して、暗黙的に、適切な標準化されたメタデータを囲み、プラットフォームによって利用されます。 360 再生ビデオ プレーヤー内などから再生するとき、**映画とテレビ**Windows 10、結果の記録ビデオ アプリ エクスペリエンスをパン、予想される球形ビューが提供されます。

360 のカメラの使用法:

-   360 のフレームをプレビューするには、アプリケーションが明示的に、XAML を使用する必要は[MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement)プレビューを表示します。 アプリケーションにも、パンの UI との対話を明示的に処理するために必要なを使用して、 [MediaPlaybackSphericalVideoProjetion.ViewOrientation](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksphericalvideoprojection)四元数。

-   360 ビデオ レコードには、キャプチャ アプリケーションを使用している場合に 360 コンテンツに対して明示的に構成する必要ありません[MediaCapture WinRT Api](https://docs.microsoft.com/windows/uwp/audio-video-camera/basic-photo-video-and-audio-capture-with-mediacapture)、球の形式が暗黙的にレコードのシンクに渡すし、ファイルに書き込まれますヘッダー。

-   アプリケーションは 360 の写真をキャプチャを明示的に使用可能なを使用して、球の形式を指定する適切な標準化されたメタデータを追加する必要があります[WIC WinRT Api](https://docs.microsoft.com/windows/uwp/audio-video-camera/image-metadata)します。

360 カメラ投影ビューでのストリームを実装し、パンと傾き/ズーム コントロールを公開する IHV の責任です。

アプリケーションが実装して、プロジェクションを生成する効果を挿入します。 効果は、正距円筒図法フレームを識別するために、メディアの種類の属性を活用できます。


## <a name="architecture"></a>Architecture


次の図は、360 カメラ スタックに DMFT の関係を示しています。

![360 カメラ スタック](images/360-camera-stack.png)

360 カメラ Ihv が定義されている形式の球のフレームを提供する 360 のビデオ ストリームを公開する DMFT が発行されます。 DMFT はインストールされているし、INF ファイルの例では、「ドライバーの拡張機能を使用して特定カメラに関連付けられていることができます。INF 以下。

合成および正距円筒図法フレームへの変換は、カメラのハードウェアや、DMFT 内にかかります。 GPU などのハードウェア リソースを効率的に処理の使用を許可される、この目的で、DMFT を活用することをお勧めが必要があります。 DMFT は、次のストリームを設定してもとメディア タイプのプロパティ (次の表に示すように) 360 のコンテンツのストリームとして識別します。

Stiching のカメラのハードウェアで実行して、IHV が決定したら、場合でも、DMFT がストリームの設定に必須の要件とメディアの種類属性のプロパティを 360 ビデオ。

次の表は、球のフレームのソースを識別するために必要なストリームの属性を示しています。

<table>
<thead>
<tr class="header">
<th>プロパティの名前と GUID</th>
<th>
<p>値</p>
</th>
<th>
<p>属性</p>
</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="_Hlk495398335" class="anchor"><span id="_Hlk495398374" class="anchor"></span></span>MF_SD_VIDEO_SPHERICAL<br />
{A51DA449-3FDC-478C-BCB5-30BE76595F55}</td>
<td>
<p>TRUE (1)</p>
</td>
<td>
<p>Stream およびメディアの種類</p>
</td>
</tr>
<tr class="even">
<td><span id="_Hlk495398361" class="anchor"><span id="_Hlk495398391" class="anchor"></span></span>MF_SD_VIDEO_SPHERICAL_FORMAT<br />
{4A8FC407-6EA1-46C8-B567-6971D4A139C3}</td>
<td>
<p>MFVideoSphericalFormat_Equirectangular (1)</p>
</td>
<td>
<p>MediaType</p>
</td>
</tr>
</tbody>
</table>

一部として、上記のプロパティが既に存在する**mfidl.idl**します。

MF として設定する属性を持つ別の unstitched の 360 ビデオ メディアの種類を公開するオプションになっている IHV も合成を実行するカスタム アプリを利用する\_SD\_ビデオ\_球面\_を書式設定MFVideoSphericalFormat\_Unsupported(0) します。 カスタム アプリケーションは、未処理のストリームを選択し、それを処理する必要があります。

## <a name="platform-guidance"></a>プラットフォームのガイダンス

プラットフォームは、WinRT レイヤーを介してアプリケーションにすべてのストリーム属性を既に公開[MediaFrameSourceInfo.Properties](https://docs.microsoft.com/uwp/api/windows.media.capture.frames.mediaframesourceinfo)、MF を検索できる\_SD\_ビデオ\_球面上記の表で定義されている GUID。 ただし、プラットフォームの要素の球の構成のほとんどを暗黙的に管理プラットフォームでされます。 プロパティは、アプリケーション開発者、たとえば、挿入またはビデオの sphericalness によって削除する必要があるユーザー設定の効果を実装する必要がある追加の機能に対してのみ、アプリケーションで照会できます。

プラットフォームをバイパス顔検出、シーンのアナライザー、およびビデオ安定化などの受信トレイの効果 (追加) 場合、球のフレームのソースを示す stream 属性プロパティの値を検出した場合にします。

プラットフォームでは、暗黙的に 360 ビデオ プロジェクション エクスペリエンスのプレビューに接続されているメディア プレーヤーの要素を構成します。 アプリケーションは、適切なプラットフォーム プレビュー用のメディア プレーヤーの要素を選択する Api を呼び出します。 アプリケーションは、media player の投影の方向と角度を制御する UI を実装するためにもあります。 場合は、アプリケーションでは、プレビューのキャプチャの要素を選択、球の投影のエクスペリエンスを活用することはできません。

プラットフォームでは、360 ビデオを録画する MP4 シンクも暗黙的に構成します (を渡す、適切なビデオ球形式と関連メタデータあればでき、サポートされている) に使用するストリームには、表 1 – で定義されたプロパティが含まれている場合にストリームの属性が必要球のフレームのソースを識別します。

| **MF\_SD\_ビデオ\_球面\_形式の値 (MFVideoSphericalFormat)**  | **SphericalVideoFrameFormat 値** | **解釈**  |
|---|---|---|
| メディアの種類の属性にあるプロパティの値 MFVideoSphericalFormat\_正距円筒図法 (1) | SphericalVideoFrameFormat します。 正距円筒図法 | ストリームは、MediaPlayer の要素を使用して表示可能な正距円筒図法形式内の球のフレームを提供します。 |
| メディアの種類の属性にあるプロパティの値 MFVideoSphericalFormat\_サポートされていません (0)     | SphericalVideoFrameFormat します。 サポートされません     | ストリームは、MediaPlayer 要素と互換性がない別の形式で球のフレームを提供します。 (サポート可能性があるカスタム書式指定で一部のアプリ) |
| プロパティが存在しないメディアの種類の属性から。                                                   | SphericalVideoFrameFormat します。 なし            | ストリームは、通常の非球フレームを提供します。 (非 360) |

## <a name="application-guidance"></a>アプリケーションのガイダンス

アプリケーションを使用できます、 [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) 360 ビデオ球プロジェクション エクスペリエンスを活用する、XAML コントロール。

場合、MF\_SD\_ビデオ\_球面\_形式プロパティは、メディアの種類に存在し、MFVideoSphericalFormat に設定されている\_正距円筒図法、フレームは、球を予定しているし、することができます使用して適切に表示される、 [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) XAML コントロール。 アプリケーションでは、media player の再生セッション (objMediaPlayer.PlaybackSession.SphericalVideoProjection) から取得した MediaPlaybackSphericalVideoProjection のプロパティをチェックして、media player によって検出された球の形式を照会できます。 アプリケーションを設定する必要があります、 **isEnabled**プロパティを**TRUE**球の投影を開始します。

アプリケーション独自のカスタム球プロジェクション コンポーネントに実装するかどうかは、経由でフレームのソースを照会できること、 [MediaFrameSourceInfo.Properties](https://docs.microsoft.com/uwp/api/windows.media.capture.frames.mediaframesourceinfo)の表で説明するよう球ストリーム レベル ビデオのプロパティ上。 ただし、プラットフォームのすべての要素構成などの media player のプレビューと、レコードのシンクはストリームと mediatype attribuites でカメラ DMFT によって公開される球形のビデオのプロパティの検出時に、プラットフォームによって暗黙的に構成されます。



## <a name="inf-file-example-to-publish-a-dmft"></a>.INF ファイルの例を DMFT を発行するには

```INF
;=================================================================================
; Microsoft Sample Extension INF for USB Camera SampleDeviceMFT installation
; Copyright (C) Microsoft Corporation. All rights reserved.
;=================================================================================

[Version]
Signature="$WINDOWS NT$"
Class=Extension
ClassGUID={e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider=%CONTOSO%
ExtensionId = {E4FE3A00-68CF-45A3-83C8-8347A6A38069} ; replace with your own GUID
CatalogFile.NT = SampleExtensionInfForDmftInstallation.cat
DriverVer=08/28/2017,10.0.17000.2000

[Manufacturer]
%CONTOSO% = ContosoSampleDeviceMFT,ntamd64

[ContosoSampleDeviceMFT.ntamd64]
%ContosoCamera.DeviceDesc% = ContosoSampleDeviceMFT_Install, usb\vid_xxxx&pid_xxxx&mi_xx  ; replace with your camera device VID PID

[ContosoSampleDeviceMFT_Install]
CopyFiles=ContosoSampleDeviceMFTCopy
AddReg=ContosoSampleDeviceMFT_COM.AddReg

;-----------------------------------------------------------------------------------
;
; Registers Device MFT COM object
;
;-----------------------------------------------------------------------------------

[ContosoSampleDeviceMFT_COM.AddReg]
HKCR,CLSID\%SampleDeviceMFT.CLSID%,,,%SampleDeviceMFT.FriendlyName%
HKCR,CLSID\%SampleDeviceMFT.CLSID%InProcServer32\,,,%%SystemRoot%%\ContosoSampleDeviceMFT.dll
HKCR,CLSID\%SampleDeviceMFT.CLSID%InProcServer32\,ThreadingModel,,"Both"

[ContosoSampleDeviceMFT_Install.Interfaces]
AddInterface=%KSCATEGORY_VIDEO_CAMERA%,,ContosoSampleDeviceMFT.Interfaces,

[ContosoSampleDeviceMFT.Interfaces]
AddReg=ContosoSampleDeviceMFT.AddReg

;-----------------------------------------------------------------------------------
;
; Add DeviceMFT CLSID to device interface instance registry key
;
;-----------------------------------------------------------------------------------

[ContosoSampleDeviceMFT.AddReg]
HKR,,CameraDeviceMftClsid,,%SampleDeviceMFT.CLSID%

;-----------------------------------------------------------------------------------
;
; File copy sections
;
;-----------------------------------------------------------------------------------

[SourceDisksFiles]
ContosoSampleDeviceMFT.dll=1

[SourceDisksNames]
1 = %MediaDescription%

[DestinationDirs]
ContosoSampleDeviceMFTCopy=11
DefaultDestDir = 11

[ContosoSampleDeviceMFTCopy]
ContosoSampleDeviceMFT.dll

[Strings]
CONTOSO = "Contoso Inc."
ContosoCamera.DeviceDesc = "Contoso Camera Extension"
MediaDescription="Contoso Camera Sample Device MFT Installation Media"
SampleDeviceMFT.CLSID = "{zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz}" ; replace with your Device MFT COM object's CoClass ID
SampleDeviceMFT.FriendlyName = "Contoso Camera Device MFT"
KSCATEGORY_VIDEO_CAMERA="{E5323777-F976-4f5b-9B55-B94699C46E44}"
```

## <a name="example-frame-flow-with-a-uvc-device"></a>UVC デバイスでフレーム フローの例

(USBVdeo.sys から結合されたフレーム unstitched 1):

![Unstitched 結合されたフレーム](images/unstitched-combined.png)

(2) フレーム ワープされていない、合成し、プレビュー、保存するビデオ シンクまたは写真シンクへのアプリケーションのレンダリング要素に送られます DMFT 内で正距円筒図法に変換するファイル。

![フレーム ワープされていない、合成および変換](images/unwarped-stitched-transformed.png)

(ビューポートの回転のパンとビューのフィールドの相互作用を提供できるだけでなく、球のプロジェクションを適用する UI 要素を使用して、アプリケーション内で 3) レンダリング ビューポートは:

![ビューポートの表示](images/rendered-viewport.png)


