---
title: 拡張カメラ コントロール
description: 拡張コントロールは、KSK プロパティ機構を使用して、カメラコントロールをアプリケーションに公開します。
ms.assetid: B480C007-7DCA-4CFB-9169-BE2D0B2D2137
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e41705876d0bcd6f910a54f9f1cd7443a40dbab7
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565600"
---
# <a name="extended-camera-controls"></a>拡張カメラ コントロール

拡張コントロールは、 **Ksk プロパティ**機構を使用して、カメラコントロールをアプリケーションに公開します。

(メディアファンデーションによって定義された) 次の標準化された拡張コントロールの一覧では、追加の Windows カメラ機能が有効になります。

- [メタデータ](#metadata)
- [優先順位](#focus-priority)
- [フォーカス状態](#focus-state)
- [対象となる拡張領域 (ROI)](#extended-region-of-interest-roi)
- [写真の確認](#photo-confirmation)
- [フォトシーケンスサブモード](#photo-sequence-submode)
- [EXIF および HW JPEG エンコーダー](#exif-and-hw-jpeg-encoder)
- [整数 ISO](#integer-iso)
- [高度なフォーカス](#advanced-focus)
- [『](#flash)
- [[ズーム]](#zoom)
- [シーンモード](#scene-mode)

一部のコントロールは非同期コントロールとしてアプリケーションに公開され、他のコントロールは同期コントロールとして公開されます。

## <a name="synchronous-controls"></a>同期コントロール

これらのコントロールでは、キャプチャパイプラインは**Ksk プロパティ**のカメラコントロール構造を発行し、ドライバーが同期的に要求を返すことを想定しています。

## <a name="asynchronous-controls"></a>非同期コントロール

これらのコントロールの場合、キャプチャパイプラインは**Ksk プロパティ**を発行し、そのプロパティに関連付けられた**KSEVENT**を有効にして、イベントを待機してシグナル状態にします。 ドライバーは**Ksk プロパティ**を同期的に完了し、それをトリガーとして使用して非同期操作を開始する必要があります。 非同期操作の完了時に、ドライバーは、キャプチャパイプラインが待機している関連する**KSEVENT**を通知する必要があります。 キャプチャパイプラインは、シグナルを受信したときの操作の完了をアプリケーションに通知します。

非同期コントロールをキャンセルできる場合は、コントロールで**KSCAMERA\_extendedprop\_フラグ\_CANCELOPERATION**フラグを指定する必要があります。 コントロールをキャンセルできない場合、コントロールの操作は5ミリ秒を超えることはできません。

これらの拡張コントロールは、ksmedia. h で定義されている次の KS プロパティセットの一部です。

```cpp
#define STATIC_KSPROPERTYSETID_ExtendedCameraControl \
     0x1CB79112, 0xC0D2, 0x4213, 0x9C, 0xA6, 0xCD, 0x4F, 0xDB, 0x92, 0x79, 0x72
DEFINE_GUIDSTRUCT("1CB79112-C0D2-4213-9CA6-CD4FDB927972", KSPROPERTYSETID_ExtendedCameraControl);
#define KSPROPERTYSETID_ExtendedCameraControl DEFINE_GUIDNAMED(KSPROPERTYSETID_ExtendedCameraControl);
```

## <a name="metadata"></a>メタデータ

メタデータを取得するには、ユーザーモードコンポーネント (DevProxy) がドライバーにメタデータバッファー要件を照会する必要があります。 ユーザーモードコンポーネントがこの情報を取得すると、ドライバーが入力してユーザーモードコンポーネントに返すための適切なメタデータバッファーが割り当てられます。

Ksproperty [ **\_\_CAMERACONTROL拡張プロパティに定義されているCAMERACONTROL\_拡張メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-metadata)プロパティ ID [ **\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙体は、メタデータバッファー割り当てのために必要なメタデータのサイズ、メモリアラインメントの要件、必要なメモリ割り当ての種類などのメタデータバッファー要件を照会するために、クライアントによって使用されます。

ユーザーモードコンポーネントがドライバーからメタデータバッファー要件を取得すると、適切にサイズ設定されたメタデータバッファーが、目的のメモリプールから必要なメモリアラインメントに割り当てられます。 このメタデータバッファーは、実際のフレームバッファーと共にドライバーに送信され、満たされた後、ユーザーモードコンポーネントがいっぱいになったときに戻されます。 マルチショットのシナリオでは、割り当てられた各フレームバッファーに対応するメタデータバッファーが割り当てられ、カメラドライバーに配信されます。

次のフラグと共に[**ksk ストリーム\_\_メタデータ情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_metadata_info)の構造を使用して、メタデータバッファーをドライバーに送信します。

```cpp
#define KSSTREAM_HEADER_OPTIONSF_METADATA           0x00001000
```

バッファー (メタデータ + フレーム) がドライバーのキューに登録されると、devproxy は標準の[**ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)構造を送信し、その後に[**KS\_フレーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info)構造を送信し、その後に**ksk ストリーム\_を送信します。メタデータ\_情報**の構造。 Devproxy は、さらに**ksk\_ストリームヘッダーをマスクします。オプションフラグ**を**ksk ストリーム\_ヘッダー\_オプション\_** を使用して、バッファーをドライバーに渡します。

ドライバーがメタデータをサポートしていない場合、または**ksk プロパティ\_CAMERACONTROL\_拡張\_メタデータ**が実装されていない場合は、 **ksk プロパティ\_CAMERACONTROL\_が拡張\_されます。メタデータ**プロパティコントロールは失敗します。 この場合、devproxy はメタデータバッファーを割り当てません。また、devproxy からドライバーに渡されたペイロードには、 **ksk ストリーム\_メタ\_データ情報**の構造体が含まれません。

ドライバーがメタデータをサポートし、クライアントがメタデータを必要としない場合、devproxy は、バッファーをドライバーに送信するときに、メタデータバッファーを割り当てず、 **ksk ストリーム\_\_メタデータ情報**を渡しません。 この動作により、アプリが特定の pin でメタデータを必要としない場合に、不要なメタデータのメモリ割り当てが減少します。

次の構造体は、メタデータバッファー内のカメラドライバーによって格納されるメタデータ項目のレイアウトを示します。

- [**KSCAMERA\_metadataid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-kscamera_metadataid)
- [**KSCAMERA\_METADATA\_ITEMHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)
- [**KSCAMERA\_メタ\_データ PHOTOCONFIRMATION 確認**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)

次の一覧には、メタデータ項目のレイアウトが含まれています。 これは8バイトでアラインされている必要があります。

- [**KSCAMERA\_METADATA\_ITEMHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)
- メタデータ

画像確認メタデータは、 **metadataid\_photoconfirmation**によって識別されます。 表示されている場合は、関連付けられているプレビューフレームがフォト確認フレームであることを示します。 フォト確認メタデータは、DevProxy によって解析されます。

カスタムメタデータは、 **metadataid\_カスタム\_スタート**から開始する**metadataid**によって識別されます。 カスタムメタデータ項目にはメタデータの blob を含めることができます。これは、プレビューピン、EXIF、またはイメージ pin の OEM メタデータに対して検出された、フォーカス状態や顔になります。 カスタム blob の正確な形式は、ドライバーと MFT0 を実装する OEM によって決まります。 MFT0 は、カスタム blob を解析し、各メタデータ項目を、 **mfsampleextension\_CaptureMetadata**属性バッグの下にグループ化された属性として、MF のキャプチャパイプラインおよび/または WinRT で読み取り可能な形式でアタッチします。

次の IMFAttributes は、 **mfapi .h**で定義されています。 これらは、MF キャプチャパイプラインおよび WinRT で必要です。 MFT0 は、フォト確認フレームが DevProxy を超えてフローしないため、フォト確認用の IMFAttributes を設定しないことに注意してください。

| 属性 (GUID)                            | データの種類 |
|---------------------------------------------|-----------|
| **MF\_キャプチャ\_メタデータ\_FOCUSSTATE**       | UINT32    |
| **MF\_キャプチャ\_メタデータ\_FACEROIS**         | Blob      |
| **MF\_キャプチャ\_メタデータ\_フレーム\_RAWSTREAM** | IUnknown  |

**MF\_キャプチャメタ\_データ\_フレームrawstreamimfattributesが作成され、devproxyによってCaptureMetadataにアタッチされます。この拡張機能には、\_** **\_** 生のメタデータバッファーに関連付けられている IMFMediaBuffer インターフェイスへのポインター (**ksk ストリーム\_メタ\_データ情報)。データ**)。

MFT0 は imfsample を受け取ると、 **MF\_キャプチャ\_メタデータ\_\_フレーム rawstream**から生のメタデータバッファーを取得し、フォーカス状態などの追加のカスタムメタデータ項目を解析します。は、上記で定義されている対応する imfattributes に変換し、それらを**mfsampleextension\_CaptureMetadata**属性バッグに添付します。
次の IMFAttributes は、MF パイプラインおよびサードパーティ提供の MFTs によって引き継がれる必要があります。

| 名前                                           | 種類                          |
|------------------------------------------------|-------------------------------|
| **Mfsampleextension\_CaptureMetadata**         | **IUnknown**(IMFAttributes)  |
| **Mfsampleextension\_EOS**                     | **UINT32**演算          |
| **Mfsampleextension\_photothumbnail**          | **IUnknown**(IMFMediaBuffer) |
| **Mfsampleextension\_PhotoThumbnailMediaType** | **IUnknown**(IMFMediaType)   |

生のメタデータバッファーにアクセスするために、MFT0 は次のことを行います。

1. Imfsample インターフェイスから、属性バッグの imfsample インターフェイスを取得するために、 **CaptureMetadata\_** で**既知の getunknown**を呼び出します。
2. IMFMediaBuffer インターフェイスを取得するために、前の手順で取得した imfattributes インターフェイスから、 **\_\_\_MF\_** によって認識される**getunknown**呼び出します。
3. ロックを呼び出して、IMFMediaBuffer に関連付けられている未加工のメタデータバッファーを取得します。

必要な imfattributes を**mfsampleextension\_CaptureMetadata**属性バッグに追加すると、MFT0 は次のことを実行します。

1. Imfsample インターフェイスから、属性バッグの imfsample インターフェイスを取得するために、 **CaptureMetadata\_** で**既知の getunknown**を呼び出します。
2. 指定された GUID とデータ型に基づいて、前の手順で取得した imfattributes インターフェイスから、**メイン\_フレームキャプチャ\_\_メタデータ XXX**の**SetUINT32**、 **setblob**、または**setblob**を呼び出します。上の表を例に示します。

### <a name="mandatory-metadata-attributes"></a>必須のメタデータ属性

利用可能なメタデータ属性の完全な一覧については、「 [Capture Stats Metadata attributes](mf-capture-metadata.md) 」を参照してください。

## <a name="focus-priority"></a>優先順位

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDEDFOCUSPRIORITYプロパティIDは、フォーカス優先度DDIに関連付けられている唯一のコントロールです。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focuspriority)

## <a name="focus-state"></a>フォーカス状態

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDEDFOCUSSTATEプロパティIDは、フォーカス状態DDIに関連付けられている唯一のコントロールです。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusstate)

## <a name="extended-region-of-interest-roi"></a>目標とする ROI の拡張領域

次のプロパティ Id は、ROI DDI に関連付けられているコントロールです。

- [**KSK プロパティ\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-roi-configcaps)

- [**KSK プロパティ\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-roi-ispcontrol)

## <a name="photo-confirmation"></a>写真の確認

[**Ksk プロパティ\_CAMERACONTROL\_拡張photoconfirmationプロパティIDは、フォト確認DDIに関連付けられている唯一のコントロールです。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoconfirmation)

## <a name="photo-sequence-submode"></a>フォトシーケンスサブモード

[**Ksk プロパティ\_CAMERACONTROL\_拡張photomodeプロパティIDは、フォトシーケンスDDIに関連付けられている唯一のコントロールです。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)

## <a name="exif-and-hw-jpeg-encoder"></a>EXIF および HW JPEG エンコーダー

このパイプラインでは、ハードウェア JPEG エンコーダーの EXIF データを処理またはワープする必要はありません。そのため、EXIF データ形式は driver、MFT0、および OEM HW JPEG encoder によって提供されます。 Oem パートナーは、EXIF 属性のカスタム属性 GUID とバリアント型を定義し、それを **\_CaptureMetaData**属性バッグにアタッチして、oem コンポーネントが使用できるようにすることができます。 ハードウェア jpeg エンコーダーが使用可能な場合、パイプラインのフォトシンクコンポーネントは、ハードウェア jpeg エンコーダーを読み込み、その後、を使用して、 **\_CaptureMetaData**属性バッグに保持されている exif データを exif エンコーダーオプションとして hw jpeg エンコーダーに設定します。[IPropertyBag2:: Write](https://go.microsoft.com/fwlink/?LinkId=331589)メソッド。

エンコーダーオプションのプロパティバッグには、使用可能なエンコードオプションのプロパティを指定する PROPBAG2 構造体の配列が含まれています。 ハードウェア JPEG エンコーダーに設定されている EXIF エンコーダーオプションは、encoder option プロパティバッグの次のプロパティによって識別されます。

| プロパティ名      | VARTYPE         | 値                                                                                                                                                       | 適用可能なコーデック |
|--------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| **SampleMetaData** | **VT\_不明** | EXIF データを含む OEM サブ属性を含む、 **mfsampleextension\_CaptureMetaData**属性バッグの imfattributes インターフェイスへのポインター。 | JPEG              |

**Mfsampleextension\_CaptureMetaData**属性バッグには、MFT0 および HW JPEG エンコーダーが exif データを保持するために読み取ることができる OEM 定義の exif サブ属性のみを含めることができます。 ドライバーからハードウェア JPEG エンコーダーに EXIF データを渡すには、ドライバーと MFT0 は次の操作を行う必要があります。

1. このドライバーは、パイプラインによって提供されるメタデータバッファーにカスタム EXIF メタデータを提供します。 これは、サンプルが返されたときに、devproxy によって、 **mfsampleextension\_CaptureMetadata** **\_\_\_\_** に関連付けられます。DevProxy。

2. MFT0 は imfsample を受け取ると、 **MF\_キャプチャ\_メタデータ\_\_フレーム rawstream**から生のメタデータバッファーを取得し、カスタム EXIF メタデータ項目を解析して、OEM 定義に変換します。Imfattribute を行い、それを**mfsampleextension\_CaptureMetadata**属性バッグに添付します。

MFT0 から HW JPEG エンコーダーに EXIF データを渡すために、パイプラインの写真シンクは次の処理を実行します。

1. Imfsample が受信されたときに属性バッグの imfsample インターフェイスを取得するために、imfsample から**CaptureMetadata\_** で**既知の getunknown**を呼び出します。

2. [IPropertyBag2:: Write](https://go.microsoft.com/fwlink/?LinkId=331589)を呼び出して、SampleMetadata によって識別されるエンコーダーオプションプロパティを HW JPEG エンコーダーに設定します。 エンコーダオプションプロパティには、前の手順で取得した IMFAttributes インターフェイスが含まれています。 このインターフェイスには、OEM EXIF サブ属性を含むすべてのカスタムサブ属性と、このトピックで既に説明した**メタデータ**セクションの標準化されたサブ属性が含まれています。

さらに処理するために EXIF データを取得するために、HW JPEG エンコーダーは次の処理を実行します。

1. **IPropertyBag2:: Read**を呼び出して、SampleMetadata プロパティ名と **\_VT UNKNOWN**型によって識別されるプロパティのプロパティ値を取得します。 返された場合、 **punkVal**は、 **\_mfsampleextension CaptureMetadata**の imfattributes インターフェイスを受け取ります。

2. Oem exif サブ属性の GUID とデータ型に基づいて EXIF データ blob を取得するために、前の手順で取得したインターフェイスから、OEM EXIF サブ属性に対して**Getblob**または**getunknown**を呼び出します。

## <a name="thumbnail"></a>サムネイル

MFT0 は、カメラドライバーのサムネイルを生成するためには必要ありません。 カメラアプリは、独自のサムネイルを生成することが想定されています。 サムネイルは、写真の確認画像、HW JPEG エンコーダー、またはフルサイズのイメージのサイズ変更から生成されます。 これはアプリの開発者にとってです。 Windows 8.1 アプリとの API およびアプリの互換性を維持するには、カメラドライバーが**ksk\_プロパティ\_CAMERACONTROL\_拡張 photothumbnail**コントロールを実装してはいけません。

## <a name="integer-iso"></a>整数 ISO

[ **\_Ksk プロパティ CAMERACONTROL\_拡張\_iso詳細プロパティIDは、整数ISODDIに関連付けられている唯一の制御です。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso-advanced)

## <a name="advanced-focus"></a>高度なフォーカス

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDEDFOCUSMODEプロパティIDは、整数ISODDIに関連付けられている唯一の制御です。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)

## <a name="flash"></a>Flash

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDEDFLASHMODEプロパティIDは、flashDDIに関連付けられている唯一のコントロールです。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)

## <a name="zoom"></a>ズーム

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDEDzoomプロパティIDは、zoomDDIに関連付けられている唯一のコントロールです。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-zoom)

## <a name="scene-mode"></a>シーンモード

[**Ksk プロパティ\_CAMERACONTROL\_EXTENDEDSCENEMODEプロパティIDは、シーンモードDDIに関連付けられている唯一のコントロールです。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode)
