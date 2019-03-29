---
title: 拡張カメラ コントロール
description: 拡張コントロールは、アプリケーションにカメラ コントロールを公開するのに KSPROPERTY メカニズムを使用します。
ms.assetid: B480C007-7DCA-4CFB-9169-BE2D0B2D2137
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 663c8ac91121e92633598cd5ce9c86380f72f7d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582685"
---
# <a name="extended-camera-controls"></a>拡張カメラ コントロール


コントロールの使用の拡張、 **KSPROPERTY**カメラ コントロールをアプリケーションを公開するためのメカニズムです。

(Media Foundation によって定義される) 標準の拡張コントロールの次の一覧には、Windows のカメラの追加機能が有効にします。

-   [メタデータ](#metadata)
-   [フォーカスの優先順位](#focus-priority)
-   [フォーカス状態](#focus-state)
-   [拡張 (ROI) の関心領域](#extended-region-of-interest-roi)
-   [写真の確認](#photo-confirmation)
-   [フォト シーケンス サブモード](#photo-sequence-submode)
-   [フォト キャプチャ フィードバックが適用されるデバイスの設定](#photo-capture-feedback-applied-device-settings)
-   [ISO の整数](#integer-iso)
-   [高度なフォーカス](#advanced-focus)
-   [フラッシュ](#flash)
-   [ズーム](#zoom)
-   [シーンのモード](#scene-mode)

コントロールの一部は非同期のコントロールとしてのアプリケーションに公開して、同期コントロールとして他のユーザーに公開されます。

-   **同期コントロール**-キャプチャ パイプラインの問題、これらのコントロールの**KSPROPERTY**カメラ制御構造体とは同期的に要求を返すことが必要です。

-   **非同期コントロール**-キャプチャ パイプラインの問題、これらのコントロールの**KSPROPERTY**、により、 **KSEVENT**に関連付けられて、そのプロパティ、および通知を取得するイベントで発生する待機します。 ドライバーを完了する必要があります、 **KSPROPERTY**同期的に非同期操作を開始するトリガーとして使用するとします。 非同期操作を完了すると、ドライバーは、関連付けられている通知する必要があります**KSEVENT**キャプチャ パイプラインが待機しています。 キャプチャ パイプラインは、シグナルを受信するときに、アプリケーションについて、操作の完了を通知します。

    フラグを指定する必要がありますが、非同期のコントロールをキャンセルできる場合**KSCAMERA\_EXTENDEDPROP\_フラグ\_CANCELOPERATION**コントロール。 コントロールがキャンセルされた場合コントロールの操作が 5 ミリ秒を超えない必要があります。

Ksmedia.h で定義されている次の KS プロパティの一部であるこれらのコントロールを拡張します。

```cpp
#define STATIC_KSPROPERTYSETID_ExtendedCameraControl \
     0x1CB79112, 0xC0D2, 0x4213, 0x9C, 0xA6, 0xCD, 0x4F, 0xDB, 0x92, 0x79, 0x72
DEFINE_GUIDSTRUCT("1CB79112-C0D2-4213-9CA6-CD4FDB927972", KSPROPERTYSETID_ExtendedCameraControl);
#define KSPROPERTYSETID_ExtendedCameraControl DEFINE_GUIDNAMED(KSPROPERTYSETID_ExtendedCameraControl);
```

## <a name="metadata"></a>メタデータ


メタデータを取得するには、ユーザー モード コンポーネント (DevProxy) が必要なメタデータ バッファーのドライバーのクエリを実行する必要があります。 ユーザー モード コンポーネントは、この情報には後、は、ドライバーを入力し、ユーザー モード コンポーネントに戻すの適切なメタデータ バッファーを割り当てます。

[ **KSPROPERTY\_CAMERACONTROL\_拡張\_メタデータ**](https://msdn.microsoft.com/library/windows/hardware/dn917952)で定義されているプロパティ ID、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/dn917962)列挙型がメタデータ バッファー要件は、必要なメタデータのサイズ、メモリのアラインメント要件など、クライアントへのクエリで使用し、メタデータのバッファーの割り当て用のメモリ割り当ての種類が必要です。

ユーザー モード コンポーネントは、ドライバーからメタデータ、バッファーの要件を入手が、目的のメモリ プールから目的のメモリ アラインメント メタデータの適切なサイズのバッファーを割り当てます。 実際のフレーム バッファーと共に、このメタデータのバッファーを満たすために、ドライバーに送信し、いっぱいになると、ユーザー モード コンポーネントにし、返されます。 Multishot のシナリオでは、対応するメタデータのバッファーが割り当てられ、割り当てられた各フレーム バッファーのカメラのドライバーに配信。

[ **KSSTREAM\_メタデータ\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn936959)ドライバーにメタデータのバッファーを送信する構造体には、次のフラグとを使用します。

```cpp
#define KSSTREAM_HEADER_OPTIONSF_METADATA           0x00001000
```

(メタデータ + フレーム) のバッファーは、ドライバーをキューに置かれた、DevProxy 送信標準[ **KSSTREAM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567138)続く構造を[ **KS\_フレーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567645)構造体、および後に、 **KSSTREAM\_メタデータ\_情報**構造体。 DevProxy はさらにマスク**KSSTREAM\_ヘッダー。OptionFlags**で**KSSTREAM\_ヘッダー\_OPTIONSF\_メタデータ**ドライバーにバッファーを渡す前にします。

ドライバーは、メタデータをサポートしていない場合、または場合**KSPROPERTY\_CAMERACONTROL\_拡張\_メタデータ**は実装されていません、 **KSPROPERTY\_CAMERACONTROL\_拡張\_メタデータ**プロパティ コントロールは失敗します。 この場合、DevProxy はメタデータのバッファーを割り当てられません、DevProxy からドライバーに渡されたペイロードにが含まれていない、 **KSSTREAM\_メタデータ\_情報**構造体。

ドライバーは、メタデータをサポートしているクライアントには、すべてのメタデータはしない場合は、DevProxy はメタデータのバッファーの割り当ても渡す**KSSTREAM\_メタデータ\_情報**ドライバーにバッファーを送信するときにします。 この動作は、アプリが与えられた暗証番号 (pin) のメタデータをしない場合に、不要なメタデータのメモリ割り当てを減らします。

次の構造体には、メタデータ、バッファー内のカメラのドライバーが格納されるメタデータ項目のレイアウトについて説明します。

-   [**KSCAMERA\_MetadataId**](https://msdn.microsoft.com/library/windows/hardware/dn925181)

-   [**KSCAMERA\_メタデータ\_ITEMHEADER**](https://msdn.microsoft.com/library/windows/hardware/dn925184)

-   [**KSCAMERA\_METADATA\_PHOTOCONFIRMATION**](https://msdn.microsoft.com/library/windows/hardware/dn925187)

以下の一覧には、メタデータ項目のレイアウトが含まれています。 これには、8 バイトでアラインがあります。

-   [**KSCAMERA\_メタデータ\_ITEMHEADER**](https://msdn.microsoft.com/library/windows/hardware/dn925184)

-   メタデータ

確認の写真のメタデータがで識別される**MetadataId\_PhotoConfirmation**します。 存在する場合、関連付けられている、プレビュー フレームがフォト確認のフレームを示します。 確認の写真のメタデータは、DevProxy によって解析されます。

カスタムのメタデータがで識別される、 **MetadataId**から始まる**MetadataId\_カスタム\_開始**します。 カスタム メタデータ項目は、フォーカスの状態やプレビューの暗証番号 (pin)、EXIF やイメージのピン留めの OEM メタデータの検出された顔可能性のあるメタデータの blob を含めることができます。 カスタムの blob の正確な形式については、ドライバーを実装する OEM と MFT0 によって決まります。 カスタムの blob を解析し、下にグループ化属性として、各メタデータ項目を接続、MFT0 責任を負います、 **MFSampleExtension\_CaptureMetadata** MF キャプチャによって読み取り可能な形式で属性バッグパイプラインや WinRT します。

次の IMFAttributes がで定義されている**mfapi.h**します。 これらは、MF キャプチャ パイプラインや WinRT で必要とします。 MFT0 は設定されていないこと、IMFAttributes フォト確認 DevProxy を超えての写真確認フレームのフローがないので注意してください。

| 属性 (GUID)                            | データ型 |
|---------------------------------------------|-----------|
| **MF\_キャプチャ\_メタデータ\_FOCUSSTATE**       | UINT32    |
| **MF\_キャプチャ\_メタデータ\_FACEROIS**         | Blob      |
| **MF\_キャプチャ\_メタデータ\_フレーム\_RAWSTREAM** | IUnknown  |

 

**MF\_キャプチャ\_メタデータ\_フレーム\_RAWSTREAM** IMFAttributes が作成されに接続されている**MFSampleExtension\_CaptureMetadata**これによって、DevProxy 未処理のメタデータのバッファーに関連付けられた IMFMediaBuffer インターフェイスへのポインターが含まれています (**KSSTREAM\_メタデータ\_情報。データ**)。 MFT0、IMFSample を受信する場合から未処理のメタデータのバッファーを取得します。、 **MF\_キャプチャ\_メタデータ\_フレーム\_RAWSTREAM**し、追加のカスタム メタデータ項目を解析します。変換に対応する IMFAttributes 上で定義およびそれらに接続し、フォーカス状態など、 **MFSampleExtension\_CaptureMetadata**属性バッグ。

未処理のメタデータのバッファーにアクセスするには、MFT0 は、次を行います。

1.  呼び出し**GetUnknown**で**MFSampleExtension\_CaptureMetadata** IMFAttributes インターフェイス、属性のバッグを取得する IMFSample インターフェイスから。

2.  呼び出し**GetUnknown**で**MF\_キャプチャ\_メタデータ\_フレーム\_RAWSTREAM** 、前の手順から取得した IMFAttributes インターフェイスからIMFMediaBuffer インターフェイスを取得します。

3.  IMFMediaBuffer に関連付けられているメタデータの生バッファーを取得するロックを呼び出します。

必要な IMFAttributes を追加する、 **MFSampleExtension\_CaptureMetadata**属性バッグ、MFT0 は次を実行します。

1.  呼び出し**GetUnknown**で**MFSampleExtension\_CaptureMetadata** IMFAttributes インターフェイス、属性のバッグを取得する IMFSample インターフェイスから。

2.  呼び出し**SetUINT32**、 **SetBlob**、または**SetUnknown**で**MF\_キャプチャ\_メタデータ\_XXX**IMFAttributes インターフェイス上の表で指定された GUID とデータの種類に基づいて、前の手順から取得したからです。

## <a name="focus-priority"></a>フォーカスの優先順位


[ **KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSPRIORITY** ](https://msdn.microsoft.com/library/windows/hardware/dn917942)プロパティ ID は、フォーカスの優先度 DDI に関連付けられている唯一のコントロール。

## <a name="focus-state"></a>フォーカス状態


[ **KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSSTATE** ](https://msdn.microsoft.com/library/windows/hardware/dn917944)プロパティ ID はフォーカス状態 DDI に関連付けられている唯一のコントロール。

## <a name="extended-region-of-interest-roi"></a>ROI を関心のある領域を拡張


次のプロパティ Id は、ROI DDI に関連付けられているコントロールです。

-   [**KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS**](https://msdn.microsoft.com/library/windows/hardware/dn917964)

-   [**KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL**](https://msdn.microsoft.com/library/windows/hardware/dn917966)

## <a name="photo-confirmation"></a>写真の確認


[ **KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOCONFIRMATION** ](https://msdn.microsoft.com/library/windows/hardware/dn917957)プロパティ ID は、フォト確認 DDI に関連付けられている唯一のコントロール。

## <a name="photo-sequence-submode"></a>フォト シーケンス サブモード


[ **KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE** ](https://msdn.microsoft.com/library/windows/hardware/dn567582)プロパティ ID は、フォト シーケンス DDI に関連付けられている唯一のコントロール。

## <a name="photo-capture-feedback-applied-device-settings"></a>フォト キャプチャ フィードバックが適用されるデバイスの設定


MFT0 IMFAttributes にドライバーと接続の適用の必要なデバイスの設定によって提供されるメタデータ バッファーの解析、 **MFSampleExtension\_CaptureMetadata**各 IMFSample に関連付けられている属性のバッグ。 MF パイプラインによって次の IMFAttributes を実行する必要があり、任意のサードパーティの仕様を提供します。

| 名前                                           | 型                          |
|------------------------------------------------|-------------------------------|
| **MFSampleExtension\_CaptureMetadata**         | **IUnknown** (IMFAttributes)  |
| **MFSampleExtension\_EOS**                     | **UINT32** (ブール値)          |
| **MFSampleExtension\_PhotoThumbnail**          | **IUnknown** (IMFMediaBuffer) |
| **MFSampleExtension\_PhotoThumbnailMediaType** | **IUnknown** (IMFMediaType)   |

 

**必須のメタデータ属性**

**MFSampleExtension\_CaptureMetaData**はメタデータ属性のバッグを次の属性を持つことができます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_REQUESTED_FRAME_SETTING_ID</strong></td>
<td><strong>UINT32</strong></td>
<td>この属性には、変数の写真のシーケンス内の対応するフレームのフレーム ID が含まれています。 この属性は、変数フォト シーケンスのキャプチャのみ設定されます。</td>
</tr>
<tr class="even">
<td><strong>MF_CAPTURE_METADATA_EXPOSURE_TIME</strong></td>
<td><strong>UINT64</strong></td>
<td>この属性には、公開期間適用 (100 ナノ秒単位) にはが含まれています。</td>
</tr>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_EXPOSURE_COMPENSATION</strong></td>
<td><strong>Blob</strong></td>
<td>この属性には、EV 補正手順フラグと写真をキャプチャしたときに、ドライバーが適用されたステップ単位で EV 報酬値が含まれています。 <a href="https://msdn.microsoft.com/library/windows/hardware/dn897242" data-raw-source="[&lt;strong&gt;CapturedMetadataExposureCompensation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897242)"> <strong>CapturedMetadataExposureCompensation</strong> </a>データ構造体には、この属性にのみ blob の形式がについて説明します。 EV 補正のメタデータ項目構造体の形式 (<strong>KSCAMERA_METADATA_ITEMHEADER</strong> + EV 補正メタデータ ペイロード) は、ドライバーによって提供され、8 バイトで整列をする必要があります。</td>
</tr>
<tr class="even">
<td><strong>MF_CAPTURE_METADATA_ISO_SPEED</strong></td>
<td><strong>UINT32</strong></td>
<td>この属性には、整数として適用される ISO 速度の値が含まれています。</td>
</tr>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_LENS_POSITION</strong></td>
<td><strong>UINT32</strong></td>
<td>この属性は、フォーカスがキャプチャされた写真に適用されたときに、レンズの論理位置を格納します。 この値には、特定の単位はありません。</td>
</tr>
<tr class="even">
<td><strong>MF_CAPTURE_METADATA_SCENE_MODE</strong></td>
<td><strong>UINT64</strong></td>
<td>この属性には、シーンのモードとして適用、 <strong>UINT64KSCAMERA_EXTENDEDPROP_SCENEMODE_XXX</strong>フラグ。</td>
</tr>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_FLASH</strong></td>
<td><p><strong>UINT32</strong></p>
<p>(Boolean)</p></td>
<td>この属性には、フラッシュの状態を含むブール値が含まれています。 値 1 は、flash し、値 0 では、キャプチャされた写真のオフ、flash であることを指定することを指定します。</td>
</tr>
<tr class="even">
<td><strong>MF_CAPTURE_METADATA_FLASH_POWER</strong></td>
<td><p><strong>UINT32</strong></p></td>
<td>この属性には、0 ~ 100 のパーセント値として適用フラッシュの電源が含まれています。</td>
</tr>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_WHITEBALANCE</strong></td>
<td><p><strong>UINT32</strong></p>
<p>(ケルビン)</p></td>
<td>この属性には、ケルビンで値として適用ホワイト バランスが含まれています。</td>
</tr>
<tr class="even">
<td><strong>MF_CAPTURE_METADATA_ZOOMFACTOR</strong></td>
<td><p><strong>UINT32</strong></p>
<p>(Q16)</p></td>
<td>この属性がからクエリを実行できるのと同じ値を適用するズームの値が含まれています、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn936756" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn936756)"> <strong>KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM</strong> </a> GET 呼び出しで。 値は、Q16 である必要があります。</td>
</tr>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_FRAME_ILLUMINATION</strong></td>
<td><strong>UINT64</strong></td>
<td><p><strong>MF_CAPTURE_METADATA_FRAME_ILLUMINATION</strong> IR カメラの属性は、フレームがアクティブな IR 照明を使用しているしと組み合わせて使用する必要があるかどうかを指定します<strong>FACEAUTH_MODE_ALTERNATIVE_FRAME_。照明</strong>します。 IR サンプルの使用のみと、カメラが赤外線と色の両方のサンプルをサポートしている場合に RGB フレーム上に存在できないする必要があります。</p>
<p>アクティブな照明が上、照明がフレームをキャプチャするときに存在しない場合は、0xXXXXXXXXXXXXXXX0 に設定すると、フレームをキャプチャした場合、0xXXXXXXXXXXXXXXX1 に値を設定する必要があります。</p></td>
</tr>
<tr class="even">
<td>任意のカスタム GUID</td>
<td>任意のバリアント型</td>
<td>この属性には、カスタム GUID に関連付けられているカスタム データが含まれています。</td>
</tr>
</tbody>
</table>

 

**EXIF と HW JPEG エンコーダー**

パイプラインは、HW JPEG エンコーダー; の EXIF データを warp または処理する必要はありません。ドライバー、MFT0、および OEM ハードウェア JPEG EXIF のデータ形式を提供するそのため、エンコーダー。 Oem パートナーは、任意のカスタム属性の GUID と EXIF 属性のバリアントの型を定義し、アタッチ先、 **MFSampleExtension\_CaptureMetaData**属性バッグに OEM コンポーネントによって使用されます。 パイプライン フォト シンク コンポーネントは HW JPEG エンコーダーをロードし、保持されている EXIF データを設定 HW JPEG エンコーダーを使用できる場合、 **MFSampleExtension\_CaptureMetaData** EXIF として HW JPEG エンコーダーに属性バッグエンコーダーのオプションを使用して、 [IPropertyBag2::Write](https://go.microsoft.com/fwlink/?LinkId=331589)メソッド。

エンコーダーのオプションのプロパティ バッグには、使用可能なエンコーディング オプション プロパティを指定する PROPBAG2 構造体の配列が含まれています。 HW JPEG エンコーダーに設定された EXIF エンコーダー オプションは、エンコーダーのオプションのプロパティ バッグ内の次のプロパティによって識別されます。

| プロパティ名      | VARTYPE         | 値                                                                                                                                                       | 適用可能なコーデック |
|--------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| **SampleMetaData** | **VT\_不明** | IMFAttributes インターフェイスへのポインター **MFSampleExtension\_CaptureMetaData** EXIF データを格納している OEM sub 属性を含む属性のバッグ。 | JPEG              |

 

**MFSampleExtension\_CaptureMetaData**属性バッグだけを含めたりする OEM に EXIF データを保持するために読み取ることができる MFT0 と HW JPEG エンコーダー EXIF sub 属性が定義されています。 EXIF データをドライバーから HW JPEG エンコーダーに渡す、ドライバーと MFT0 に、次は必要があります。

1.  ドライバーは、パイプラインによって指定されたメタデータのバッファーでのカスタムの EXIF メタデータを提供します。 これに接続されている**MFSampleExtension\_CaptureMetadata**として、 **MF\_キャプチャ\_メタデータ\_フレーム\_RAWSTREAM**DevProxy DevProxy にサンプルが返されるときに、IMFAttribute します。

2.  MFT0、IMFSample を受信する場合から未処理のメタデータのバッファーを取得します**MF\_キャプチャ\_メタデータ\_フレーム\_RAWSTREAM**とカスタムの EXIF メタデータ項目を解析して変換。OEM に IMFAttribute を定義およびにアタッチします、 **MFSampleExtension\_CaptureMetadata**属性バッグ。

EXIF データを MFT0 から HW JPEG エンコーダーに渡す、パイプラインの写真のシンクは、次の。

1.  呼び出し**GetUnknown**で**MFSampleExtension\_CaptureMetadata** IMFSample IMFSample が受信したときに、属性のバッグ IMFAttributes インターフェイスを取得するからです。

2.  呼び出し[IPropertyBag2::Write](https://go.microsoft.com/fwlink/?LinkId=331589) HW JPEG エンコーダーに SampleMetadata で識別されるエンコーダー オプションのプロパティを設定します。 エンコーダーのオプションのプロパティには、前の手順から取得した IMFAttributes インターフェイスが含まれています。 このインターフェイスには、OEM EXIF sub 属性を含むすべてのユーザー定義のサブ属性とで標準化されたサブ属性が含まれています、**メタデータ**セクションでは、このトピックで前述しました。

さらに処理するための EXIF データを取得するには、HW JPEG エンコーダーは、次を行います。

1.  呼び出し**IPropertyBag2::Read** SampleMetadata プロパティ名で識別されるプロパティのプロパティ値を取得し、 **VT\_不明な**型。 返されると、 **VARIANT.punkVal**の IMFAttributes インターフェイスを受け取る**MFSampleExtension\_CaptureMetadata**します。

2.  呼び出し**GetBlob**または**GetUnknown** OEM EXIF EXIF データ blob を取得する前の手順から取得したインターフェイスからサブ属性に基づいて OEM EXIF sub 属性の GUID とデータ型。

**サムネイル**

MFT0 がカメラのドライバーのサムネイルを生成するために必要ではありません。 独自のサムネイルを生成するには、カメラ アプリが必要です。 写真の確認イメージ、HW JPEG エンコーダーからサムネイルを生成できなかったまたはフル サイズの画像のサイズを変更します。 これは、アプリ開発者です。 Windows 8.1 アプリと API およびアプリの互換性を維持するためにカメラのドライバーを実装する必要がありますいない、 **KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOTHUMBNAIL**コントロール。

## <a name="integer-iso"></a>ISO の整数


[ **KSPROPERTY\_CAMERACONTROL\_拡張\_ISO\_詳細**](https://msdn.microsoft.com/library/windows/hardware/dn917947)プロパティ ID は整数 ISO DDI に関連付けられている唯一のコントロール。

## <a name="advanced-focus"></a>高度なフォーカス


[ **KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSMODE** ](https://msdn.microsoft.com/library/windows/hardware/dn567576)プロパティ ID は整数 ISO DDI に関連付けられている唯一のコントロール。

## <a name="flash"></a>Flash


[ **KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE** ](https://msdn.microsoft.com/library/windows/hardware/dn567575)プロパティ ID はフラッシュ DDI に関連付けられている唯一のコントロール。

## <a name="zoom"></a>ズーム


[ **KSPROPERTY\_CAMERACONTROL\_拡張\_ズーム**](https://msdn.microsoft.com/library/windows/hardware/dn936756)プロパティ ID はズーム DDI に関連付けられている唯一のコントロール。

## <a name="scene-mode"></a>シーンのモード


[ **KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE** ](https://msdn.microsoft.com/library/windows/hardware/dn567585)プロパティ ID は、シーン モード DDI に関連付けられている唯一のコントロール。

 

 




