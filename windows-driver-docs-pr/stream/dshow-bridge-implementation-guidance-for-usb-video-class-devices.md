---
title: UVC デバイス DShow ブリッジ実装ガイダンス
description: UVC デバイス DShow ブリッジ実装ガイダンスを提供します。
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ccaa5be9ac2ff404335aaa5dc2f3a31caf75464
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549159"
---
# <a name="dshow-bridge-implementation-guidance-for-uvc-devices"></a>UVC デバイス DShow ブリッジ実装ガイダンス

このトピックでは、カメラと USB ビデオ クラス (UVC) 仕様に準拠しているデバイス DShow ブリッジを構成するための実装のガイダンスを提供します。 プラットフォームは[Microsoft OS ディスクリプター](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors) DShow ブリッジを構成する標準の USB バスから。 拡張プロパティの OS ディスクリプター USB の標準的な記述子の拡張機能は、USB デバイスでは標準の仕様を有効になっていない Windows の特定のデバイス プロパティを返すために使用します。

## <a name="overview"></a>概要

DirectShow とマルチ メディア Foundation と呼ばれる最新のフレームワークと呼ばれる従来のフレームワークのスタックの Microsoft のカメラ キャプチャのスタックで構成されます。 Ihv と Oem がパイプラインの両方を満たすために、デバイスのコンポーネントを作成する必要があります。

DShow ブリッジは、メディア ファンデーションのプラットフォームで DShow パイプラインをブリッジする目的で記述されています。 これにより、Ihv と Oem は、アプリケーションを実行できます MediaFoundation DShow と Windows のバージョン 1607 以降のドライバーを記述できますよう、ユニバーサル ドライバーの場合は true。 DShow ブリッジ選択では有効になっている、DShow アプリケーションとアプリケーションの共有を共有できますカメラと同じハードウェアに同時に。

Ihv と Oem DShow パイプラインを制御するポリシーからの除外を必要があります。 パートナーは、OS ディスクリプターを使用して、次の機能を有効にできます。

-   **オプトイン DShow ブリッジの内外で**:デバイスできますのオプトイン、オプトアウト、ブリッジ パイプラインにより、ニーズに適しています。 最新のパイプラインはについてさらに詳しく記載されており、複数のリリースで、OS に追加された機能を利用します。 従来のパイプラインでは、メンテナンス モードになることよりも遅れています。

-   **フレームのサーバーで圧縮解除を MJPEG**:フレームのサーバーは、カメラのデバイスを仮想化サービスです。 これにより、複数のクライアント間で共有するデバイスからのピンができます。 最適化されたメディア ファンデーション圧縮解除プログラムのアーキテクチャでは、フレームのサーバーでの MJPEG をデコードするのにこの機能を使用できます。 翻訳の非圧縮メディア formats(YUY2) は複数のアプリケーションに提供します。 ストリームは複数の可能なクライアントに 1 回圧縮解除のみ。 これにより、アプリケーションのパフォーマンスが向上します。 次の図は、カメラ キャプチャのパイプラインを示しています。

![カメラ キャプチャ パイプライン](images/camera-capture-pipeline.png)

Oem および ihv 向けのパッケージ化、USB カメラ デバイスは、その UVC ドライバーの INF ファイルの変更を使用しなくても DShow ブリッジを構成するのに、USB バスの標準の拡張プロパティの OS 機能記述子の仕様を使用できます。

デバイスを USB デバイスのレジストリのプロパティを定義または複合デバイス OS ディスクリプターを許可します。

USB の OS ディスクリプターを使用して DShow ブリッジを構成するには、ホスト ソフトウェアは、USB デバイスのインターフェイスごとに次のレジストリ キーを作成する必要があります。

> HKLM\\システム\\CurrentControlSet\\Enum\\USB\\&lt;*DeviceVID & PID* &gt; \\ &lt;*DeviceInstance*&gt;\\デバイス パラメーター
>
> DWORD:**EnableDshowRedirection**

**EnableDshowRedirection**レジストリ値がビットのマスク値によって次の表の説明に従って、DShow ブリッジを構成するために使用できます。

| ビット マスク | 説明 | 注釈 |
|---|---|---|
| 0x00000001 | DShow ブリッジを選択します。 | 0 – オプト アウト<br>1 – オプトイン  |
| 0x00000002 | フレームのサーバーでの MJPEG デコードを有効にする (下記の注を参照してください) | 0 – 圧縮 MJPEG メディア公開される型 (操作なし)<br>1 – MJPEG (YUY2) から翻訳済みの圧縮されていないメディアの種類を公開します。 |

> [!NOTE]
> 種類はアプリケーションに提供し、1 回のみ圧縮されていないメディアをデコード MJPEG を有効にします。

## <a name="example-layouts"></a>レイアウトの例

例は、次の仕様については後述します。

-   Microsoft OS ディスクリプター仕様 1.0 の拡張

-   Microsoft OS 2.0 記述子の仕様

### <a name="microsoft-os-extended-property-descriptors-specification-version-10"></a>Microsoft OS の拡張プロパティ記述子の仕様バージョン 1.0

拡張プロパティの OS の記述子が 2 つのコンポーネント

-   固定長のヘッダー セクション

-   1 つまたは複数可変長のカスタム プロパティのセクションでは、ヘッダー セクションの続き

#### <a name="header-section"></a>ヘッダー セクション

ヘッダー セクションには、長さの合計とバージョン番号を含む、全体の拡張プロパティの記述子がについて説明します。

| Offset | フィールド      | サイズ (バイト) | Value      | 説明                     |
|--------|------------|--------------|------------|---------------------------------|
| 0      | dwLength   | 4            | 0x0000004c | 10 進数の 76                      |
| 4      | bcdVersion | 2            | 0x0100     | バージョン 1.0                     |
| 6      | wIndex     | 2            | 0x005      | 拡張プロパティ記述子の OS |
| 8      | wCount     | 2            | 0x0001     | 1 つのカスタム プロパティ             |

#### <a name="custom-property-section"></a>カスタム プロパティ」セクション

USB HID デバイスは、作成する 1 つのカスタム プロパティ セクションに OS の記述子がプロパティの拡張、 **EnableDshowRedirection** DWORD レジストリ キー。

| Offset | フィールド | サイズ (バイト) | Value |
|--------|----------------------|---------|-------------------------------------------|
| 0      | ない dwSize               | 4       | 0x00000042 (このプロパティの 66 のバイト数)   |
| 4      | dwPropertyDataType   | 4       | 0x00000004 (REG\_DWORD\_リトル\_ENDIAN)   |
| 8      | wPropertyNameLength  | 2       | 0x0030                                    |
| 10     | bPropertyName        | 48      | **EnableDshowRedirection** (Unicode 文字列) |
| 58     | dwPropertyDataLength | 4       | 0x00000004 (Sizeof(DWORD))                |
| 62     | bPropertyData        | 4       | 0x00000001 (DWORD データ)                   |

### <a name="microsoft-os-20-descriptors-specification"></a>Microsoft OS 2.0 記述子の仕様

この例は、Microsoft 2.0 記述子のセットを使用しての単一の DWORD レジストリ値を提供する方法を示します**EnableDshowRedirection** Windows バージョンに適用します。

#### <a name="custom-property-section"></a>カスタム プロパティ」セクション

| Offset | フィールド | サイズ (バイト) | Value |
|--------|----------------------|----------|-----------------------------------------|
| 0      | wLength              | 2        | この記述子のバイト長      |
| 4      | wDescriptorType      | 2        | 0x00000004 (REG\_DWORD\_リトル\_ENDIAN) |
| 8      | wPropertyDataType    | 2        | 0x0030                                  |
|        | wPropertyNameLength  | 2        |                                         |
| 10     | PropertyName         | 変数 | プロパティ名の長さ             |
| 58     | dwPropertyDataLength | 2        | プロパティ データの長さ                 |
| 62     | PropertyData         | 変数 | プロパティのデータ                           |


```cpp
UCHAR Example2\_MSOS20DescriptorSetForFutureWindows\[0x48\] =
{
    //
    // Microsoft OS 2.0 Descriptor Set Header
    //
    0x0A, 0x00,                 // wLength - 12 bytes
    0x00, 0x00,                 // MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x0?, 0x06,     // dwWindowsVersion – 0x06030000 for future Windows version
    0x4A, 0x00,                 // wTotalLength – 72 bytes

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x3E, 0x00,                 // wLength - 62 bytes
    0x04, 0x00,                 // wDescriptorType – 5 for Registry Property
    0x04, 0x00,                 // wPropertyDataType - 4 for REG_DWORD
    0x30, 0x00,                 // wPropertyNameLength – 48 bytes
    0x45, 0x00, 0x6E, 0x00,     // Property Name - "EnableDshowRedirection"
    0x61, 0x00, 0x62, 0x00,
    0x6C, 0x00, 0x65, 0x00,
    0x44, 0x00, 0x73, 0x00,
    0x68, 0x00, 0x6F, 0x00,
    0x77, 0x00, 0x52, 0x00,
    0x65, 0x00, 0x64, 0x00,
    0x69, 0x00, 0x72, 0x00,
    0x65, 0x00, 0x63, 0x00,
    0x74, 0x00, 0x69, 0x00,
    0x6F, 0x00, 0x6E, 0x00,
    0x00, 0x00, 0x00, 0x00,
    0x04, 0x00,                 // wPropertyDataLength – 4 bytes
    0x00, 0x00, 0x00, 0x00      // PropertyData – 0x00000003 (see note below)
}
```

> [!NOTE]
> 0x00000003: - DShow ブリッジが有効になっているし、MJPEG が FrameServer、たとえば、ソースでデコードされます

### <a name="resources"></a>参考資料

[USB デバイスの Microsoft OS ディスクリプター](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)

[一般的な親の USB ドライバー (Usbccgp.sys)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-common-class-generic-parent-driver)

[USB 仕様](http://www.usb.org/developers/docs)
