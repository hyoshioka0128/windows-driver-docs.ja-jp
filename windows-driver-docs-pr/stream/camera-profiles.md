---
title: カメラプロファイル
description: このトピックでは、カメラプロファイルの形式とそれらを定義するさまざまな方法について説明します。
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 641bfb29715f3b846864a9ac90dc89007e1e750f
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565930"
---
# <a name="camera-profiles"></a>カメラプロファイル

## <a name="ks-api-profile"></a>KS API プロファイル

### <a name="ksinitializedeviceprofile"></a>KsInitializeDeviceProfile

デバイスプロファイルを発行するには、すべてのミニポートドライバーでプロファイルストアを初期化する必要があります。これを行うには、次の KS API を呼び出す必要があります。

```c
__drv_maxIRQL(PASSIVE_LEVEL)
KSDDKAPI
NTSTATUS
NTAPI
KsInitializeDeviceProfile(
    __in PKSFILTERFACTORY FilterFactory
    );
```

#### <a name="filterfactory-ksfilterfactory"></a>FilterFactory (KSK FILTERFACTORY)

これは、カメラのフィルターファクトリを一意に識別するためにカメラドライバーによって作成された KSK FILTERFACTORY です。

Ksfilterfactory に含まれる ksk フィルター\_記述子構造体の referenceguid フィールドに、このフィルターの種類の一意の guid が設定されている必要があります。 \_Ksk フィルター記述子の Flags フィールドには、referenceguid フラグが設定さ\_れた ksk フィルター\_フラグ\_の優先順位が設定されています。

指定された\_ksk filterfactory に KSCATEGORY VIDEO\_カメラに関連付けられているデバイスインターフェイスが含まれていない場合\_、この API 呼び出しはステータス\_が無効なパラメーターで失敗します。

この KSK FILTERFACTORY のデバイスインターフェイスに関連付けられているプロファイルストアからすべてのプロファイルを削除するには、ドライバーが KsInitializeDeviceProfile を呼び出し、その直後に KsPersistDeviceProfile を呼び出します。 これにより、プロファイル情報が空になり、プロファイルストアからプロファイル情報が削除されます。

### <a name="kspublishdeviceprofile"></a>KsPublishDeviceProfile

この情報を公開するために、次の新しい KS API が導入されました。

```c
__drv_maxIRQL(PASSIVE_LEVEL)
KSDDKAPI
NTSTATUS
NTAPI
KsPublishDeviceProfile(
    __in PKSFILTERFACTORY FilterFactory,
    __in PKSDEVICE_PROFILE_INFO Profile
    );
```

この API は、カメラドライバーがサポートしている各プロファイルに対して繰り返し呼び出されます。 各呼び出しには、異なる同時実行およびデータ範囲情報のセットが含まれる場合があります。 KSCAMERA\_プロファイル\_情報のプロファイル id フィールドは一意である必要があります。 同じプロファイル id が使用され、プロファイル情報の内容が異なる場合は、それ以降の呼び出しで以前のプロファイル情報が上書きされます。

#### <a name="filterfactory-ksfilterfactory"></a>FilterFactory (KSK FILTERFACTORY)

これは、KsInitializeDeviceProfile API で使用される FilterFactory と同じです。

カメラプロファイル情報は、KSCATEGORY\_VIDEO\_カメラインターフェイスカテゴリにのみ関連付けられます。 このインターフェイスカテゴリなしで作成され、カメラプロファイルを登録しようとしたフィルターファクトリは、この\_API\_によって "無効な状態" パラメーターが返されます。

#### <a name="profile-ksdevice_profile_info"></a>プロファイル (ksk デバイス\_プロファイル\_情報)

Ksk デバイス\_プロファイル\_情報は、さまざまな種類のデバイスのプロファイル情報を処理するように設計された汎用構造です。

```c
##define KSDEVICE_PROFILE_TYPE_CAMERA 0x00000001

typedef struct _KSDEVICE_PROFILE_INFO
{
    UINT32 Type;
    UINT32 Size;
    union
    {
        struct
        {
            KSCAMERA_PROFILE_INFO Info;
            UINT32 Reserved;
            UINT32 ConcurrencyCount;
            PKSCAMERA_PROFILE_CONCURRENCYINFO Concurrency;
        } Camera;

        // Add other device type specific "profiles" here.
    };
} KSDEVICE_PROFILE_INFO, *PKSDEVICE_PROFILE_INFO;
```

***Type***

プロファイルの種類を定義します。 現時点では、唯一定義され\_て\_いる\_型は ksdevice PROFILE type カメラです。

***Size***

Sizeof (ksk device\_PROFILE\_INFO) 構造体に設定する必要があります。

***Camera.Info***

カメラのプロファイル\_情報\_を定義する KSCAMERA プロファイル情報の構造。

***カメラ。予約済み***

未使用。 0に設定する必要があります。

***ConcurrencyCount***

同時実行配列\_内\_の KSCAMERA PROFILE CONCURRENCYINFO 構造体の数。 Windows しきい値の場合は1以下である必要があります。
>
値 0 (Camera. Concurrency が NULL に設定されている) は、このプロファイルが非同時実行であることを示します。

***Camera. Concurrency***

このプロファイルの\_同時\_実行サポートを記述する KSCAMERA profile CONCURRENCYINFO 構造体の配列。 CountOfConcurrency が0の場合、このパラメーターは NULL である必要があります。 CountOfConcurrency が\>0 の場合、このパラメーターを NULL にすることはできません。

#### <a name="kscamera_profile_info"></a>KSCAMERA_PROFILE_INFO

KSCAMERA\_profile\_INFO 構造体は、特定のプロファイルを一意に識別するために使用されます。

```c
typedef struct _KSCAMERA_PROFILE_INFO
{
    UINT32 ProfileId;
    UINT32 Index;
    UINT32 PinCount;
    PKSCAMERA_PROFILE_PININFO Pins
} KSCAMERA_PROFILE_INFO, *PKSCAMERA_PROFILE_INFO;
```

***プロファイル id***

プロファイルの一意の ID を表す GUID。 この GUID は、一意の IHV/OEM が作成したカスタムプロファイルを表す GUID である場合もあれば、セクション3.1 で説明されている定義済みの guid のいずれかである場合もあります。

注: このフィールドを KSCAMERAPROFILE\_Legacy に設定することはできません。 レガシプロファイルは、カメラドライバーによって発行されていない必要があります。 プロファイルをサポートできることがアプリケーションに示されていない場合は、キャプチャエンジンまたはメディアキャプチャの初期化中に、レガシプロファイル ID がカメラドライバーに送信されます。 このような場合、カメラドライバーは動作を Windows 8.1 モードに戻す必要があります。また、縮小されたセットのメディアの種類のみ\_を\_、\_対応する ksk プロパティ CAMERACONTROL IMAGE PIN\_と共に公開する必要があります。レコード\_と\_ksk\_プロパティCAMERACONTROL\_IMAGEPIN 機能シーケンス\_と排他的な機能\_\_\_\_録音\_機能\_ビットを使用した排他的。カメラドライバーが、縮小されたメディアの種類の中で、同時録音/写真/録音/フォトシーケンスをサポートできるかどうかを示します。

***Index***

特定のプロファイル id グループ内の各プロファイルには、一意のインデックス値が必要です。 これにより、デバイスのすべてのプロファイルをプロファイル id + Index で一意に識別できるようになります。

***PinCount***

ピンが指す KSCAMERA\_PROFILE\_pininfo 構造体の数。 この値は\>0 にする必要があります。

***エジェクタピン***

このプロファイルの\_各\_ピンでサポートされているメディアの種類を定義する KSCAMERA PROFILE pininfo 構造体の配列。

このフィールドを NULL にすることはできません。

#### <a name="concurrency-kscamera_profile_concurrencyinfo"></a>同時実行 (\_KSCAMERA\_PROFILE CONCURRENCYINFO)

現在、アプリケーションには、試行が成功するか失敗するまで、複数のカメラからのストリームを試行できるかどうかについての情報はありません。
Web ブログのシナリオでは、アプリケーションは、picture video 要素の画像を使用して UI を描画する前に、両方のストリームのアクティブ化を試みる必要があることを意味します。

Concurrency パラメーターは、アプリケーションに対して、特定のプロファイル (または一連のプロファイル) を使用して、フロントカメラとバックカメラの両方を同時にアクティブ化できることを示すヒントを提供します。 この知識があれば、アプリケーションは、アクティブ化する前に両方のストリームの UI 要素を描画できます。

複数のアプリケーションの場合、同時実行操作を保証するには同時実行性が十分ではありません。 同時実行の情報は、このシナリオの解決を試みません。 代わりに、Windows 8 の既存のカメラ Yanking 機能が活用されます。

Concurrency パラメーターは、KSCAMERA\_profile\_CONCURRENCYINFO structure (配列のサイズが CountOfConcurrency パラメーターで指定されている) の配列を表します。この構造体は、プロファイルで特定されたプロファイルをKSCAMERA\_PROFILE\_INFO 構造体は、異なるカメラで同時に実行できます。

CountOfConcurrency と camera の両方が 0 & NULL の場合は、KSCAMERA\_プロファイル\_情報によって定義されたプロファイルが同時実行プロファイルではないことを OS に示します。

```c
typedef struct _KSCAMERA_PROFILE_CONCURRENCYINFO
{
    GUID ReferenceGuid;
    UINT32 Reserved;
    UINT32 ProfileCount;
    PKSCAMERA_PROFILE_INFO Profiles;
} KSCAMERA_PROFILE_CONCURRENCYINFO,*PKSCAMERA_PROFILE_CONCURRENCYINFO;
```

***ReferenceGuid***

は、このプロファイルが同時に使用されて\_いる他のデバイスに対応する ksk フィルター記述子の referenceguid に設定する必要があります。

***Reserved***

未使用。 0 を指定する必要があります。

***ProfileCount***

プロファイル配列に格納されているプロファイル Id の数。 1 以上であることが必要です。

***Profiles***

これは、referenceguid によっ\_て\_指定された他のカメラデバイスで同時に使用できる KSCAMERA プロファイル情報の配列です。

このフィールドを NULL にすることはできません。

#### <a name="pins-kscamera_profile_pininfo"></a>ピン (KSCAMERA\_PROFILE\_pininfo)

各 pin に使用できるメディアの種類の一覧を指定するには、KSCAMERA\_PROFILE\_pininfo の配列を指定する必要があります。配列のサイズは、CountOfPins パラメーターで指定します。

```c
typedef struct _KSCAMERA_PROFILE_PININFO
{
    GUID PinCategory;
    UINT32 Reserved;
    UINT32 MediaInfoCount;
    PKSCAMERA_PROFILE_MEDIAINFO MediaInfos;
} KSCAMERA_PROFILE_PININFO, *PKSCAMERA_PROFILE_PININFO;
```

***PinCategory***

これは、Capture、Preview、静止画像ピンに対応する PINNAME カテゴリです。 Windows Threshold の場合、サポートされている pin カテゴリは次のとおりです。PINNAME\_VIDEO\_CAPTURE、PINNAME\_VIDEO\_PREVIEW、PINNAME\_VIDEO\_. その他のすべてのカテゴリは、\_"\_無効なパラメーターエラー" という状態になります。

***Reserved***

未使用。 0 を指定する必要があります。

***メディアの数***

MediaInfos フィールドに指定\_さ\_れている KSCAMERA PROFILE mediainfo.xml 構造体の配列サイズ。

***Mediainfo.xml***

KSCAMERA\_PROFILE\_mediainfo.xml 構造体の配列。

#### <a name="mediainfos-kscamera_profile_mediainfo"></a>MediaInfos (KSCAMERA\_PROFILE\_mediainfo.xml)

各プロファイルについて表示される関連メディアの種類情報は、次の方法で説明されています。

```c
##define KSCAMERAPROFILE_FLAGS_VIDEOHDR              0x0000000000000002
##define KSCAMERAPROFILE_FLAGS_VARIABLEPHOTOSEQUENCE 0x0000000000000010

typedef struct _KSCAMERA_PROFILE_MEDIAINFO
{
    struct
    {
        UINT32 X;
        UINT32 Y;
    } Resolution;
    struct
    {
        UINT32 Numerator;
        UINT32 Denominator;
    } MaxFrameRate;
    ULONGLONG Flags;
    UINT32 Data0;
    UINT32 Data1;
    UINT32 Data2;
    UINT32 Data3;
} KSCAMERA_PROFILE_MEDIAINFO, *PKSCAMERA_PROFILE_MEDIAINFO;
```

***解決方法***

X (水平) と Y (垂直) のフレームサイズ (ピクセル単位)。

***MaxFrameRate レート***

フレームレートの num/デ om 比率 (例:30/1 = 30fps)。 このフレームレートは、理想的な照明条件下での指定された解像度の最大フレームレートを表します。 実際のフレームレートは、この値よりも小さくなる場合があります。

写真メディア情報の場合、指定された写真解像度に対するハードウェアの制約が原因で写真シーケンスを有効にできない場合は、フレームレートを 0 (num = 0、の場合は、を0に設定) に設定する必要があります。 これにより、特定の写真メディアの種類が選択されたときに、ドライバーによってフォトシーケンスコントロールが拒否されることがアプリケーションレイヤーに通知されます。

***フラグ***

次のフラグの1つ以上のビットごとの OR を使用できます。

- **KSCAMERAPROFILE\_FLAGS\_videohdr**ビデオの hdr フラグがメディア情報に設定されている場合、そのメディア設定のレコードストリームでビデオの hdr が有効になっている可能性があります。

  このフラグは、フォト pin のメディア情報には設定できません。
- **KSCAMERAPROFILE\_FLAGS\_VARIABLEPHOTOSEQUENCE** 、メディア情報に対して変数 photo Sequence フラグが設定されている場合、フォトメディア情報でフレームレートが提供されていなくても、VPS サポートは使用できます。

  このフラグが設定されている場合 & フレームレートが0以外の場合は、VPS とフォトシーケンスを使用できます。

  このフラグが設定されている場合 & フレームレートが0の場合、VPS は使用できますが、写真シーケンスでは使用できません。

  このフラグが設定されていない &、そのフォトメディア情報に対してフレームレートが0以外の場合、VPS は使用できませんが、フォトシーケンスは使用できます。

  このフラグが設定されていない & フレームレートが0の場合は、そのメディア情報に対して VPS も Photo シーケンスも使用できません。

  このフラグは、フォト pin のメディア情報に対してのみ設定できます。 フォト pin 以外のメディア情報にこのフラグが存在すると、プロファイルセットが拒否されます。

***Data0...番***

フラグに基づいて決定される値。 この時点では、は0に設定されている必要があります。

### <a name="kspersistdeviceprofile"></a>KsPersistDeviceProfile

プロファイル情報を永続ストアにコミットするには、次の KS API を呼び出す必要があります。

```c
__drv_maxIRQL(PASSIVE_LEVEL)
KSDDKAPI
NTSTATUS
NTAPI
KsPersistDeviceProfile(
    __in PKSFILTERFACTORY FilterFactory
    );
```

#### <a name="filterfactory-ksfilterfactory"></a>FilterFactory (KSK FILTERFACTORY)

これは、Ksk Initializedeviceprofile でプロファイルストアを初期化するために使用された KSK FILTERFACTORY です。 最初に kspersistdeviceprofile を使用してプロファイルストアを初期化せずに、ksk persistdeviceprofile が呼び出された場合、kspersistdeviceprofile への呼び出しは失敗し、状態\_が無効な\_デバイス\_要求で失敗します。

さらに、プロファイル情報が保存され\_て\_いるときにページプールが使い果たされた場合、この API はリソース不足の状態で失敗することもあります。

### <a name="ksproperty_cameracontrol_extended_profile"></a>KSPROPERTY_CAMERACONTROL_EXTENDED_PROFILE

> ***検索バージョン1***
>
> ***制御フィルター***
>
> ***各種キャンセル可能なではなく非同期***

新しい拡張プロパティコントロールが導入されました。これにより、キャプチャフレームワークは、選択されたプロファイルをカメラドライバーに通知できるようになります。

#### <a name="kscamera_extendedprop_header"></a>KSCAMERA_EXTENDEDPROP_HEADER

**バージョン**

拡張プロパティコントロールバージョン1に対して定義されています。

**PinId**

(0xffffffff `KSCAMERA_EXTENDEDPROP_FILTERSCOPE` ) である必要があります。

**Size**

にする必要があります。`sizeof(KSCAMERA_EXTENDEDPROP_HEADER) +
sizeof(KSCAMERA_EXTENDEDPROP_PROFILE)`

**結果**

最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。 0は、エラーが検出されなかったことを示します。

**機能**

にする必要があります。`KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL` 他のモードはサポートされていません。

**フラグ**

0 を指定する必要があります。

#### <a name="kscamera_extendedprop_profile"></a>KSCAMERA_EXTENDEDPROP_PROFILE

Ksk\_プロパティ CAMERACONTROL\_\_\_\_ EXTENDED PROFILE コントロールのペイロードには、KSCAMERA extendedprop ヘッダー + KSCAMERA extendedprop が含まれています。\_\_PROFILE.

```c
typedef struct _KSCAMERA_EXTENDEDPROP_PROFILE
{
    GUID ProfileId;
    UINT32 Index;
    UINT32 Reserved;
} KSCAMERA_EXTENDEDPROP_PROFILE, *PKSCAMERA_EXTENDEDPROP_PROFILE;
```

**プロファイル id**

選択されたプロファイルを表す GUID。 これが KSCAMERAPROFILE\_レガシの場合、プロファイルは選択されていません。カメラドライバーは、縮小されたセットメディアの種類を公開する必要があります。

このフィールドが GUID\_NULL の場合、プロファイルは選択されていませんが、アプリケーションはプロファイルに対応しているため、カメラドライバーはすべてのメディアの種類を公開する必要があります。

**Index**

識別されたプロファイルに関連付けられているインデックス値。

**Reserved**

未使用。 0 を指定する必要があります。

## <a name="inf-profile"></a>INF プロファイル

Oem による柔軟性を実現するために、同じ参照ドライバーを使用するが、センサーが異なる (または異なるパフォーマンスレベルの場合でも) 異なる Sku に基づいて、プロファイルを発行または上書きするには、次の INF セクションを使用します。

新規または既存の各プロファイルには、 \[デバイスインターフェイスノードの下\]に格納される、セミコロンで区切られた文字列の profildid GUID、インデックス値が必要です。

```reg
OEMCameraProfiles: REG_SZ:
KSCAMERAPROFILE_VideoRecording,0;KSCAMERAPROFILE_HighQualityPhoto,0;KSCAMERAPROFILE_BalancedVideoPhoto,0;KSCAMERAPROFILE_VideoConferencing,0;{3074C75C-1D69-4A0A-895D-EB9EFDE1CF30},0
```

上記の例では、0<sup>番目</sup>のインデックス付き、KSCAMERAPROFILE\_VideoRecording、KSCAMERAPROFILE\_HighQualityPhoto、KSCAMERAPROFILE\_BalancedVideoPhoto、および\_ KSCAMERAPROFILE をオーバーライドしています。ID が {3074C75C-1D69-4A0A-895D-EB9EFDE1CF30} の新しいカスタムプロファイルと共にビデオ会議を行う

OEMCameraProfiles 内の各プロファイル GUID に対して、区切られた文字列で指定された名前と一致するデバイスインターフェイスノードに新しいサブキーを作成する必要があります。

次の値を追加して、このサブキーの下で、OEM はプロファイルが無効になっている (つまり、ドライバーによって発行された設定を上書きする) ことを示している可能性があります。

```reg
Disabled: REG_DWORD: 0x1
```

OEM では、プロファイルを単に無効にするのではなく、使用可能なメディアの種類を変更または公開する必要がある場合は、ストリームの PinCategory に一致する別のサブキーを作成する必要があります。

たとえば、インデックス番号が 0<sup>番目</sup>の KSCAMERAPROFILE\_のプレビューピンを発行するには、次のように VideoRecording します。

```reg
<Device Interface Node>KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW

MediaCount: REG_DWORD: N
Media0: REG_SZ: <MediaInfo Format>
...
MediaN-1: REG_SZ: <MediaInfo Format>
```

MediaCount レジストリ値は、この pin に存在する Mediainfo.xml の数を示します。 各 mediainfo.xml には、"Media\#" のレジストリエントリ名を指定する必要があります。ここで、\ は0から始まるインデックス (つまり、Media0、Media1、Media2,..., 中央値) を表します。

Media0 によって指定された Mediainfo.xml は、プロファイルの優先メディアの種類として扱われます。

上記の Mediainfo.xml 形式では、次の構文を指定します。

```reg
MediaInfo Format = <ResolutionX>, <ResolutionY>, <MaxFrameRateNum>,<MaxFrameRateDenom>, Flags, Data0, Data1, Data2, Data3
```

次に例を示します。

```reg
<Device Interface Node>KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW

MediaCount: REG_DWORD: 2
Media0: REG_SZ: 1280,720,30,1,0,0,0,0,0
Media1: REG_SZ: 640,360,30,1,0,0,0,0,0

<Device Interface
Node>KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_CAPTURE

MediaCount: REG_DWORD: 3
Media0: REG_SZ: 1280,720,30,1,0,0,0,0,0
Media1: REG_SZ: 1920,1080,30,1,0,0,0,0,0
Media2: REG_SZ: 640,360,30,1,0,0,0,0,0
```

は、VideoRecording プロファイルを IHV の設定から発行します。これは、(720p が優先メディアの種類を設定した) 1080p、720p、360p の記録のみを許可し、フォトサポートなしでは720p と360p のプレビューのみを許可します。

カスタムプロファイルを定義する場合は、同じ構文を使用できますが、プロファイル名はカスタムプロファイルの GUID ID に置き換えられます。

```reg
<Device Interface
Node>{3074C75C-1D69-4A0A-895D-EB9EFDE1CF30},0\PINNAME_VIDEO_PREVIEW

MediaCount: REG_DWORD: 2
Media0: REG_SZ: 1280,720,30,1,0,0,0,0,0
Media1: REG_SZ: 640,360,30,1,0,0,0,0,0

<Device Interface
Node>{3074C75C-1D69-4A0A-895D-EB9EFDE1CF30},0\PINNAME_VIDEO_CAPTURE
MediaCount: REG_DWORD: 2
Media0: REG_SZ: 1280,720,30,1,0,0,0,0,0
Media2: REG_SZ: 640,360,30,1,0,0,0,0,0

<Device Interface
Node>{3074C75C-1D69-4A0A-895D-EB9EFDE1CF30},0\PINNAME_IMAGE
MediaCount: REG_DWORD: 2
Media0: REG_SZ: 1920,1080,0,0,0,0,0,0,0
Media1: REG_SZ: 1280,720,0,0,0,0,0,0,0
```

レジストリに対する変更は、OEM に適した方法で処理できます。 カメラのインストール中にレジストリエントリを作成できるように、カメラドライバーの INF ファイルに AddReg セクションを作成することをお勧めします (ドライバーが削除されたときに削除されます)。

```INF
[SampleDriver.DeviceInterface.AddReg]
HKR,,”OEMCameraProfiles”,0,”KSCAMERAPROFILE_VideoRecording,0”,
HKR,”KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW”,”MediaCount”,0x00010001,2,
HKR,”KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW”,”Media0”,0,”1280,720,30,1,0,0,0,0,0”,
HKR,”KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW”,”Media1”,0,”640,360,30,1,0,0,0,0,0”,
```

…

### <a name="inf-profile--concurrency"></a>INF プロファイル:コンカレンシー

プロファイルの同時実行設定を公開するには、次のレジストリ値を追加することができます。

```reg
<Device Interface Node>KSCAMERAPROFILE_VideoConferencing,0

Concurrency: REG_SZ:
{ConcurrentDeviceReferenceGUID};{ProfileID},{Index};…
```

ConcurrentDeviceRefefenceGUID は、このプロファイルが同時に実行さ\_れる可能性のある、カメラに関連付けられている ksk フィルター記述子の referenceguid です。

### <a name="example-inf"></a>INF の例

```INF
;---------------------------------------------------------------
; S t r i n g s
;---------------------------------------------------------------

[Strings]
; non-localizable
RefGUIDFrontCamera="{C3FDE193-01D1-4A78-AA0F-0D2395611C3D}"
RefGUIDRearCamera="{3E5169E8-8DB8-4951-A33F-CFF94F2C87BE}"

;---------------------------------------------------------------
; A d d R e g
;---------------------------------------------------------------

[SampleDriver.FrontCameraInterface.AddReg]
HKR,,"OEMCameraProfiles",0,"KSCAMERAPROFILE_VideoRecording;KSCAMERAPROFILE_VideoConferencing;KSCAMERAPROFILE_HighQualityPhoto;KSCAMERAPROFILE_PhotoSequence",
HKR,,"ReferenceGUID",0,%RefGUIDFrontCamera%
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW","MediaCount",0x00010001,2,
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW","Media0",0,"1280,720,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW","Media1",0,"640,360,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_CAPTURE","MediaCount",0x00010001,2,
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_CAPTURE","Media0",0,"1280,720,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_CAPTURE","Media1",0,"640,360,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_PhotoSequence,0","Disabled",0x00010001,1,
HKR,"KSCAMERAPROFILE_HighQualityPhoto,0\PINNAME_VIDEO_PREVIEW","Media0",0,"1280,720,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_HighQualityPhoto,0\PINNAME_VIDEO_PREVIEW","Media1",0,"640,360,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_HighQualityPhoto,0\PINNAME_IMAGE","MediaCount",0x00010001,2,
HKR,"KSCAMERAPROFILE_HighQualityPhoto,0\PINNAME_IMAGE","Media0",0,"1920,1080,0,0,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_HighQualityPhoto,0\PINNAME_IMAGE","Media1",0,"1280,720,5,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_PREVIEW","MediaCount",0x00010001,2,
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_PREVIEW","Media0",0,"1280,720,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_PREVIEW","Media1",0,"640,360,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_CAPTURE","MediaCount",0x00010001,2,
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_CAPTURE","Media0",0,"1280,720,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_CAPTURE","Media1",0,"640,360,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoConferencing,0","Concurrency",0,"%RefGUIDRearCamera%;KSCAMERAPROFILE_VideoConferencing,0",
```

上記の INF のサンプルセクションでは、と OEM がプロファイルの既定の IHV 設定を発行 (または上書き) する方法を示しています。 上のサンプルでは、フロントカメラの0番目のインデックス付き VideoRecording が、プレビューとレコードの両方について、写真をサポートしていないことに制限されています。

フロントカメラの PhotoSequence も無効になります (IHV の発行済みプロファイルを上書きします)。

HighQualityPhoto profile は、1080p のシングルショットまたは720p の写真 (5fps) で 720p preview に限定されています。

ビデオ会議プロファイルは、プレビューとキャプチャの両方に対して1つだけに制限されており、背面のカメラのビデオ会議プロファイルで同時に実行できることを示しています (背面カメラのビデオ会議プロファイルは INF に表示されません)。INF で指定されている場合、背面カメラのビデオ会議プロファイルは、発行されたすべての IHV を使用します。存在しない場合は、上記の上書きが無効であるため、プロファイルは無効になります。

## <a name="inf-vs-ks-api-profile"></a>INF とKS API プロファイル

INF プロファイル情報は、常に KS API によって発行されたプロファイル情報よりも優先されます。 優先順位は、プロファイルごとのレベルにあります。

ドライバーが VideoRecording、HighQualityPhoto、KS API を使用してビデオ会議プロファイルを発行し、INF 設定に HighQualityPhoto のプロファイルエントリが含まれている場合、ドライバーによって発行された HighQualityPhoto プロファイルのみが、INF からのプロファイル情報。

これは、1つの参照ドライバー (IHV によって実装される) が特定のセンサーで使用可能なプロファイルのセットを公開することを想定して行われますが、OEM は別のセンサーを選択するか、最終的なフォームファクターによって、変更または制限することを選択できます。使用可能なプロファイル。

また、INF プロファイルを使用すると、ドライバーバイナリを変更することなく Oem は、INF を更新するだけで既存の Windows 8.1 ドライバーのプロファイルを発行できます。
