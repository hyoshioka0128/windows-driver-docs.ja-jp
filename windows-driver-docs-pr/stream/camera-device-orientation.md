---
title: カメラの向きのドライバーサポート
description: デバイスでカメラの向きを明示的に指定する方法について説明します。
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2c6fbea2e686830418ae7c8bfc5567ab860e2f69
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565772"
---
# <a name="driver-support-for-camera-orientation"></a>カメラの向きのドライバーサポート

> [!IMPORTANT]
> このトピックの後半で説明する自動修正方式は、カメラセンサーの非参照指向マウントに*推奨*されるソリューションです。 これは、カメラのフィードを使用するために既に作成されているほとんどのアプリケーションが、ローテーション情報を確認したり、修正したりすることがわからないため、アプリの互換性を確保するためです。 以下の自動修正セクションの情報をよく確認してください。

コンピューティングデバイスがさまざまな形式で導入されているため、物理的な制約の一部ではカメラセンサーが従来の向きではなくマウントされます。 このため、生成されたビデオを適切にレンダリングまたは記録できるように、OS とアプリケーションを正しく記述し、センサーがどのようにマウントされるかを適切に説明する必要があります。

Windows 10 バージョン1607以降では、カメラが[最小ハードウェア要件](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)に従ってマウントされているかどうかに関係なく、カメラの向きを明示的に指定するためにすべてのカメラドライバーが必要になります。
具体的には、カメラドライバーは、キャプチャデバイスインターフェイスに関連付けられて\_いる ACPI pld 構造体に新しく導入されたフィールドであるローテーションを設定する必要があります。

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
    UINT32 Rotation:4;      // 0 – Rotate by 0° clockwise
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

カメラの場合、 ACPI \_pld 構造の回転フィールドは、角度 (0 °の場合は ' 0 '、90°の場合は ' 2 '、180の場合は ' 4 '、270の場合は ' 6 ') を指定します。キャプチャされたフレームは、画面を基準にして回転します。

**[回転]** フィールドの値に基づいて、キャプチャされたフレームを正しく表示するために、必要に応じて追加の回転を実行できます。

## <a name="rotation-values"></a>回転値

カメラとディスプレイが同じハウジング (または*エンクロージャ*/の*大文字と小文字*) を共有しているデバイスについては、これらの周辺機器を別の表面にマウントし、それぞれを固定した状態で回転させることができます。それぞれの面で。 そのため、アプリケーションには、キャプチャされたフレームを正しい向きでレンダリングサーフェイスに転置できるように、2つの周辺機器間の空間リレーションシップを記述するメカニズムが必要です。

この問題を解決する方法の1つとし\_て、既に*surface*と*回転角度*の概念が定義されている ACPI pld 構造体を使用する方法があります。 たとえば、 \_pld 構造体には既に、周辺機器が存在するサーフェイスを指定する*panel*フィールドがあります。

![ACPI PLD パネルフィールド](images/acpi-pld-panel-field.png)

*ACPI \_pld Panel フィールドの定義 (Rev. 5.0 a)*

次の2つの図は、各パネルの定義を視覚的に示しています。

![パネル定義-デスクトップ](images/panel-definitions-desktop.png)

*デスクトップ Pc とほとんどのデバイスのパネル定義*

![パネル定義-たたみ込みデバイス](images/panel-definitions-foldable-devices.png)

*たたみ込みデバイスのパネル定義*

実際、ACPI の "panel" の概念は、次のような Windows によって既に採用されています。

- カメラデバイスインターフェイスは、キャプチャデバイスが\_固定された場所に静的にマウントされている場合に、それに応じてパネルフィールドが設定される pld 構造に関連付けられています。
- アプリケーションでは、 [EnclosureLocation](https://msdn.microsoft.com/en-us/library/windows/apps/windows.devices.enumeration.enclosurelocation.panel.aspx)プロパティを呼び出すことによって、キャプチャデバイスが存在するパネルを取得できます。

ACPI \_pld 構造体には、次のように定義されている回転フィールドもあります。

![ACPI \_pld の回転フィールドの定義](./images/acpi-pld-rotation-field.png)

*ACPI \_pld 回転フィールドの定義 (Rev 5.0 a)*

上記の定義を "その他" として使用する代わりに、あいまいさを避けるためにさらに改良します。

- カメラの場合、ACPI \_pld 構造の回転フィールドは、角度 (0 °の場合は ' 0 '、90°の場合は ' 2 '、180の場合は ' 4 '、270の場合は ' 6 ') を指定します。キャプチャされたフレームは、画面を基準にして回転します。

## <a name="landscape-primary-vs-portrait-primary"></a>横方向のプライマリと縦方向のプライマリ

Windows では、**横**方向または**縦**方向のどちらかを返すプロパティ[DisplayInformation](https://msdn.microsoft.com/en-us/library/windows/apps/windows.graphics.display.displayinformation.nativeorientation.aspx)を呼び出すことによって、ネイティブの表示方向に対してクエリを実行できます。

![ネイティブの向きのスキャンパターンを表示する](./images/native-scanning-pattern.png)

値がどのように返されるかに関係なく、論理ディスプレイのスキャンパターンは、左から右へ移動する画面の左上隅から開始されます (図5を参照)。 既定の物理的な向きが明示されていないデバイスについては、このプロパティは、ACPI*上*のパネルの場所を意味するだけでなく、カメラの出力バッファーとレンダリングサーフェイスの間の空間リレーションシップも提供します。

カメラとは異なり、"データ**指向**" プロパティは ACPI に基づいていないため、 \_pld 構造はありません。 これは、ディスプレイがデバイスに静的にマウントされている場合でも当てはまります。

## <a name="offset-mounting"></a>オフセットマウント

アプリケーションの互換性を維持するために、センサーを0°以外のオフセットでマウントしないようにすることを強くお勧めします。 既存のアプリとレガシアプリの多くでは、ACPI の PLD テーブルを探すことはできません。また、0でない角度オフセットの修正も試行されません。 そのため、このようなアプリでは、結果として得られるビデオが正しくレンダリングされません。

前述のように、IHV/Oem がセンサーを0度でマウントできない場合は、次の対策手順を優先順位でお勧めします。

1. カメラドライバー内の0度以外の向きを自動修正します (AV ストリームミニポートドライバーを使用したカーネルモード、またはデバイス MFT や MFT0 などのプラグインを使用してユーザーモードで)。結果の出力フレームは、0度の向きになります。
2. カメラのパイプラインがキャプチャされたイメージを修正できるように、FSSensorOrientation タグを使用して0度以外の方向を宣言します。
3. 上記の説明に従って、ACPI の PLD テーブルで0度以外の方向を宣言します。

### <a name="compressedencoded-media-types"></a>圧縮/エンコードされたメディアの種類

圧縮またはエンコードされたメディアの種類 (MJPG、JPEG、H264、HEVC など) の場合は、パイプラインを正しく使用できません。 このため、FSSensorOrientation が0以外の値に設定されている場合、圧縮またはエンコードされたメディアの種類はフィルターで除外されます。

MJPG メディアタイプ (UVC カメラなど) の場合、フレームサーバーパイプラインは、自動デコードされたメディアの種類 (NV12 または YUY2 ベースのアプリケーションの場合は YUY2) を提供します。 自動デコードおよび修正されたメディアの種類が表示されますが、元の MJPG 形式は表示されません。

> [!メモ!]圧縮またはエンコードされたメディアの種類をアプリケーションに公開する必要がある場合、IHV/Odm は FSSensorOrientation の修正を利用することはできません。 代わりに、カメラドライバー (AV ストリームドライバーを介してカーネルモードにするか、DMFT/MFT0 を使用してユーザーモードで) で修正を行う必要があります。

### <a name="auto-correct-via-av-stream-miniportdevice-mftmft0"></a>AV ストリームミニポート/デバイス MFT/MFT0 を使用して自動修正

センサーを0度オフセットでマウントできない場合は、推奨されるシナリオとして、AV ストリームミニポートドライバー (または、DMFT または MFT0 のいずれかの形式のユーザーモードプラグイン) で、結果として得られたフレームを修正して、0度でパイプラインに公開することを*お勧め*します。位置のオフセット。

AV ストリームのミニポートまたはデバイスの MFT/MFT0 プラグインからビデオフレームを修正する場合、結果として得られるメディアの種類の宣言は、修正されたフレームに基づいている必要があります。 センサーが90度のオフセットでマウントされ、結果として得られるビデオはセンサーからの9:16 の縦横比ですが、修正されたビデオは16:9 であるため、メディアの種類は16:9 の縦横比を宣言する必要があります。

これには、結果として得られる stride 情報が含まれます。 このことが必要なのは、修正を行うコンポーネントが IHV/OEM によって制御されており、カメラのパイプラインが、修正された後を除き、ビデオフレームを表示できない場合です。

ユーザーモードで修正を実行し、パイプラインとユーザーモードプラグイン間の API コントラクトを従う必要があることを強くお勧めします。 具体的には、dmft または MFT0 のいずれかを使用しているときに、imfdevicetransform::P roて message または imftransform::P\_roが\_、\_MFT メッセージ\_セットの D3D マネージャーメッセージを使用して呼び出された場合、ユーザーモードになります。プラグインは、次のガイドラインに従う必要があります。

- D3D マネージャーが指定されていない場合 (メッセージの ulParam が0の場合)、ユーザーモードプラグインは、ローテーションの修正を処理する GPU 操作を呼び出さないようにする必要があります。 また、結果として得られるフレームは、システムメモリ内に提供される必要があります。
- D3D マネージャーが提供されている場合 (メッセージの ulParam が DXGI マネージャーの IUnknown である場合) は、その DXGI マネージャーを使用して回転を修正する必要があり、結果のフレームは GPU メモリである必要があります。
- ユーザーモードプラグインは、実行時に D3D マネージャーメッセージも処理する必要があります。 MFT\_メッセージ\_セット\_D3Dマネージャーメッセージが発行されたときに、プラグインによって生成される次のフレームは、要求されたメモリの種類(たとえば、DXGIマネージャーが提供された場合はGPU、CPU以外)に対応する必要があります。\_
- AV ストリームドライバー (またはユーザーモードプラグイン) がローテーションの修正を処理するときは、ACPI の PLD 構造体の回転フィールドを0に設定する必要があります。

> [!NOTE]
> 自動修正を使用する場合、oem および ihv は、pld \_**回転**フィールドを使用してセンサーの実際の向きをアドバタイズすることはできません。 この場合、 **[回転]** フィールドは修正後の向きを示す必要があります。0度。

## <a name="declare-via-fssensororientation"></a>FSSensorOrientation を使用した宣言

```INF
; Defines the sensor mounting orientation offset angle in
; degrees clockwise.
FSSensorOrientation: REG_DWORD: 90, 180, 270
```

FSSensorOrientation レジストリタグを介してセンサーの0度以外の方向を宣言することで、カメラのパイプラインは、キャプチャされたフレームを修正してからアプリケーションに提示することができます。

パイプラインは、ユースケースとアプリの要求/シナリオに基づいて GPU または CPU リソースを活用することで、ローテーションロジックを最適化します。

### <a name="acpi-pld-rotation"></a>ACPI PLD ローテーション

ACPI PLD 構造体の回転フィールドは0である必要があります。 これは、PLD 情報を使用してフレームを修正する可能性のあるアプリケーションの混乱を避けるためです。

### <a name="media-type-information"></a>メディアの種類の情報

ドライバーによって提示されるメディアの種類は、修正されていないメディアの種類である必要があります。 FSSensorOrientation エントリを使用して、0度オフセット以外のカメラパイプラインに通知する場合、センサーによって示されるメディアの種類の情報は、修正されていないメディアの種類である必要があります。 たとえば、センサーが90°時計回りのオフセットでマウントされている場合、16:9 の縦横比ではなく、最終的なビデオは9:16 で、9:16 の縦横比のメディアの種類をカメラのパイプラインに表示する必要があります。

これは、パイプラインがカウンターローテーションプロセスを正しく構成できるようにするために必要です。パイプラインには、アプリケーションの入力メディアの種類と必要な出力メディアの種類が必要です。

これには、stride 情報が含まれます。 メディアの種類が修正されていない場合は、stride 情報をカメラパイプラインに提示する必要があります。

### <a name="registry-subkey"></a>レジストリ サブキー

FSSensorOrientation レジストリエントリは、デバイスインターフェイスノードに発行する必要があります。 カメラドライバーの INF の AddInterface ディレクティブ宣言中に、これを AddReg ディレクティブとして宣言することをお勧めします。

Fssensororientation に表示されるデータは REG\_DWORD である必要があり、有効な値は90、180、および270だけです。 その他の値は0°オフセットとして処理されます (つまり、無視されます)。

各値は、時計回りの角度でセンサーの向きを表します。 カメラパイプラインは、ビデオを同じ量のカウンターで時計回りに回転するカウンターによって、結果として得られるビデオフレームを修正します。つまり、90度時計回りの宣言では、90度に反時計回りの回転が行われ、結果のビデオフレームが0に戻ります。度オフセット。

### <a name="ms-os-descriptor-10"></a>MS OS 記述子1.0

USB ベースのカメラの場合は、MSOS の記述子を使用して FSSensorOrientation を公開することもできます。

<!-- FIXME: Overview of OS descriptor could be removed -->
MS OS 記述子1.0 には、次の2つのコンポーネントがあります。

- 固定長ヘッダーセクション
- ヘッダーセクションの後に続く1つ以上の可変長カスタムプロパティセクション

#### <a name="ms-os-descriptor-10-header-section"></a>MS OS 記述子1.0 ヘッダーセクション

ヘッダーセクションでは、1つのカスタムプロパティ (Face Auth Profile) について説明します。

| Offset | フィールド      | サイズ (バイト) | 値  | 説明                     |
| ------ | ---------- | ------------ | ------ | ------------------------------- |
| 0      | dwLength   | 4            | \<\>   |                                 |
| 4      | bcdVersion | 2            | 0x0100 | バージョン 1.0                     |
| 6      | wIndex     | 2            | 0x0005 | 拡張プロパティの OS 記述子 |
| 8      | wCount     | 2            | 0x0001 | 1つのカスタムプロパティ             |

#### <a name="custom-ms-os-descriptor-10-property-section"></a>カスタム MS OS 記述子1.0 プロパティセクション

| Offset | フィールド                | サイズ (バイト) | 値                              | 説明                                  |
| ------ | -------------------- | ------------ | ---------------------------------- | -------------------------------------------- |
| 0      | dwSize               | 4            | 0x00000036 (54)                    | このプロパティの合計サイズ (バイト単位)。     |
| 4      | dwPropertyDataType   | 4            | 0x00000004                         | REG\_DWORD\_リトル\_エンディアン                   |
| 8      | wPropertyNameLength  | 2            | 0x00000024 (36)                    | プロパティ名のサイズ (バイト単位)。        |
| 10     | bPropertyName        | 50           | UVC-FSSensorOrientation            | Unicode での "UVC-FSSensorOrientation" 文字列。 |
| 60     | dwPropertyDataLength | 4            | 0x00000004                         | プロパティデータ (sizeof (DWORD)) の場合は4バイト。   |
| 64     | bPropertyData        | 4            | 時計回りのオフセット角度 (度単位)。 | 有効な値は、90、180、および270です。           |

### <a name="ms-os-descriptor-20"></a>MS OS 記述子2.0

MSOS 拡張記述子2.0 を使用して、FSSensorOrientation サポートを追加するためのレジストリ値を定義できます。 これを行うには、 [MICROSOFT OS 2.0 のレジストリプロパティ記述子](uvc-camera-implementation-guide.md#microsoft-os-20-registry-property-descriptor)を使用します。

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

## <a name="declare-via-acpi-pld-information"></a>ACPI PLD 情報を使用して宣言する

最後の手段として、前に説明したように PLD 情報を利用して、レンダリングまたはエンコードする前にビデオフレームを修正する必要があることをアプリケーションに示すことができます。 ただし、既に説明したように、既存のアプリケーションの多くは PLD 情報を使用せず、フレームのローテーションも処理しないため、アプリが結果のビデオを正しく表示できない場合があります。

次の図は、各ハードウェア構成\_の pld 回転フィールドの値を示しています。

### <a name="rotation-0-degree-clockwise"></a>ローテーション時計回りに0度

![0度回転の図](./images/rotation-0-degree-reference-orientation.png)

上の図では、次のようになります。

- 左側の画像は、キャプチャするシーンを示しています。
- 中央の画像は、左側から上に向かって左から右へ移動する、CMOS センサーによってシーンがどのように表示されるかを示しています。
- 右側の画像は、カメラドライバーの出力を表しています。 この例では、メディアバッファーの内容を直接レンダリングできます。一方、ディスプレイは、追加の回転を必要としないネイティブな方向です。 その結果、ACPI \_pld 回転フィールドの値は0になります。

### <a name="rotation-90-degrees-clockwise"></a>ローテーション90°時計回り

![90度回転の図](./images/rotation-90-degrees-clockwise.png)

この場合、元のシーンと比較して、メディアバッファーの内容が時計回りに90°回転します。 その結果、ACPI \_pld の回転フィールドの値は2になります。

### <a name="rotation-180-degrees-clockwise"></a>ローテーション180°時計回り

![180度回転の図](./images/rotation-180-degrees-clockwise.png)

この場合、元のシーンと比較して、メディアバッファーの内容が時計回りに180°回転します。 その結果、ACPI \_pld 回転フィールドの値は4になります。

### <a name="rotation-270-degrees-clockwise"></a>ローテーション270°時計回り

![270度回転の図](./images/rotation-270-degrees-clockwise.png)

この場合、元のシーンと比較して、メディアバッファーの内容が時計回りに270°回転します。 その結果、ACPI \_pld 回転フィールドの値は6になります。
