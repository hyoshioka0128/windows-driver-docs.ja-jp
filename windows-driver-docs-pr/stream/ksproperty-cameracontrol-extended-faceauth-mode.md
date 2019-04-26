---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_FACEAUTH\_モード
description: KSPROPERTY\_CAMERACONTROL\_拡張\_FACEAUTH\_モードがオンとオフ顔認証に使用するプロパティ ID。
ms.assetid: 240AABDB-585B-462E-B391-1CB55BA563D5
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE ストリーミング メディア デバイス
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
ms.openlocfilehash: 53c77198cd2eb297a3bee8cc5890e3bd35186789
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348025"
---
# <a name="kspropertycameracontrolextendedfaceauthmode"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_FACEAUTH\_モード


**KSPROPERTY\_CAMERACONTROL\_拡張\_FACEAUTH\_モード**オンとオフ顔認証に使用されるプロパティの ID です。

### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Scope</th>
<th>コントロール</th>
<th>種類</th>
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

 

次ビット フラグ コントロール顔認証ドライバーで:

```cpp
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED                        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION  0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION          0x0000000000000004
```

次の表では、フラグの機能について説明します。

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
<td><p>省略可能な機能です。</p>
<p>指定した場合、ドライバーでビデオの顔認証モードは無効です。 このフラグはで相互に排他的では、 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong>と<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>フラグ。</p></td>
</tr>
<tr class="even">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong></p></td>
<td><p>必須機能場合<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong>はサポートされていません。</p>
<p>設定するのには必須では指定した場合、 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>フレーム メタデータによる記述では、各サンプルにします。 このフラグはで相互に排他的では、 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong>と<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong>フラグ。 このモードでキャプチャされた各フレームのオン/オフを代替の IR strobe 予定です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong></p></td>
<td><p>必須機能場合<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>はサポートされていません。</p>
<p>このフラグはで相互に排他的では、 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>と<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong>フラグ。 このモードでは、アンビエント IR ライトを反射減算の背景を持つ IR イメージの作成に想定されます。</p></td>
</tr>
</tbody>
</table>

 

既定では、ドライバーが必要**KSPROPERTY\_CAMERACONTROL\_拡張\_FACEAUTH\_モード**設定**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_無効**汎用 IR カメラ。 それ以外の場合に設定する必要がある**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_バック グラウンド\_減算**または**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_代わり\_フレーム\_照明**します。

IR のカメラをアドバタイズする必要があります**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_無効**の Windows こんにちは以外の一般的なシナリオで機能が予想される場合。

顔のログインに使用する IR カメラは、いずれかをサポートする必要があります**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_代わり\_フレーム\_照明**または**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_モード\_バック グラウンド\_減算**する必要があります機能だけがサポートこれらのフラグのいずれかのない機能両方とも。

次の表には、説明と要件が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)コントロールを使用する場合は、フィールドを構造体します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>これは、1 でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>フィルターを 1 つだけの pin にアドバタイズする必要があります。 Pin は型である必要があります<strong>PINNAME_VIDEO_CAPTURE</strong>または<strong>PINNAME_VIDEO_PREVIEW</strong>FrameServer の共有可能とマークや、IR のセンサー データを生成する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>これでなければなりません<strong>sizeof</strong>(<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + <strong>sizeof</strong>(<a href="https://msdn.microsoft.com/library/windows/hardware/dn567566" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567566)"><strong>KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING</strong></a>).</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>ビット単位の OR のサポートされている必要があります<strong>KSCAMERA_EXTENDEDPROP_ FACEAUTH_MODE_xxx</strong>前述のようにフラグを設定します。</p>
<p>ドライバーが両方をアドバタイズしません<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>と<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong></p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これのいずれを指定することができます、 <strong>KSCAMERA_EXTENDEDPROP_ FACEAUTH_MODE_xxx</strong>上記で定義されたフラグ。</p></td>
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
