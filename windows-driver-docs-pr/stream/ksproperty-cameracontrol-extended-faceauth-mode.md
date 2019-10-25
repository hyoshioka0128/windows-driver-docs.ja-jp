---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FACEAUTH\_モード
description: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FACEAUTH\_MODE は、顔認証を有効または無効にするために使用されるプロパティ ID です。
ms.assetid: 240AABDB-585B-462E-B391-1CB55BA563D5
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 74de82c04523e3ac6de3c5268c0bcf2f31d2fbf3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843237"
---
# <a name="ksproperty_cameracontrol_extended_faceauth_mode"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FACEAUTH\_モード


**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_FACEAUTH\_MODE**は、顔認証を有効または無効にするために使用されるプロパティ ID です。

### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>適用範囲</th>
<th>コントロール</th>
<th>タスクバーの検索ボックスに</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン 1</p></td>
<td><p>Pin</p></td>
<td><p>同期</p></td>
</tr>
</tbody>
</table>

 

次のビットフラグは、ドライバーの顔認証を制御します。

```cpp
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED                        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION  0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION          0x0000000000000004
```

次の表では、フラグ機能について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong></p></td>
<td><p>オプション機能。</p>
<p>指定した場合、ドライバーのビデオ顔認証モードは無効になります。 このフラグは、 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong>および<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>フラグと同時に指定することはできません。</p></td>
</tr>
<tr class="even">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong></p></td>
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong>がサポートされていない場合は、必須の機能です。</p>
<p>指定する場合は、フレームメタデータで説明されている各サンプルに<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>を設定することが必須です。 このフラグは、 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong>および<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong>フラグと同時に指定することはできません。 このモードでは、キャプチャされたフレームごとに IR ストロボが交互にオン/オフになることが予想されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong></p></td>
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>がサポートされていない場合は、必須の機能です。</p>
<p>このフラグは、 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>および<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong>フラグと同時に指定することはできません。 このモードでは、バックグラウンドアンビエント IR 光が減算された赤外線イメージを作成する必要があります。</p></td>
</tr>
</tbody>
</table>

 

既定では、ドライバーは**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_FACEAUTH\_mode**が**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_mode**に設定されている必要があります (一般的な場合)。目的の IR カメラ。 それ以外の場合は、 **KSCAMERA\_extendedprop\_FACEAUTH\_モード\_バックグラウンド\_減算**または**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_代替 @no__t_ を設定する必要があり11_ フレーム\_照明**。

IR カメラは、Windows Hello 以外の一般的なシナリオで動作することが予想される場合に、 **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_\_モード**をアドバタイズする必要があります。

顔ログインに使用される IR カメラは、 **KSCAMERA\_extendedprop\_FACEAUTH\_モード\_代替\_フレーム\_照明**または**KSCAMERA\_EXTENDEDPROP\_FACEAUTH をサポートする必要があり @no__t\_バックグラウンド\_の減算**機能の場合は、これらのフラグのいずれか1つだけをサポートする必要があります。

次の表に、コントロールを使用する場合の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体のフィールドの説明と要件を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メンバー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>これは1である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>は、フィルターの1つのピンでのみアドバタイズする必要があります。 Pin は<strong>PINNAME_VIDEO_CAPTURE</strong>または<strong>PINNAME_VIDEO_PREVIEW</strong>型である必要があり、IR センサーデータを生成する必要があり、frameserver で共有可能とマークされている必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは<strong>sizeof</strong>(<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + <strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)"><strong>KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING</strong></a>) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>は、前の手順で定義したように、サポートされている<strong>KSCAMERA_EXTENDEDPROP_ FACEAUTH_MODE_xxx</strong>フラグのビット単位である必要があります。</p>
<p>ドライバーでは、 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>と<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong>の両方をアドバタイズしないでください。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これには、上で定義した<strong>KSCAMERA_EXTENDEDPROP_ FACEAUTH_MODE_xxx</strong>フラグのいずれかを指定できます。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
