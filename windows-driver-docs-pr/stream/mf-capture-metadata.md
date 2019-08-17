---
title: キャプチャの統計情報メタデータ属性
description: このトピックでは、MFT0 によって設定または転送する必要がある capture stats メタデータの IMFAttributes について説明します。
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1a4fc6ddb963e745063785aa452d4fc467bb310d
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565920"
---
# <a name="capture-stats-metadata-attributes"></a>キャプチャの統計情報メタデータ属性

次の表は、preview、video、および capture の MFT0's **mfsampleextension\_CaptureMetaData**メタデータ属性バッグの利用可能な capture stats imfattributes をまとめたものです。

それ以外の場合は、キャプチャされたすべての写真に対して、キャプチャの統計情報は必須です。 プレビューおよびビデオ用に一覧表示されているキャプチャの統計情報は、ベストエフォートとして配信される必要があります。ドライバーは、可用性とパフォーマンスに関する考慮事項に基づいて、すべてのフレームに対するすべてのキャプチャの統計情報を提供することができます。

| 名前                                                                                              | 種類             | Pin                   | 説明            |
| ------------------------------------------------------------------------------------------------- | ---------------- | --------------------- | ---------------------- |
| [MF\_キャプチャ\_メタデータ\_FOCUSSTATE](#mf_capture_metadata_focusstate)                              | UINT32           | [プレビュー]               | この属性には、次のいずれかの値を取ることができる現在のフォーカス状態が含まれます。 |
| [MF\_キャプチャ\_メタデータ\_の SENSORFRAMERATE](#mf_capture_metadata_sensorframerate)                    | UINT64           | [プレビュー]               | この属性には、プレビューフレームがキャプチャされたときの測定単位の測定値が含まれます。これは、32ビットの分子値と下位32ビットの分母値で構成されます。 |
| [MF\_キャプチャ\_メタデータ\_FACEROIS](#mf_capture_metadata_facerois)                                  | Blob             | プレビュー、ビデオ        | この属性には、ドライバーによって検出された顔四角形情報が含まれます。 |
| [MF\_キャプチャ\_メタデータ\_FACEROITIMESTAMPS](#mf_capture_metadata_faceroitimestamps)                | Blob             | プレビュー、ビデオ        | この属性には、 **MF\_CAPTURE\_\_メタデータ FACEROIS**で識別される face ROIs のタイムスタンプ情報が含まれます。 |
| [MF\_キャプチャ\_メタデータ\_FACEROICHARACTERIZATIONS](#mf_capture_metadata_faceroicharacterizations)  | Blob             | プレビュー、ビデオ        | この属性には\\、 **MF\_キャプチャ\_メタ\_データ FACEROIS**で識別される face ROIs の点滅および顔式の状態が含まれます。 |
| [メイン\_フレーム\_キャプチャ\_メタ\_データの公開時間](#mf_capture_metadata_exposure_time)                       | UINT64           | プレビュー、引き続き        | この属性には、100ナノ秒で適用される露出時間が含まれます。 |
| [MF\_\_\_CAPTURE\_のメタデータの露出の補正](#mf_capture_metadata_exposure_compensation)       | Blob             | プレビュー、引き続き        | この属性には、EV 補正ステップフラグと、写真がキャプチャされたときにドライバーに適用されたステップの単位での EV 補正値が含まれています。 |
| [MF\_の\_キャプチャ\_の\_メタデータ ISO 速度](#mf_capture_metadata_iso_speed)                               | UINT32           | プレビュー、引き続き        | この属性には、整数として適用される ISO 速度の値が含まれます。 |
| [MF\_キャプチャ\_メタデータ\_のレンズ\_位置](#mf_capture_metadata_lens_position)                       | UINT32           | プレビュー、引き続き        | この属性には、キャプチャした写真にフォーカスが適用されたときの論理レンズ位置が含まれます。 この値には、特定の単位がありません。 |
| [MF\_キャプチャ\_メタデータ\_シーンモード\_](#mf_capture_metadata_scene_mode)                             | UINT64           | それでもなお                 | この属性には、 **UINT64KSCAMERA_EXTENDEDPROP_SCENEMODE_XXX**フラグとして適用されるシーンモードが含まれます。 |
| [MF\_キャプチャ\_メタデータ\_のフラッシュ](#mf_capture_metadata_flash)                                        | UINT32 (ブール値) | プレビュー、引き続き        | この属性には、flash の状態を含むブール値が含まれます。 値が1の場合は、フラッシュがオンになっていることを示し、値0は、キャプチャされた写真のフラッシュがオフであることを示します。 |
| [MF\_キャプチャ\_メタデータ\_のフラッシュ\_パワー](#mf_capture_metadata_flash_power)                           | UINT32           | それでもなお                 | \[省略\]可能。この属性には、0 ~ 100 のパーセント値として適用されるフラッシュ電源が含まれます。 |
| [メイン\_フレーム\_キャプチャ\_メタデータのホワイトバランス](#mf_capture_metadata_whitebalance)                          | UINT32 (ケルビン)  | プレビュー、引き続き        | この属性には、値として適用される白のバランス (ケルビン) が含まれます。 |
| [MF\_キャプチャ\_メタデータ\_ZOOMFACTOR](#mf_capture_metadata_zoomfactor)                              | UINT32 (Q16)     | それでもなお                 | この属性は、適用されるズーム値を含み、GET 呼び出しで[**KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-zoom)からクエリを実行できるのと同じ値です。 値は Q16 にある必要があります。 |
| [メイン\_フレーム\_キャプチャ\_のメタデータ EXIF](#mf_capture_metadata_exif)                                          | Blob             | それでもなお                 | \[省略\]可能。この属性には、 [blob 定義セクション](#blob-definition)で指定されている EXIF メタデータが含まれます。 |
| [MF\_キャプチャメタデータ\_でフレーム\_\_設定\_ID が要求されました\_](#mf_capture_metadata_requested_frame_setting_id) | UINT32           | それでもなお                | \[省略\]可能。この属性には、変数のフォトシーケンス内の対応するフレームのフレーム ID が格納されます。 この属性は、変数の写真シーケンスキャプチャに対してのみ設定されます。 |
| [メイン\_フレーム\_の\_キャプチャ\_メタデータの ISO の利点](#mf_capture_metadata_iso_gains)                               | Blob             | [プレビュー]               | この属性には、senor はプレビューフレームがキャプチャされたときに適用されるアナログおよびデジタルの向上が含まれます。 これは、単位はありません。 |
| [メイン\_フレーム\_キャプチャ\_メタデータ\_のホワイトバランスの向上](#mf_capture_metadata_whitebalance_gains)             | Blob             | [プレビュー]               | この属性に\\は、プレビューフレームがキャプチャされたときに、センサーまたは ISP によって R、G、B に適用されたホワイトバランスの向上が含まれます。 これは単位なしです。 |
| [MF\_キャプチャ\_メタデータ\_ヒストグラム](#mf_capture_metadata_histogram)                                | Blob             | [プレビュー]               | この属性には、apreview フレームがキャプチャされたときのヒストグラムが含まれます。 |
| [MF\_キャプチャ\_メタデータ\_フレーム\_の照明](#mf_capture_metadata_frame_illumination)             | UINT64           | Hello に使用される IR Pin | IR カメラのこの属性は、フレームがアクティブな IR 照明を使用していて、 **FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION**と組み合わせて使用する必要があるかどうかを指定します。 |
| 任意のカスタム GUID                                                                                   | 任意のバリアント型 |                       | この属性には、カスタム GUID に関連付けられたカスタムデータが含まれます。 |

## <a name="mf_capture_metadata_focusstate"></a>MF_CAPTURE_METADATA_FOCUSSTATE

MF\_CAPTURE\_METADATA\_FOCUSSTATE 属性には、次のいずれかの値を取ることができる現在のフォーカス状態が含まれています。

```cpp
typedef enum
{
    KSCAMERA_EXTENDEDPROP_FOCUSSTATE_UNINITIALIZED = 0,
    KSCAMERA_EXTENDEDPROP_FOCUSSTATE_LOST,
    KSCAMERA_EXTENDEDPROP_FOCUSSTATE_SEARCHING,
    KSCAMERA_EXTENDEDPROP_FOCUSSTATE_FOCUSED,
    KSCAMERA_EXTENDEDPROP_FOCUSSTATE_FAILED,
} KSCAMERA_EXTENDEDPROP_FOCUSSTATE;
```

## <a name="mf_capture_metadata_sensorframerate"></a>MF_CAPTURE_METADATA_SENSORFRAMERATE

MF\_キャプチャ\_メタデータ\_の sensorframerate 属性には、プレビューフレームがキャプチャされたときの測定単位の測定値が含まれます。これは、32ビットの分子値と、32ビットより下位。

## <a name="mf_capture_metadata_facerois"></a>MF_CAPTURE_METADATA_FACEROIS

MF\_CAPTURE\_METADATA\_FACEROIS 属性には、ドライバーによって検出された顔四角形情報が含まれています。 既定では\\、ドライバー MFT0 はプレビューストリームで顔情報を提供する必要があります。 ドライバーが他のストリームに対して機能を\\アドバタイズする場合、アプリケーションがそれらのストリームで顔検出を有効にすると、ドライバー MFT は対応するストリームに顔情報を提供する必要があります。 ドライバーでビデオ安定化が有効になっている場合は、ビデオを安定化した後、顔情報を入力する必要があります。 以下のデータ構造は、MF\_\_\_の blob 形式を示しています。 FACEROIS です。 優位の顔は、blob の最初の Facerの情報である必要があります。

```cpp
typedef struct tagFaceRectInfoBlobHeader
{
    ULONG Size;             // Size of this header + all FaceRectInfo following
    ULONG Count;            // Number of FaceRectInfo’s in the blob
} FaceRectInfoBlobHeader;

typedef struct tagFaceRectInfo
{
    RECT Region;            // Relative coordinates on the frame that face detection is running (Q31 format)
    LONG ConfidenceLevel;   // Confidence level of the region being a face ([0, 100])
} FaceRectInfo;
```

Facerて infoboblobheader および facerFACEROIS info 構造体は、MF\_\_\_の blob 形式のみを表しています。 Face ROIs のメタデータ項目構造 (KSCAMERA\_metadata\_itemheader + face ROIs metadata payload) はドライバーまでであり、8バイトでアラインされている必要があります。

仕様により、ストリームが顔検出を有効にして構成されていて、問題のシーンにキャプチャ中に顔が含まれていない場合でも\_、\_ドライバー\_は "ダミー" の MF キャプチャメタデータをアタッチする必要があり FACEROISface 情報が関連付けられていない各サンプルの属性です。 ("ダミー" フェイス ROI 属性では、 *Facerに*対して " *Count* " フィールドが0に設定されています)。

## <a name="mf_capture_metadata_faceroitimestamps"></a>MF_CAPTURE_METADATA_FACEROITIMESTAMPS

Mf\_capture\_\_metadata FACEROITIMESTAMPS 属性には、mf キャプチャメタデータ\_FACEROIS で識別される face ROIs のタイムスタンプ情報が含まれています。\_\_ デバイスで face ROIs のタイムスタンプを指定できない場合は、この属性を省略する必要があります。

以下のデータ構造は、MF\_\_\_の blob 形式を示しています。 FACEROITIMESTAMPS です。

```cpp
typedef struct tagMetadataTimeStamps
{
    ULONG Flags;            // Bitwise OR of MF_METADATATIMESTAMPS_XXX flags
    LONGLONG Device;        // QPC time for the sample where the face rect is derived from (in 100ns)
    LONGLONG Presentation;  // PTS for the sample where the face rect is derived from (in 100ns)
} MetadataTimeStamps;
```

Flags フィールドには、有効なタイムスタンプを示す次のビットフラグを定義します。 MFT0 は、ドライバーが face\_ROIs のタイムスタンプ\_メタデータを提供する場合、メインフレームにフラグを設定し、デバイスに対して適切な qpc の時刻を設定する必要があります。

\#メインフレーム\_\_デバイス0x00000001 を定義する

\#メインフレーム\_\_の表示を定義する0x00000002

MetadatFACEROITIMESTAMPS 構造体は、MF\_\_の blob 形式だけを説明しています。\_ Timestamp のメタデータ項目構造 (KSCAMERA\_metadata\_itemheader + タイムスタンプメタデータペイロード) はドライバーまでであり、8バイトでアラインされている必要があります。

## <a name="mf_capture_metadata_faceroicharacterizations"></a>MF_CAPTURE_METADATA_FACEROICHARACTERIZATIONS

Mf\_capture\_\\\_メタデータ\_FACEROICHARACTERIZATIONS 属性には、mf キャプチャメタデータで識別される face ROIs の点滅および顔式の状態が含まれます。\_\_FACEROIS。  点滅および\\顔式の検出をサポートしていないデバイスの場合は、この属性を省略する必要があります。

以下のデータ構造は、MF\_\_\_の blob 形式を示しています。 FACEROICHARACTERIZATIONS です。

FaceCharacterizationBlobHeader と FaceCharacterization の構造体では、MF\_CAPTURE\_METADATA\_FACEROICHARACTERIZATIONS 属性の blob 形式のみが記述されていることに注意してください。 Face 文字を表すメタデータ項目の構造 (KSCAMERA\_metadata\_itemheader + face 文字のメタデータペイロード) はドライバーまでであり、8バイトでアラインされている必要があります。

```cpp
typedef struct tagFaceCharacterizationBlobHeader
{
    ULONG Size;     // Size of this header + all FaceCharacterization following
    ULONG Count;    // Number of FaceCharacterization’s in the blob. Must match the number of FaceRectInfo’s in FaceRectInfoBlobHeader
} FaceCharacterizationBlobHeader;

typedef struct tagFaceCharacterization
{
    ULONG BlinkScoreLeft;   // [0, 100]. 0 indicates no blink for the left eye. 100 indicates definite blink for the left eye
    ULONG BlinkScoreRight;  // [0, 100]. 0 indicates no blink for the right eye. 100 indicates definite blink for the right eye
    ULONG FacialExpression; // Any one of the MF_METADATAFACIALEXPRESSION_XXX defined
    ULONG FacialExpressionScore; // [0, 100]. 0 indicates no such facial expression as identified. 100 indicates definite such facial expression as defined
} FaceCharacterization;
```

次の例では、検出可能な顔式を定義しています。  

```cpp
#define MF_METADATAFACIALEXPRESSION_SMILE             0x00000001
```

MF\_CAPTURE\_METADATAFACEROICHARACTERIZATIONS属性にが示されている場合、blob内のFaceCharacterizationエントリの数と順序が、のblob内のfacerているエントリの数と順序と一致している必要があります。\_MF\_CAPTURE\_メタデータ\_FACEROIS。   各 FaceCharacterization エントリは、同じインデックス\\にある対応する facer info エントリ内の顔の点滅および顔式の状態を表します。

次の図は、face の ROIs blob のレイアウトと4つの顔の face blob を示しています。1つ目は点滅も笑顔でもありません。2番目の顔は左に点滅し、3番目の顔は点滅 (2 番目) と笑顔.

## <a name="mf_capture_metadata_exposure_time"></a>MF_CAPTURE_METADATA_EXPOSURE_TIME

MF\_CAPTURE\_METADATA露光\_\\時間属性には、プレビューフレームまたはフォトフレームがキャプチャされたときにセンサーに適用された露出時間が含まれます。これは UINT64 であり、100ナノ秒単位です。\_

## <a name="mf_capture_metadata_exposure_compensation"></a>MF_CAPTURE_METADATA_EXPOSURE_COMPENSATION

MF\_CAPTURE\_メタデータ\_公開\\補正属性には、ev 補正ステップフラグと、プレビュー時にセンサーに適用されるステップの単位での ev 補正値が含まれています。\_フォトフレームがキャプチャされました。

以下のデータ構造\_は、MF のキャプチャ\_メタデータ\_の露出\_補正の blob 形式を示しています。

```cpp
typedef struct tagCapturedMetadataExposureCompensation
{
    UINT64 Flags;   // KSCAMERA_EXTENDEDPROP_EVCOMP_XXX step flag
    INT32 Value;    // EV Compensation value in units of the step
} CapturedMetadataExposureCompensation;
```

CapturedMetadataExposureCompensation 構造体では、\_MF CAPTURE\_METADATA\_露光量\_補正属性の blob 形式のみが記述されていることに注意してください。 EV 補正のメタデータ項目構造 (KSCAMERA\_metadata\_itemheader + EV 補正メタデータペイロード) はドライバーまでであり、8バイトでアラインされている必要があります。

## <a name="mf_capture_metadata_iso_speed"></a>MF_CAPTURE_METADATA_ISO_SPEED

MF\_CAPTURE\_メタデータ\_iso\\speed 属性には、プレビューフレームまたはフォトフレームがキャプチャされたときにセンサーに適用される iso 速度の値が含まれています。\_ これは、単位はありません。

## <a name="mf_capture_metadata_iso_gains"></a>MF_CAPTURE_METADATA_ISO_GAINS

メイン\_フレームキャプチャ\_メタ\_データの ISO 取得\_属性には、senor はプレビューフレームがキャプチャされたときに適用されるアナログおよびデジタルの向上が含まれています。
これは、単位はありません。

以下のデータ\_構造は、MF\_\_\_の blob 形式について説明しています。

```cpp
typedef struct tagCapturedMetadataISOGains
{
    FLOAT AnalogGain;
    FLOAT DigitalGain;
} CapturedMetadataISOGains;
```

CapturedMetadataISOGains 構造体では\_、MF CAPTURE METADATA\_ISO\_の取得\_属性の blob 形式のみが記述されていることに注意してください。 Iso の利点を得るためのメタデータ\_項目\_の構造 (KSCAMERA metadata itemheader + ISO はメタデータペイロードを取得) はドライバーまでであり、8バイトでアラインされている必要があります。

## <a name="mf_capture_metadata_lens_position"></a>MF_CAPTURE_METADATA_LENS_POSITION

MF\_CAPTURE\_METADATALENS\_\\position 属性には、プレビューフレームまたはフォトフレームがキャプチャされたときの論理レンズ位置 (単位は単位) が含まれています。\_ これは、GET 呼び出しで\_CAMERACONTROL\_拡張\_フォーカスからクエリを実行できるのと同じ値です。

## <a name="mf_capture_metadata_scene_mode"></a>MF_CAPTURE_METADATA_SCENE_MODE

MF\_キャプチャ\_\_メタデータ\_シーン\_モード属性には、キャプチャした写真に適用されたシーンモードが含まれています。これは、64ビット KSCAMERA extendedprop SCENEMODE です。\_\_XXX フラグ。

## <a name="mf_capture_metadata_flash"></a>MF_CAPTURE_METADATA_FLASH

MF\_CAPTURE\_METADATAFLASH\_属性には、プレビューフレームまたはフォトフレームがキャプチャされたときのブール値が含まれています。1つはflashon、0は\\flash off です。

## <a name="mf_capture_metadata_flash_power"></a>MF_CAPTURE_METADATA_FLASH_POWER

MF\_CAPTURE \[\]METADATA FLASH電源\_属性には、キャプチャした写真に適用されたフラッシュ電力が格納されます。これは、0 ~ 100 の範囲の値です。\_\_ ドライバーが flash の調整可能な電力をサポートしていない場合は、この属性を省略する必要があります。

## <a name="mf_capture_metadata_whitebalance"></a>MF_CAPTURE_METADATA_WHITEBALANCE

MF\_CAPTURE\_メタデータ\_のホワイトバランス属性には、プレビューフレーム\\またはフォトフレームがキャプチャされたときにセンサーに適用される白いバランスが含まれます。これは、加山の値です。

## <a name="mf_capture_metadata_whitebalance_gains"></a>MF_CAPTURE_METADATA_WHITEBALANCE_GAINS

MF\_キャプチャ\_メタデータ\_\\ホワイトバランス\_の取得属性には、プレビューフレームがキャプチャされたときに、センサーまたは ISP によって R、G、B に適用されたホワイトバランスの向上が含まれます。 これは単位なしです。

以下のデータ構造は、メイン\_フレームキャプチャ\_メタデータ\_のホワイトバランス\_の向上のための blob 形式を示しています。

```cpp
typedef struct tagCapturedMetadataWhiteBalanceGains
{
    FLOAT R;
    FLOAT G;
    FLOAT B;
} CapturedMetadataWhiteBalanceGains;
```

CapturedMetadataWhiteBalanceGains 構造体\_では、MF\_\_\_の blob 形式のみが記述されていることに注意してください。 ホワイトバランスの向上のためのメタデータ項目\_の\_構造 (KSCAMERA metadata itemheader + ホワイトバランスが得られるメタデータのペイロードを取得する) はドライバーまでであり、8バイトでアラインされている必要があります。

## <a name="mf_capture_metadata_zoomfactor"></a>MF_CAPTURE_METADATA_ZOOMFACTOR

MF\_CAPTURE\_METADATA\_\_ZOOMFACTOR 属性には、キャプチャした写真に適用されたズーム値が含まれます。これは、ksk プロパティ CAMERACONTROL EXTENDED からクエリを実行できる値と同じです。\_\_GET 呼び出しを拡大します。
これは Q16 にあります。

## <a name="mf_capture_metadata_exif"></a>MF_CAPTURE_METADATA_EXIF

メイン\_フレーム\_キャプチャ\_メタデータ exif には、セクション 3.1 (Blob 定義) で指定されている exif メタデータが含まれています。 MFT0 は、メインの EXIF メタデータを抽出します。これは\>、MF\_キャプチャ\_メタデータ\_フレームから\_カスタム\_メタデータ項目 (metadataid = metadataid カスタムスタート) として識別されます。\_ドライバーによって提供される rawstream バッファー。
MFT0 は、その後、生データを MF\_CAPTURE\_METADATA\_EXIF 属性に変換します。

### <a name="blob-definition"></a>Blob の定義

この blob は、exif 2.3 および TIFF 6.0 仕様で定義されている完全な TIFF ヘッダー、インデックス ifd、および exif サブ IFD で構成されている必要があります。 Blob には、TIFF ヘッダーの前にデータを含めることはできません。 Blob には、インデックス IFD の終了後にデータを含めることはできません。 たとえば、サムネイルデータを含む IFD を含めることはできません。

TIFF 仕様からコピーされた次の図は、想定されるメモリレイアウトを示しています。

![EXIF blob の定義](images/exif-blob-definition.png)

次に示すのは、EXIF および TIFF 仕様と一致するが、強調のために呼び出される要件です。

- バイト順には、リトルエンディアン ("II") またはビッグエンディアン ("MM") のいずれかを指定する必要があります。
- ポインター (TIFF 仕様の "バイトオフセット") は、TIFF ヘッダーの先頭に対する相対パスである必要があります。

以下は、EXIF と TIFF 仕様よりも制限が厳しい要件です。

- 次の IFD へのオフセットは0である必要があります。つまり、追加の IFDs がポイントされていないことを示します。
- TIFF ヘッダーとインデックス ifd は連続している必要があります。つまり、バイト4-7 に格納されているインデックス ifd へのオフセットは、0x8 である必要があります。

### <a name="mandatory-exif-metadata"></a>必須の EXIF メタデータ

以下のセクションでは、メインフレーム\_キャプチャ\_メタデータ\_に含める必要がある exif メタデータについて説明します。

| 名前                  | EXIF タグ  | 説明                                                           |
| --------------------- | --------- | --------------------------------------------------------------------- |
| 方向           | 274       | 行と列の観点から見た画像の向き。 詳細については、「EXIF spec」を参照してください。 |
| 使用                  | 271       | 録画装置の製造元                           |
| モデル                 | 272       | デバイスのモデル名またはモデル番号                      |
| XResolution           | 282       | ImageWidth 方向の解像度単位あたりのピクセル数  |
| YResolution           | 283       | ImageLength 方向の解像度単位あたりのピクセル数 |
| 解像度の単位        | 296       | XResolution と YResolution を測定する単位                    |
| ソフトウェア              | 305       | ファームウェアの名前とバージョン                                      |
| ColorSpace            | 40961     | 色空間の情報 (通常は sRGB)                           |
| SubsSecTimeOriginal   | 37521     | DateTimeOriginal タグに関連付けられた秒の小数部を記録します     |
| SubSecTimeDigitized   | 37522     | DateTimeDigitized タグに関連付けられた秒の小数部を記録します    |
| ExposureTime          | 33434     | 公開時間 (秒単位) (精度は 0.001)                         |
| FNumber               | 33437     | キャプチャに使用する F 番号                                         |
| ISOSpeedRatings       | 34855     | ISO 12322 で定義されている ISO 速度の値 (鮮やかさベース)             |
| DateTimeOriginal      | 36867     | 元のイメージデータが生成された日付と時刻              |
| DateTimeDIgitized     | 36868     | 画像がデジタルデータとして保存された日付と時刻             |
| シャッター SpeedValue    | 37377     | 写真露出 (頂点) ユニットの加法システムでのシャッタースピード|
| アパーチャの値        | 37378     | 頂点単位のレンズアパーチャ                                       |
| ExposureBias 値    | 37380     | 頂点単位の露出バイアス値                                     |
| MeteringMode          | 37383     | AE 使用状況測定モード (「EXIF 仕様」を参照)                                      |
| ライトソース           | 37384     | ライトソースの種類 (「EXIF 仕様」を参照)                              |
| Flash                 | 37385     | イメージキャプチャ中の flash の状態                              |
| FocalLength           | 37386     | レンズの実際の焦点の長さ                                   |
| ExposureMode          | 41986     | キャプチャ中の露出モード                                          |
| WhiteBalance          | 41987     | キャプチャ中の白いバランスモード                                     |
| DigitalZoomRatio      | 41988     | 画像キャプチャ中のデジタルズーム比                               |
| FocalLengthIn35mmFilm | 41989     | 35 mm 相当の焦点の長さ                                         |
| SceneCaptureType      | 41990     | ショットされたシーンの種類                                           |

### <a name="optionaloem-defined-metadata"></a>オプション/OEM 定義のメタデータ

カメラドライバーでは、EXIF 仕様に準拠している限り、カスタム EXIF タグの形式で追加のメタデータを含めることができます。これは、0番目の TIFF IFD または EXIF サブ IFD のいずれかに格納されます。

### <a name="makernote-requirements-and-binary-layout-expectations"></a>MakerNote の要件とバイナリレイアウトの予測

カメラドライバーには、メーカーノート (タグ 37500) の形式で製造元固有の情報が含まれている場合があります。 作成者メモには、ファイルの先頭や TIFF ヘッダーの位置など、メーカーの外部にあるデータへのポインターを含めたり、それ以外の場合に依存したりすることはできません。 また、TIFF ヘッダーで指定されているファイルのエンディアンに関する想定を作成することはできません。

一般に、オペレーティングシステムでは、メタデータ blob のバイナリレイアウトが出力 JPEG ストリームに書き込まれるときに保持されることは保証されません。 これは、EXIF 仕様に準拠してメタデータが書き込まれることのみを保証します。 たとえば、メーカーのメモが連続したブロックとしてコピーされ、正しい IFD タグ、型、およびオフセットによって識別されることのみが保証されます。

### <a name="usage-with-wic-jpeg-encoder"></a>WIC JPEG エンコーダーを使用した使用

MF\_の使用目的\_は、OS によって提供される Windows Imaging Component (WIC) の JPEG エンコーダーです。\_ Windows カメラパイプラインは、windows WIC jpeg エンコーダーを使用して、メインフレーム\_キャプチャ\_メタ\_データから取得した exif メタデータを使用します。また、アプリケーションが jpeg をキャプチャしていない場合、イメージピクセルデータを jpeg ファイルに保存します。カメラから直接取得しますが、NV12/YUY2 にキャプチャして OS によってエンコードされるように構成されたパイプライン

## <a name="mf_capture_metadata_requested_frame_setting_id"></a>MF_CAPTURE_METADATA_REQUESTED_FRAME_SETTING_ID

MF\_CAPTURE\_メタデータ\_要求\_フレームSETTING_ID属性には、変数の写真シーケンス内の対応するフレームのフレームIDが含まれ\_ています。 この属性は、変数の写真シーケンスキャプチャに対してのみ設定されます。

## <a name="mf_capture_metadata_frame_illumination"></a>MF_CAPTURE_METADATA_FRAME_ILLUMINATION

Ir\_カメラ\_の\_MF\_キャプチャメタデータフレームの照明属性フレームがアクティブな ir 照明を使用していて、FACEAUTH\_モードと組み合わせて使用する必要があるかどうかを指定します。\_代替\_フレーム照明\_。 これは IR サンプルにのみ使用され、カメラが IR サンプルとカラーサンプルの両方をサポートしている場合は、RGB フレーム上に存在していない必要があります。

アクティブな照明がオンのときにフレームがキャプチャされ、フレームをキャプチャするときに照明が存在しない場合は0xXXXXXXXXXXXXXXX0 に設定されている場合は、値を0xXXXXXXXXXXXXXXX1 に設定する必要があります。

## <a name="mf_capture_metadata_histogram"></a>MF_CAPTURE_METADATA_HISTOGRAM

MF\_キャプチャ\_メタデータ\_ヒストグラム属性には、apreview フレームがキャプチャされたときのヒストグラムが含まれています。

以下のデータ構造は、MF\_のキャプチャ\_メタデータ\_のヒストグラムの blob 形式を示しています。

```cpp
typedef struct tagHistogramGrid
{
    ULONG Width;    // Width of the sensor output that histogram is collected from
    ULONG Height;   // Height of the sensor output that histogram is collected from
    RECT Region;    // Absolute coordinates of the region on the sensor output that the histogram is collected for
} HistogramGrid;

typedef struct tagHistogramBlobHeader
{
    ULONG Size;         // Size of the entire histogram blob in bytes
    ULONG Histograms;   // Number of histograms in the blob. Each histogram is identified by a HistogramHeader
} HistogramBlobHeader;

typedef struct tagHistogramHeader
{
    ULONG Size;         // Size of this header + (HistogramDataHeader + histogram data following) * number of channels available
    ULONG Bins;         // Number of bins in the histogram
    ULONG FourCC;       // Color space that the histogram is collected from
    ULONG ChannelMasks; // Masks of the color channels that the histogram is collected for
    HistogramGrid Grid; // Grid that the histogram is collected from
} HistogramHeader;

typedef struct tagHistogramDataHeader
{
    ULONG Size;         // Size in bytes of this header + histogram data following
    ULONG ChannelMask;  // Mask of the color channel for the histogram data
    ULONG Linear;       // 1, if linear; 0 nonlinear
} HistogramDataHeader;
```

[ChannelMasks] フィールドでは、ヒストグラムで使用可能なチャネルを示すために、次のビットマスクを定義します。

```cpp
#define MF_HISTOGRAM_CHANNEL_Y  0x00000001
#define MF_HISTOGRAM_CHANNEL_R  0x00000002
#define MF_HISTOGRAM_CHANNEL_G  0x00000004
#define MF_HISTOGRAM_CHANNEL_B  0x00000008
#define MF_HISTOGRAM_CHANNEL_Cb 0x00000010
#define MF_HISTOGRAM_CHANNEL_Cr 0x00000020
```

注:

1. 各 blob には、異なる地域から収集された複数のヒストグラムまたは同じフレームの異なる色空間を含めることができます。
2. Blob 内の各ヒストグラムは、独自の HistogramHeader によって識別されます。
3. 各ヒストグラムには、独自のリージョンとセンサーの出力サイズが関連付けられています。
   完全なフレームヒストグラムの場合、リージョンは HistogramGrid で指定されたセンサー出力サイズと一致します。
4. 使用可能なすべてのチャンネルのヒストグラムデータは、1つのヒストグラムの下にグループ化されます。 各チャネルのヒストグラムデータは、データの上の HistogramDataHeader によって識別されます。 Channelmasks は、上で定義されている、サポートされている MF\_ヒストグラム\_チャネル\_XXX ビットマスクのビットごとの or である、ヒストグラムデータを保持しているチャネルの数と数を示します。 Channelmask は、データがどのようなものであるかを示します。これは\_、\_上記で定義されているいずれかの MF ヒストグラム channel\_XXX ビットマスクによって識別されます。

次の図は、完全なフレームの Y のみのヒストグラムを含むヒストグラム blob のレイアウトを示しています。

ヒストグラムデータは、各エントリの ULONG の配列であり、ビンによって分類された一連の色調値の下にあるピクセル数を表します。 配列内のデータは、ビン0から bin N-1 に開始する必要があります。ここで、N はヒストグラムのビン数 (つまり、HistogramBlobHeader) です。

次の図は、ヒストグラムデータセクションのレイアウトを示しています。

次の図は、4つのチャネルを持つ完全なフレームの YRGB ヒストグラムを持つヒストグラム blob のレイアウトを示しています。

次の図は、ヒストグラム blob のレイアウトを示しています。これには、Y のみのヒストグラムと、3つのチャンネルを持つ RGB ヒストグラムがあります。

しきい値の場合、少なくとも Y チャネルを含む完全なフレームヒストグラムを指定する必要があります。これは、ksk プロパティ\_CAMERACONTROL\_拡張\_ヒストグラムがサポートされている場合、ヒストグラム blob の最初のヒストグラムにする必要があります。

HistogramBlobHeader、HistogramHeader、HistogramDataHeader、およびヒストグラムデータでは、MF\_CAPTURE\_METADATA\_ヒストグラム属性の blob 形式のみが記述されていることに注意してください。 ヒストグラムのメタデータ項目構造 (KSCAMERA\_metadata\_itemheader + all ヒストグラムメタデータペイロード) はドライバーまでであり、8バイトでアラインされている必要があります。

## <a name="histogram-metadata-control"></a>ヒストグラムメタデータコントロール

Ksk プロパティ\_CAMERACONTROL\_拡張\_ヒストグラムは、ドライバーによって生成されるヒストグラムメタデータを制御するために使用されるプロパティ ID です。
これはプレビューピンの pin レベルコントロールであり、次のように定義されています。

```cpp
typedef enum {
    …
#if (NTDDI_VERSION >= NTDDI_WIN8)
    KSPROPERTY_CAMERACONTROL_EXTENDED_HISTOGRAM
#endif
} KSPROPERTY_CAMERACONTROL_EXTENDED_PROPERTY;
```

KSCAMERA\_extendedprop\_ヘッダーの場合、ドライバーのヒストグラムメタデータを制御するために、次のビットフラグを定義します。 既定値は OFF です。

```cpp
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_OFF 0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_ON  0x0000000000000001
```

適切なサイズのメタデータバッファーが確実\_に\_割り当てられるようにするには、このコントロールを CAMERACONTROL 拡張\_メタデータコントロールの前に使用する必要があります。

ヒストグラム\_をオフに設定した場合、ドライバーはプレビューピンでヒストグラムメタデータを配信しません。 ドライバーでは、メタデータバッファーサイズの要件にヒストグラムメタデータのサイズを含めないでください。

[ヒストグラム\_] に設定されている場合、ドライバーはプレビューピンでヒストグラムメタデータを配信します。 ドライバーでは、メタデータバッファーサイズの要件にヒストグラムメタデータのサイズが含まれている必要があります。

ドライバーがヒストグラムメタデータを生成する機能を備えていない場合、ドライバーはこのコントロールを実装しません。 ドライバーがこのコントロールをサポートしている場合は、ksk\_プロパティ\_CAMERACONTROL\_拡張メタデータコントロールもサポートする必要があります。

プレビューピンの状態が ksk 状態\_の停止状態よりも大きい場合、このコントロールの SET 呼び出しは効果がありません。 Preview が停止状態ではなく、状態\_が無効な\_デバイス\_状態を返す場合、ドライバーは受け取った設定呼び出しを拒否します。 GET 呼び出しでは、ドライバーは Flags フィールドの現在の設定を返します。

これは同期コントロールです。 このコントロールに定義されている機能はありません。

### <a name="kscamera_extendedprop_header"></a>KSCAMERA_EXTENDEDPROP_HEADER

#### <a name="version"></a>バージョン

1にする必要があります。

#### <a name="pinid"></a>PinId

は、プレビュー pin に関連付けられている Pin ID である必要があります。

#### <a name="size"></a>サイズ

にする必要があります`sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)`

#### <a name="result"></a>結果

最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。

#### <a name="capability"></a>機能

0 を指定する必要があります。

#### <a name="flags"></a>フラグ

これは、読み取り/書き込みフィールドです。 これには、 `KSCAMERA_EXTENDEDPROP_HISTOGRAM_XXX`上で定義したフラグのいずれかを指定できます。

### <a name="kscamera_extendedprop_value"></a>KSCAMERA_EXTENDEDPROP_VALUE

使用しない
