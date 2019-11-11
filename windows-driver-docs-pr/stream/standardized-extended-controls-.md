---
title: 拡張カメラ コントロール
description: 拡張コントロールは、KSK プロパティ機構を使用して、カメラコントロールをアプリケーションに公開します。
ms.assetid: B480C007-7DCA-4CFB-9169-BE2D0B2D2137
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4ad1343a95f3f1678168995577e530f8f864930
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837693"
---
# <a name="extended-camera-controls"></a>拡張カメラ コントロール

拡張コントロールは、 **Ksk プロパティ**機構を使用して、カメラコントロールをアプリケーションに公開します。

(メディアファンデーションによって定義された) 次の標準化された拡張コントロールの一覧では、追加の Windows カメラ機能が有効になります。

- [Metadata](#metadata)
- [優先順位](#focus-priority)
- [フォーカス状態](#focus-state)
- [対象となる拡張領域 (ROI)](#extended-region-of-interest-roi)
- [写真の確認](#photo-confirmation)
- [フォトシーケンスサブモード](#photo-sequence-submode)
- [EXIF および HW JPEG エンコーダー](#exif-and-hw-jpeg-encoder)
- [整数 ISO](#integer-iso)
- [高度なフォーカス](#advanced-focus)
- [『](#flash)
- [倍率](#zoom)
- [シーンモード](#scene-mode)

一部のコントロールは非同期コントロールとしてアプリケーションに公開され、他のコントロールは同期コントロールとして公開されます。

## <a name="synchronous-controls"></a>同期コントロール

これらのコントロールでは、キャプチャパイプラインは**Ksk プロパティ**のカメラコントロール構造を発行し、ドライバーが同期的に要求を返すことを想定しています。

## <a name="asynchronous-controls"></a>非同期コントロール

これらのコントロールの場合、キャプチャパイプラインは**Ksk プロパティ**を発行し、そのプロパティに関連付けられた**KSEVENT**を有効にして、イベントを待機してシグナル状態にします。 ドライバーは**Ksk プロパティ**を同期的に完了し、それをトリガーとして使用して非同期操作を開始する必要があります。 非同期操作の完了時に、ドライバーは、キャプチャパイプラインが待機している関連する**KSEVENT**を通知する必要があります。 キャプチャパイプラインは、シグナルを受信したときの操作の完了をアプリケーションに通知します。

非同期コントロールをキャンセルできる場合は、コントロールの**CANCELOPERATION\_KSCAMERA\_EXTENDEDPROP\_フラグ**を指定する必要があります。 コントロールをキャンセルできない場合、コントロールの操作は5ミリ秒を超えることはできません。

これらの拡張コントロールは、ksmedia. h で定義されている次の KS プロパティセットの一部です。

```cpp
#define STATIC_KSPROPERTYSETID_ExtendedCameraControl \
     0x1CB79112, 0xC0D2, 0x4213, 0x9C, 0xA6, 0xCD, 0x4F, 0xDB, 0x92, 0x79, 0x72
DEFINE_GUIDSTRUCT("1CB79112-C0D2-4213-9CA6-CD4FDB927972", KSPROPERTYSETID_ExtendedCameraControl);
#define KSPROPERTYSETID_ExtendedCameraControl DEFINE_GUIDNAMED(KSPROPERTYSETID_ExtendedCameraControl);
```

## <a name="metadata"></a>メタデータ

メタデータを取得するには、ユーザーモードコンポーネント (DevProxy) がドライバーにメタデータバッファー要件を照会する必要があります。 ユーザーモードコンポーネントがこの情報を取得すると、ドライバーが入力してユーザーモードコンポーネントに返すための適切なメタデータバッファーが割り当てられます。

Ksk プロパティ[ **\_CAMERACONTROL\_拡張\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-metadata)プロパティ ID で定義されている、 [**KSK プロパティ\_CAMERACONTROL\_拡張\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙型のクエリを実行するためにクライアントによって使用されます。メタデータバッファー割り当てのために必要なメタデータのサイズ、メモリアラインメントの要件、必要なメモリ割り当ての種類などのメタデータバッファー要件。

ユーザーモードコンポーネントがドライバーからメタデータバッファー要件を取得すると、適切にサイズ設定されたメタデータバッファーが、目的のメモリプールから必要なメモリアラインメントに割り当てられます。 このメタデータバッファーは、実際のフレームバッファーと共にドライバーに送信され、満たされた後、ユーザーモードコンポーネントがいっぱいになったときに戻されます。 マルチショットのシナリオでは、割り当てられた各フレームバッファーに対応するメタデータバッファーが割り当てられ、カメラドライバーに配信されます。

次のフラグと共に、 [**Ksk ストリーム\_metadata\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_metadata_info)構造体を使用して、メタデータバッファーをドライバーに送信します。

```cpp
#define KSSTREAM_HEADER_OPTIONSF_METADATA           0x00001000
```

バッファー (メタデータ + フレーム) がドライバーのキューに登録されると、DevProxy は標準の[**Ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造体を送信し、その後に[**KS\_frame\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)構造体を送信し、その後に**ksk ストリーム\_メタデータを送信し\_INFO**構造体。 DevProxy は **、Ksk ストリーム\_ヘッダーにさらにマスクします。オプションフラグ**を**ksk ストリーム\_ヘッダー\_オプション**を使用して、バッファーをドライバーに渡す前にメタデータを\_します。

ドライバーがメタデータをサポートしていない場合、または**拡張\_メタデータ\_Ksk プロパティ\_CAMERACONTROL**が実装されていない場合、 **KSPROPERTY\_CAMERACONTROL\_拡張\_メタデータ**プロパティコントロールになります。は失敗します。 この場合、DevProxy はメタデータバッファーを割り当てません。また、DevProxy からドライバーに渡されたペイロードには、 **Ksk ストリーム\_メタデータ\_情報**構造体が含まれません。

ドライバーがメタデータをサポートしており、クライアントがメタデータを必要としない場合、DevProxy は、バッファーをドライバーに送信するときに、メタデータバッファーを割り当てず、または**Ksk ストリーム\_メタデータ\_情報**を渡しません。 この動作により、アプリが特定の pin でメタデータを必要としない場合に、不要なメタデータのメモリ割り当てが減少します。

次の構造体は、メタデータバッファー内のカメラドライバーによって格納されるメタデータ項目のレイアウトを示します。

- [**KSCAMERA\_MetadataId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_metadataid)
- [**ITEMHEADER\_KSCAMERA\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)
- [**KSCAMERA\_メタデータ\_PHOTOCONFIRMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)

次の一覧には、メタデータ項目のレイアウトが含まれています。 これは8バイトでアラインされている必要があります。

- [**ITEMHEADER\_KSCAMERA\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)
- メタデータ

画像確認メタデータは、 **Metadataid\_photoconfirmation**で識別されます。 表示されている場合は、関連付けられているプレビューフレームがフォト確認フレームであることを示します。 フォト確認メタデータは、DevProxy によって解析されます。

カスタムメタデータは、 **metadataid\_カスタム\_の開始**から開始する**metadataid**によって識別されます。 カスタムメタデータ項目にはメタデータの blob を含めることができます。これは、プレビューピン、EXIF、またはイメージ pin の OEM メタデータに対して検出された、フォーカス状態や顔になります。 カスタム blob の正確な形式は、ドライバーと MFT0 を実装する OEM によって決まります。 MFT0 は、カスタム blob を解析し、CaptureMetadata 属性バッグ **\_** の下にグループ化された属性として各メタデータ項目をアタッチする役割を果たします。この形式は、MF のキャプチャパイプラインと WinRT で読み取ることができます。

次の IMFAttributes は、 **mfapi .h**で定義されています。 これらは、MF キャプチャパイプラインおよび WinRT で必要です。 MFT0 は、フォト確認フレームが DevProxy を超えてフローしないため、フォト確認用の IMFAttributes を設定しないことに注意してください。

| 属性 (GUID)                            | データの種類 |
|---------------------------------------------|-----------|
| **MF\_キャプチャ\_のメタデータ\_FOCUSSTATE**       | UINT32    |
| **MF\_キャプチャ\_のメタデータ\_FACEROIS**         | バイナリ      |
| **MF\_\_メタデータ\_フレーム\_RAWSTREAM のキャプチャ** | IUnknown  |

**MF\_CAPTURE\_メタデータ\_フレーム\_RAWSTREAM** imfattributes が作成され、IMFMediaBuffer へのポインターが含まれている devproxy によって**CaptureMetadata\_** にアタッチされます。未加工のメタデータバッファーに関連付けられたインターフェイス (**Ksk ストリーム\_メタデータ\_情報。データ**)。

MFT0 は IMFSample を受け取ると、 **MF\_CAPTURE\_メタデータ\_フレーム\_RAWSTREAM**から生のメタデータバッファーを取得し、フォーカス状態などの追加のカスタムメタデータ項目を解析してに変換します。上記で定義されている対応する IMFAttributes は、CaptureMetadata 属性バッグ\_、それを**Mfsampleextension**にアタッチします。
次の IMFAttributes は、MF パイプラインおよびサードパーティ提供の MFTs によって引き継がれる必要があります。

| 名前                                           | 種類                          |
|------------------------------------------------|-------------------------------|
| **CaptureMetadata の MFSampleExtension\_**         | **IUnknown** (imfattributes)  |
| **MFSampleExtension\_EOS**                     | **UINT32** (ブール値)          |
| **MFSampleExtension\_PhotoThumbnail**          | **IUnknown** (IMFMediaBuffer) |
| **PhotoThumbnailMediaType の MFSampleExtension\_** | **IUnknown** (imfmediatype)   |

生のメタデータバッファーにアクセスするために、MFT0 は次のことを行います。

1. は、属性バッグの Imfsample インターフェイスを取得するために IMFSample インターフェイスから CaptureMetadata を使用して、 **Mfsampleextension extension**で認識されている**getunknown**呼び出します。\_
2. IMFMediaBufferインターフェイスを取得するために、前の手順で取得した IMFAttributes インターフェイスから **\_メタデータ\_フレーム\_rawstream の\_をキャプチャ**します。
3. ロックを呼び出して、IMFMediaBuffer に関連付けられている未加工のメタデータバッファーを取得します。

CaptureMetadata attribute bag\_、必要な IMFAttributes を**Mfsampleextension**に追加すると、MFT0 は次のことを実行します。

1. は、属性バッグの Imfsample インターフェイスを取得するために IMFSample インターフェイスから CaptureMetadata を使用して、 **Mfsampleextension extension**で認識されている**getunknown**呼び出します。\_
2. 上の表で指定されている GUID とデータ型に基づいて、前の手順で取得した IMFAttributes インターフェイスから、 **SetUINT32**、 **setblob**、または**setblob**を、 **MF\_\_\_** を呼び出します.

### <a name="mandatory-metadata-attributes"></a>必須のメタデータ属性

利用可能なメタデータ属性の完全な一覧については、「 [Capture Stats Metadata attributes](mf-capture-metadata.md) 」を参照してください。

## <a name="focus-priority"></a>優先順位

FOCUSPRIORITY プロパティ ID [ **\_\_\_Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focuspriority)は、フォーカス優先度 DDI に関連付けられている唯一のコントロールです。

## <a name="focus-state"></a>フォーカス状態

FOCUSSTATE プロパティ ID [ **\_\_\_Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusstate)は、フォーカス状態 DDI に関連付けられている唯一のコントロールです。

## <a name="extended-region-of-interest-roi"></a>目標とする ROI の拡張領域

次のプロパティ Id は、ROI DDI に関連付けられているコントロールです。

- [**KSK プロパティ\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-roi-configcaps)

- [**KSK プロパティ\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-roi-ispcontrol)

## <a name="photo-confirmation"></a>写真の確認

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_photoconfirmation**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoconfirmation)プロパティ ID は、フォト確認 DDI に関連付けられている唯一のコントロールです。

## <a name="photo-sequence-submode"></a>フォトシーケンスサブモード

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)プロパティ ID は、フォトシーケンス DDI に関連付けられている唯一のコントロールです。

## <a name="exif-and-hw-jpeg-encoder"></a>EXIF および HW JPEG エンコーダー

このパイプラインでは、ハードウェア JPEG エンコーダーの EXIF データを処理またはワープする必要はありません。そのため、EXIF データ形式は driver、MFT0、および OEM HW JPEG encoder によって提供されます。 Oem パートナーは、EXIF 属性のカスタム属性 GUID とバリアント型を定義して、それを**CaptureMetaData** attribute バッグ\_にアタッチし、oem コンポーネントが使用できるようにすることができます。 ハードウェア JPEG エンコーダーが使用可能な場合、パイプラインのフォトシンクコンポーネントは、HW JPEG エンコーダーを読み込み、CaptureMetaData attribute バッグに保持されている EXIF データを、属性バッグ **\_** に設定します。これは、 [IPropertyBag2:: Write](https://go.microsoft.com/fwlink/?LinkId=331589)メソッド。

エンコーダーオプションのプロパティバッグには、使用可能なエンコードオプションのプロパティを指定する PROPBAG2 構造体の配列が含まれています。 ハードウェア JPEG エンコーダーに設定されている EXIF エンコーダーオプションは、encoder option プロパティバッグの次のプロパティによって識別されます。

| プロパティ名      | VARTYPE         | Value                                                                                                                                                       | 適用可能なコーデック |
|--------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| **SampleMetaData** | **VT\_不明** | EXIF データを含む OEM サブ属性を含む CaptureMetaData attribute bag **\_** の IMFAttributes インターフェイスへのポインター。 | JPEG              |

CaptureMetaData 属性バッグ **\_の Mfsampleextension**には、MFT0 および HW JPEG エンコーダーが exif データを保持するために読み取ることができる OEM 定義の EXIF サブ属性のみを含めることができます。 ドライバーからハードウェア JPEG エンコーダーに EXIF データを渡すには、ドライバーと MFT0 は次の操作を行う必要があります。

1. このドライバーは、パイプラインによって提供されるメタデータバッファーにカスタム EXIF メタデータを提供します。 これは、サンプルが DevProxy に返されたときに、DevProxy によって **\_メタデータ\_フレーム\_RAWSTREAM** imfattribute によってキャプチャされる\_ **\_、mfsampleextension**に関連付けられています。

2. MFT0 は IMFSample を受信すると、\_MF から未加工のメタデータバッファーを取得し、 **\_フレーム\_RAWSTREAM\_のメタ**データをキャプチャして、カスタム EXIF メタデータ項目を解析し、それを OEM によって定義された Imfsample に変換して、にアタッチします。**Mfsampleextension\_CaptureMetadata**属性バッグです。

MFT0 から HW JPEG エンコーダーに EXIF データを渡すために、パイプラインの写真シンクは次の処理を実行します。

1. IMFSample を受信したときに属性バッグの Imfsample インターフェイスを取得する**ために、** **Mfsampleextension extension で CaptureMetadata**を呼び出します。\_

2. [IPropertyBag2:: Write](https://go.microsoft.com/fwlink/?LinkId=331589)を呼び出して、SampleMetadata によって識別されるエンコーダーオプションプロパティを HW JPEG エンコーダーに設定します。 エンコーダオプションプロパティには、前の手順で取得した IMFAttributes インターフェイスが含まれています。 このインターフェイスには、OEM EXIF サブ属性を含むすべてのカスタムサブ属性と、このトピックで既に説明した**メタデータ**セクションの標準化されたサブ属性が含まれています。

さらに処理するために EXIF データを取得するために、HW JPEG エンコーダーは次の処理を実行します。

1. **IPropertyBag2:: Read**を呼び出して、SampleMetadata プロパティ名と**VT\_不明な**型で識別されるプロパティのプロパティ値を取得します。 PunkVal は、返された場合、 **CaptureMetadata\_** のの imfattributes インターフェイスを受け取ります。

2. Oem exif サブ属性の GUID とデータ型に基づいて EXIF データ blob を取得するために、前の手順で取得したインターフェイスから、OEM EXIF サブ属性に対して**Getblob**または**getunknown**を呼び出します。

## <a name="thumbnail"></a>Thumbnail

MFT0 は、カメラドライバーのサムネイルを生成するためには必要ありません。 カメラアプリは、独自のサムネイルを生成することが想定されています。 サムネイルは、写真の確認画像、HW JPEG エンコーダー、またはフルサイズのイメージのサイズ変更から生成されます。 これはアプリの開発者にとってです。 Windows 8.1 アプリとの API およびアプリの互換性を維持するには、カメラドライバーが **\_CAMERACONTROL\_拡張\_PHOTOTHUMBNAIL コントロールに Ksk プロパティ**を実装してはなりません。

## <a name="integer-iso"></a>整数 ISO

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_iso\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso-advanced)プロパティ ID は、整数 ISO DDI に関連付けられている唯一の制御です。

## <a name="advanced-focus"></a>高度なフォーカス

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_FOCUSMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)プロパティ ID は、整数 ISO DDI に関連付けられている唯一の制御です。

## <a name="flash"></a>Flash

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_FLASHMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)プロパティ ID は、flash DDI に関連付けられている唯一の制御です。

## <a name="zoom"></a>ズーム

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_zoom**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-zoom)プロパティ ID は、zoom DDI に関連付けられている唯一のコントロールです。

## <a name="scene-mode"></a>シーンモード

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_SCENEMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode)プロパティ ID は、シーンモード DDI に関連付けられている唯一のコントロールです。
