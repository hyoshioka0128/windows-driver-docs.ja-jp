---
title: KSK プロパティ\_CAMERACONTROL\_PERフレーム設定\_設定
description: KSK プロパティ\_CAMERACONTROL\_PERFRAME 設定\_、KSK プロパティで定義されているプロパティ ID\_CAMERACONTROL\_PERFRAME SETTING\_プロパティを使用して、ドライバーのフレームごとの設定を設定します。
ms.assetid: 2EFBEA64-8340-4367-A56B-2C46167F0DE5
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_SET ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_SET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f291028350a415bf16d41c2fa0b0710b13964db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843339"
---
# <a name="ksproperty_cameracontrol_perframesetting_set"></a>KSK プロパティ\_CAMERACONTROL\_PERフレーム設定\_設定

**Ksk プロパティ\_CAMERACONTROL\_PERFRAME 設定\_** 、ksk プロパティに定義されているプロパティ ID を設定します。 [ **\_CAMERACONTROL\_PERフレーム設定\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_perframesetting_property)を使用して、フレームごとの設定を設定します。driver.

## <a name="usage-summary"></a>使用状況の概要

フレームごとの設定を設定するために、 **Ksk プロパティ\_CAMERACONTROL\_PERFRAME 設定\_set**プロパティコントロールは、フレームごとの設定ペイロードと共にドライバーに送信されます。

このプロパティは、読み取りまたは書き込みが可能です。 **Get**呼び出しを使用すると、ドライバーで設定された最後のフレーム設定を返すことができますが、 **get**呼び出しはアプリクライアントに公開されず、フレームごとの設定コントロールが MF パイプラインによって構築されるときにのみ、初期化時に発行されます。ドライバーは、バッファーサイズが0の**オーバーフロー\_の状態\_バッファー**を返す必要があります。

GET 呼び出しでは、ドライバーに含まれるフレームごとの設定全体を保持するために必要なデータバッファーサイズを確認するために、最初にゼロ長のバッファーがドライバーに送信されます。 この呼び出しへの応答として、ドライバーは、必要なフレームごとの設定のバッファーサイズを使用して **\_バッファー\_オーバーフロー**を返す必要があります。これにより、フレームごとの設定が設定されていない場合や、少なくとも KSCAMERA のサイズである場合は0である必要があり[ **\_PERフレーム設定\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_header)ではありません。

フレームごとの設定ペイロードは、 **KSCAMERA\_PERFRAME setting\_ヘッダー**の後に1つ以上のフレーム設定を指定して開始する必要があります。 フレーム設定の数は、FrameCount で指定します。 各フレームの設定は、 [**KSCAMERA\_PERFRAME setting\_frame\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_frame_header)で開始し、その後に0個以上の項目設定を指定する必要があります。 項目設定の数は ItemCount で指定します。 各項目の設定 ( [**KSCAMERA\_PERフレーム設定\_項目\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_item_header)で始める必要がある場合)。

各項目の設定では、値ペイロードが存在する場合、 **KSCAMERA\_PERフレーム設定\_項目\_ヘッダー**の後に、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)を指定する必要があります。 カスタム項目が存在する場合は、 **KSCAMERA\_PERフレーム設定\_項目\_ヘッダー**\_の後に、[**カスタム\_項目\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_custom_item)、その後に GUID Id に関連付けられたカスタムデータを指定する必要があります。**カスタム\_項目\_KSCAMERA\_PERフレームの設定**で指定されます。

FrameCount が0の場合、ドライバーはフレームごとの設定ペイロードを拒否する必要があります。 ItemCount が0の場合、フレーム設定は指定されません。 ドライバーは、関連付けられているフレームにグローバル設定を適用する必要があります。 たとえば、FrameCount = 1 と ItemCount = 0 は、グローバル設定を持つ1つのフレーム変数フォトシーケンスを意味します。

次の図は、フレーム設定ペイロード構成ごとのデータ構造レイアウトを示しています。 次の例では、4つのフレームのフレームごとの設定が、3つの項目を含むフレーム0で構成されています。2つの項目 (ペイロードなし) と値のペイロードが含まれています。2つの項目 (ペイロードなし、もう一方に値ペイロードを含む) が含まれているフレーム1フレーム2には、フレーム2のグローバル設定を意味する0項目が含まれています。4つの項目を含むフレーム3。1つは値ペイロード、もう1つはカスタム項目とカスタムデータペイロード、もう1つはペイロードを含みません。

![perフレーム設定\-ヘッダーの構造](images/oem-perframesettings-header-payload-datastructure.png)

1.  **[フレームごとの設定] ヘッダーのサイズ**は、 **KSCAMERA\_perフレームの設定\_ヘッダーに入力されるペイロードの合計サイズを表します。サイズ**

2.  フレーム**ごとの設定フレームのサイズ**は、 **KSCAMERA\_perframe setting\_frame\_HEADER に格納されるサイズを表します。** フレームのサイズ。

3.  **項目のサイズ**は、 **KSCAMERA\_PERフレームの設定\_項目\_ヘッダーに入力されるサイズを表します。** 項目のサイズ。

4.  **カスタム項目のサイズ**は、**カスタム\_項目\_KSCAMERA\_perフレーム設定に格納されるサイズを表します。** カスタム項目のサイズ。

**フレームごとの設定の公開時間**

[フレームごとの設定] で手動露出時間が指定されている場合、 **KSCAMERA\_EXTENDEDPROP\_値になります。値**には、 **SET**呼び出しに必要な公開時間と**GET**呼び出しで使用されている現在の露出時間が含まれます。

**フレームごとの設定の補正**

[フレームごとの設定] で手動設定の補正が指定されている場合、 **KSCAMERA\_EXTENDEDPROP\_値になります。Value. l**には、 **SET**呼び出しに必要な露出補正と、 **GET**呼び出しで使用されている現在の露出補正が含まれます。

**フレームごとの設定のフォーカス**

フレームごとの設定が [フレームごとの設定] で指定されている場合、 **KSCAMERA\_EXTENDEDPROP\_値になります。値。 ul**には、 **SET**呼び出しの目的のレンズ位置と、 **GET**呼び出しで使用されている現在のレンズ位置が含まれます。

**フレームごとの設定: ISO**

ドライバーで**KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL**がサポートされていない場合、値ペイロードは含まれません。 それ以外の場合は、フレームごとの設定項目のヘッダーの後に、 **KSCAMERA\_EXTENDEDPROP\_値**を指定する必要があります。 **SET**呼び出しでは、 **KSCAMERA\_EXTENDEDPROP\_値です。** **KSCAMERA\_extendedprop\_ISO\_MANUAL**がサポートされていて、 **KSCAMERA\_PERフレーム設定\_ITEM\_HEADER で指定されている場合は、必要な iso 速度を含みます。フラグ**。

次の例では、項目のヘッダーと値のペイロードが、フレームごとの設定の ISO 機能が\_KSCAMERA である場合に、 **\_iso\_AUTO**、 **KSCAMERA\_extendedprop\_iso\_MANUAL のようになります。** (最小値 = 30、最大値 = 210、ステップ = 20) 次のようになります。

```cpp
KSCAMERA_EXTNDEDPROP_ISO_AUTO, 
KSCAMERA_EXTENDEDPROP_ISO_MANUAL (min = 30, max = 210, step =20)
```

1.  ISO の速度が70の場合

    ```cpp
    KSCAMERA_PERFRAMESETTING_ITEM_HEADER.Flags = KSCAMERA_EXTENDEDPROP_ISO_MANUAL
    KSCAMERA_EXTENDEDPROP_VALUE.Value.ul = 70
    ```

2.  ISO の速度が50の場合

    ```cpp
    KSCAMERA_PERFRAMESETTING_ITEM_HEADER.Flags = KSCAMERA_EXTENDEDPROP_ISO_MANUAL
    KSCAMERA_EXTENDEDPROP_VALUE.Value.ul = 50
    ```

次の表は、フレームごとの設定で使用できるコントロールと値の概要を示しています。 実際の可用性は、ドライバーの実際の機能によって決まります。これは、 [**Ksk プロパティ\_CAMERACONTROL\_PERフレーム設定\_機能**](ksproperty-cameracontrol-perframesetting-capability.md)を使用して取得できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>使用可能な値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>露出時間</p></td>
<td><p>自動または時間 (100 ナノ秒)。</p></td>
</tr>
<tr class="even">
<td><p>Flash</p></td>
<td><p>[オン/オフ]、[自動]、[赤目の縮小のオン/オフ]、[フラッシュ電力 (%)]。</p></td>
</tr>
<tr class="odd">
<td><p>露出補正</p></td>
<td><p>自動または補正のステップ値。</p></td>
</tr>
<tr class="even">
<td><p>ISO 速度</p></td>
<td><p>整数 ISO 値を持つ Auto または manual。</p></td>
</tr>
<tr class="odd">
<td><p>Focus</p></td>
<td><p>自動または論理的なレンズの位置。 この値には、特定の単位がありません。</p></td>
</tr>
<tr class="even">
<td><p>カスタムプロパティ</p></td>
<td><p>OEM はこれをカスタム GUID とプロパティデータで定義します。</p></td>
</tr>
<tr class="odd">
<td><p>確認の画像</p></td>
<td><p>オン/オフ</p></td>
</tr>
</tbody>
</table>

カスタムプロパティデータをフレームごとの設定に渡すために、アプリは次の処理を実行します。

1.  Iframe Settingscontrols の QueryInterface を呼び出して、フレームごとの設定に関連付けられている IMFGetServices インターフェイスを取得します。

2.  IMFGetServices インターフェイスから GetService を呼び出して、フレームごとの設定でカスタム IMFAttributes インターフェイスを作成します。

3.  カスタムプロパティ GUID の SetUINT32、SetBlob などを呼び出して、フレームごとの設定に関連付けられている IMFAttributes にカスタムプロパティデータを設定します。

フレームワークは、カスタムの IMFAttributes を検索して、カスタム項目ペイロードを作成します (フレームごとの設定のペイロードをアセンブルするときに、ドライバーで設定されます)。

**KSCAMERA\_PERFRAMES setting\_ヘッダー**の**LoopCount**フィールドは、フレームごとの設定を、今後のフレームに適用して、写真のシーケンスでキャプチャする必要がある繰り返しの回数を指定します。 **LoopCount**は、パイプラインによって1にハードコーディングされます (たとえば、フレームごとの設定は、それ以上繰り返さなくても適用されます)。 **KSCAMERA\_PERFRAMES setting\_HEADER**の**framecount**フィールドは、フレームごとの設定を各繰り返しのフレームに適用する必要があるフレーム設定の数を指定します。

**KSCAMERA\_PERFRAME setting\_frame\_HEADER**の**ItemCount**フィールドには、対応するフレームに適用する項目設定の数を指定します。 **ItemCount**が0の場合は、対応するフレームにグローバル設定を適用する必要があります。

次の表は、可能な構成と、対応する写真のシーケンスの種類を示しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>LoopCount</th>
<th>FrameCount</th>
<th>ItemCount</th>
<th>タスクバーの検索ボックスに</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>L (L = 1)</p></td>
<td><p>N (N&gt;0)</p></td>
<td><p>S (&gt;= 0)</p></td>
<td><p>有限変数の写真シーケンス</p></td>
</tr>
<tr class="even">
<td><p>L (L = 1)</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>グローバル設定を使用する1つのフレーム有限変数フォトシーケンス</p></td>
</tr>
<tr class="odd">
<td><p>L (L = 1)</p></td>
<td><p>0</p></td>
<td><p>S</p></td>
<td><p>無効な構成</p></td>
</tr>
</tbody>
</table>

変数 photo sequence は、1回の繰り返しだけで有限のキャプチャを実行するように簡略化されています。 フレームごとの設定を含む写真シーケンスは、常に変数の写真シーケンスとしてフラグが設定され、フレームごとの設定ペイロードは常に必要です。

ループ数が L (L = 1) で、フレーム数が N (N &gt; 0) の場合は、有限の可変の写真シーケンスです。 フレームごとの設定は、N = 1 回繰り返され、各繰り返しの次の N 個のフレームに適用されます。

ループカウントが L (L = 1) で、フレーム数が1で、項目数が0である場合は、グローバル設定を使用した1つのフレーム有限変数フォトシーケンスです。

変数のフォトシーケンスは、過去のフレームを要求しないようにさらに簡略化されています。 パイプラインは、要求された過去の写真の数 (Requestedhistory Frames など) を0にハードコーディングします。 ドライバーは、変数の写真シーケンス内の将来のフレームのみを配信します。 次の図は、ドライバーによって使用される予定のフレーム数を変数の写真シーケンスで示しています。 過去の写真の数は、 **KSCAMERA\_EXTENDEDPROP\_PHOTOMODE で指定されています。** [**Ksk プロパティ\_CAMERACONTROL\_拡張\_photomode**](ksproperty-cameracontrol-extended-photomode2.md)拡張プロパティコントロールで、パイプラインによって0にハードコーディングされた requestedhistory フレーム。

```cpp
N : Frame Count
L : Loop Count
P : Past Photos Requested
T : Total number of frame delivered by driver
L = 1
P = 0
T = (N * L) + P
```

有限変数フォトシーケンスの場合、ドライバーは Ksk ストリーム\_ヘッダーにマークする必要があり**ます。** 最後のフレームのオプションフラグは、 **ksk ストリーム\_ヘッダー\_オプション SF\_ENDOFPHOTOSEQUENCE**フラグです。 これにより、予想されるフレームの量が多くなった後に、ドライバーが自動的にフレームを MF パイプラインに配信しなくなります。 これにより、写真シーケンスが効果的に停止され、アプリクライアントに写真シーケンスの完了が通知されます。 これは、ドライバーが有限変数の写真シーケンスの最後のフレームのキャプチャを終了したときに発生します。

## <a name="requirements"></a>要件

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
