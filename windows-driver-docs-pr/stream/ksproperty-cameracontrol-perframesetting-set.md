---
title: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_設定
description: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_KSPROPERTY で定義されているプロパティ ID\_CAMERACONTROL\_PERFRAMESETTING\_プロパティは、フレームごとの設定に使用されます。ドライバーの設定。
ms.assetid: 2EFBEA64-8340-4367-A56B-2C46167F0DE5
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_SET ストリーミング メディア デバイス
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
ms.openlocfilehash: 18fe6849e44076e1cb4ae2208ca7968099f3daa4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338367"
---
# <a name="kspropertycameracontrolperframesettingset"></a>KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_設定

**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_設定**で定義されているプロパティ ID [ **KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_perframesetting_property)ドライバーでフレームごとの設定を設定するために使用します。

## <a name="usage-summary"></a>使用状況の概要

フレームの設定ごとの設定、 **KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_設定**プロパティ コントロールがと共にドライバーに送信される、ごとの設定のフレームのペイロード。

このプロパティは、読み取りまたは書き込まれることができます。 中に、**取得**を返す、ドライバーに設定されたフレームの設定ごとの最後の呼び出しを使用できます、**取得**の呼び出しは、アプリのクライアントに公開されていないと、初期化の際に発行されるだけです時間フレームごとの制御の設定は、ドライバーを返す必要があります、MF パイプラインによって構築**状態\_バッファー\_OVERFLOW**バッファー サイズは 0。

GET 呼び出しで 0 個の長バッファーには、ドライバーが全体のフレームごとの設定を保持するために必要なデータ バッファーのサイズを調べるに最初に、ドライバーに送信されます。 この呼び出しに応答してでドライバーを返す必要があります**状態\_バッファー\_OVERFLOW**フレームごとの設定が設定されていない場合または 0 をする必要があるフレームごとの必要な設定のバッファー サイズとの最小限のサイズ[ **KSCAMERA\_PERFRAMESETTING\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_header)それ以外の場合。

フレームごとの設定のペイロードで始まらなければなりません、 **KSCAMERA\_PERFRAMESETTING\_ヘッダー**、その後に 1 つ以上のフレームを設定します。 フレームの設定の数は、FrameCount で指定されます。 各フレームの設定で始まらなければなりません、 [ **KSCAMERA\_PERFRAMESETTING\_フレーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_frame_header)、その後に 0 個以上の項目の設定。 項目の設定の数は、ItemCount で指定されます。 開始する必要がありますいずれかの場合、各項目の設定、 [ **KSCAMERA\_PERFRAMESETTING\_項目\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_item_header)します。

値のペイロードが存在する場合は、各項目の設定、 **KSCAMERA\_PERFRAMESETTING\_項目\_ヘッダー**続く必要があります、 [ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)します。 カスタムの項目が存在する場合**KSCAMERA\_PERFRAMESETTING\_項目\_ヘッダー**続く必要があります、 [ **KSCAMERA\_PERFRAMESETTING\_カスタム\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_custom_item)で指定された GUID Id に関連付けられているカスタム データと、その後**KSCAMERA\_PERFRAMESETTING\_カスタム\_項目**.

FrameCount が 0 の場合、ドライバーはフレームごとの設定のペイロードを拒否する必要があります。 ItemCount が 0 の場合は、フレームの設定は指定されません。 ドライバーは、関連付けられているフレームをグローバル設定を適用する必要があります。 たとえば、FrameCount = 1、ItemCount = 0 はグローバル設定で 1 つのフレーム変数の写真のシーケンスを意味します。

次の図のデータ構造体レイアウトを示しています、あたりのフレームのペイロード設定します。 フレーム 0 含む 3 つの項目、; 値のペイロードのいずれかとペイロードがない 2 つでは、次の例では、4 つのフレームをフレームごとの設定が構成されています。フレームのペイロードがないかと; 値のペイロードで、その他の 2 つの項目を含む 1フレーム 2 フレーム 2; のグローバル設定のことを意味する 0 の項目を含むフレーム値のペイロードをカスタムの項目とカスタム データ ペイロードでは、それぞれ 2 つとペイロードがない 1 つで 1 つ、4 つのアイテムを含む 3。

![構造体の perframesetting\-ヘッダー](images/oem-perframesettings-header-payload-datastructure.png)

1.  **フレームごとの設定のヘッダーにサイズ**情報を格納する合計ペイロード サイズを表す**KSCAMERA\_PERFRAMESETTING\_ヘッダー。サイズ**

2.  **フレームごとの設定のフレーム サイズ**情報を格納するサイズを表す**KSCAMERA\_PERFRAMESETTING\_フレーム\_ヘッダー。サイズ**フレーム。

3.  **アイテムのサイズ**情報を格納するサイズを表す**KSCAMERA\_PERFRAMESETTING\_項目\_ヘッダー。サイズ**項目。

4.  **カスタム アイテム サイズ**情報を格納するサイズを表す**KSCAMERA\_PERFRAMESETTING\_カスタム\_項目。サイズ**カスタム項目。

**フレームごとの公開期間を設定**

別のフレームの設定で手動の露出時間が指定されている場合**KSCAMERA\_EXTENDEDPROP\_値。Value.ll**で目的の露出時間を含む、**設定**呼び出しと現在の露出時間で使用、**取得**を呼び出します。

**フレームごとの設定の補正**

手動による設定事項補正が別のフレームの設定で指定された場合**KSCAMERA\_EXTENDEDPROP\_値。Value.l**で目的の露出の補正を含む、**設定**呼び出しとで使用されている現在の露出の補正を**取得**を呼び出します。

**フレームごとのフォーカスの設定**

フレーム設定に従って手動が別のフレームの設定で指定された場合**KSCAMERA\_EXTENDEDPROP\_値。Value.ul**で目的のレンズの位置が含まれます、**設定**呼び出しと現在のレンズの位置で使用されている、**取得**を呼び出します。

**フレームごとの ISO の設定**

ドライバーがサポートされていない場合**KSCAMERA\_EXTENDEDPROP\_ISO\_手動**値のペイロードは含まれません。 それ以外の場合、フレームごとの設定の項目ヘッダーの後に、 **KSCAMERA\_EXTENDEDPROP\_値**します。 **設定**を呼び出すと、 **KSCAMERA\_EXTENDEDPROP\_値。Value.ul**目的の ISO 速度が含まれる場合**KSCAMERA\_EXTENDEDPROP\_ISO\_手動**サポートされで指定された**KSCAMERA\_PERFRAMESETTING\_項目\_ヘッダー。フラグ**します。

次は、フレームごとの設定の ISO 機能の場合のように項目ヘッダーと値のペイロードを表して方法**KSCAMERA\_EXTNDEDPROP\_ISO\_自動**、 **KSCAMERA\_EXTENDEDPROP\_ISO\_手動**(min = 30、最大値、210 を = ステップ = 20) 次のようにします。

```cpp
KSCAMERA_EXTNDEDPROP_ISO_AUTO, 
KSCAMERA_EXTENDEDPROP_ISO_MANUAL (min = 30, max = 210, step =20)
```

1.  ISO の速度が 70 の場合

    ```cpp
    KSCAMERA_PERFRAMESETTING_ITEM_HEADER.Flags = KSCAMERA_EXTENDEDPROP_ISO_MANUAL
    KSCAMERA_EXTENDEDPROP_VALUE.Value.ul = 70
    ```

2.  ISO の速度が 50 である場合

    ```cpp
    KSCAMERA_PERFRAMESETTING_ITEM_HEADER.Flags = KSCAMERA_EXTENDEDPROP_ISO_MANUAL
    KSCAMERA_EXTENDEDPROP_VALUE.Value.ul = 50
    ```

次の表に、利用可能なコントロールとのフレームごとの設定の値を示します。 実際の可用性を使用して取得できるドライバーの実際機能によって決まります[ **KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_機能**](ksproperty-cameracontrol-perframesetting-capability.md).

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
<td><p>公開期間</p></td>
<td><p>自動または時間 (100 ナノ秒単位)。</p></td>
</tr>
<tr class="even">
<td><p>Flash</p></td>
<td><p>オン/オフ、auto、オン/オフ、フラッシュの能力の割合の赤目減少します。</p></td>
</tr>
<tr class="odd">
<td><p>露出補正</p></td>
<td><p>自動または補正のステップ値。</p></td>
</tr>
<tr class="even">
<td><p>ISO 速度</p></td>
<td><p>自動または手動 ISO は整数値。</p></td>
</tr>
<tr class="odd">
<td><p>フォーカス</p></td>
<td><p>自動または論理レンズの位置。 この値には、特定の単位はありません。</p></td>
</tr>
<tr class="even">
<td><p>カスタム プロパティ</p></td>
<td><p>OEM は、カスタム GUID およびプロパティのデータで、これを定義します。</p></td>
</tr>
<tr class="odd">
<td><p>確認のイメージ</p></td>
<td><p>オン/オフ</p></td>
</tr>
</tbody>
</table>

フレームごとの設定にカスタム プロパティのデータに渡す、アプリは、次を行います。

1.  フレームごとの設定に関連付けられている IMFGetServices インターフェイスを取得する IFrameSettingsControls 上、QueryInterface が呼び出されます。

2.  フレームごとの設定にカスタム IMFAttributes インターフェイスを作成する IMFGetServices インターフェイスから、GetService を呼び出します。

3.  呼び出し、SetUINT32 SetBlob、カスタム プロパティの GUID をフレームごとの設定に関連付けられている IMFAttributes のカスタム プロパティのデータを設定するなど。

ドライバーに設定するフレームごとの設定のペイロードをアセンブルするときに存在する場合、カスタムの項目のペイロードを構築するカスタム IMFAttributes をフレームワークになります。

**目は、LoopCount**フィールドに**KSCAMERA\_PERFRAMESETTING\_ヘッダー**フレームごとの設定をする必要がある繰り返しの数を指定する将来のフレームに適用写真のシーケンスでキャプチャされます。 **目は、LoopCount**はパイプラインで 1 にハードコーディングされます (たとえば、フレームごとに設定がのみ適用される 1 回これ以上の繰り返しなし)。 **FrameCount**フィールドに**KSCAMERA\_PERFRAMESETTING\_ヘッダー**フレームの設定した各フレームをフレームごとの設定を適用することの数を指定します手順を繰り返します。

**ItemCount**フィールドに**KSCAMERA\_PERFRAMESETTING\_フレーム\_ヘッダー**に適用される項目の設定の数を指定します対応するフレーム。 場合**ItemCount**が 0 の対応するフレームにグローバル設定を適用する必要があります場合、。

次の表は、可能な構成と対応する写真のシーケンスの種類を示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>目は、LoopCount</th>
<th>FrameCount</th>
<th>ItemCount</th>
<th>種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>L(L=1)</p></td>
<td><p>N (N&gt;0)</p></td>
<td><p>S (S&gt;= 0)</p></td>
<td><p>シーケンスの変数の有限の写真</p></td>
</tr>
<tr class="even">
<td><p>L(L=1)</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>グローバル設定で 1 つのフレーム変数写真の有限のシーケンス</p></td>
</tr>
<tr class="odd">
<td><p>L(L=1)</p></td>
<td><p>0</p></td>
<td><p>S</p></td>
<td><p>構成が無効です。</p></td>
</tr>
</tbody>
</table>

変数の写真のシーケンスは 1 つだけの繰り返しで有限のキャプチャを実行する簡略化されました。 変数の写真のシーケンスとして別のフレームの設定を持つ写真シーケンスが常にフラグが設定して、フレームごとの設定のペイロードは常に必要です。

ループ カウントが L である場合 (L = 1) で、フレームの数は N (N &gt; 0)、有限の変数の写真が。 フレームごとの設定になります L を繰り返す N フレームの各繰り返しで次の N 将来フレームに適用される設定で 1 回を = です。

ループ カウントが L である場合 (L = 1)、フレーム数が 1、および項目数が 0 はグローバル設定で 1 つのフレーム変数の有限の写真のシーケンス。

変数の写真のシーケンスは過去のフレームを要求するさらに簡略化します。 パイプラインでは、過去の写真数、(たとえば、RequestedHistoryFrames) を 0 に、要求されたハードコーディングをされます。 ドライバーは、変数の写真のシーケンスで将来のフレームのみを提供します。 次の図は、変数の写真のシーケンス、ドライバーによって配信されるフレームの数を示します。 過去の写真の数がで指定された**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE します。RequestedHistoryFrames**によって、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE** ](ksproperty-cameracontrol-extended-photomode2.md)プロパティ コントロールを拡張パイプラインによって 0 にハードコーディングされています。

```cpp
N : Frame Count
L : Loop Count
P : Past Photos Requested
T : Total number of frame delivered by driver
L = 1
P = 0
T = (N * L) + P
```

変数の有限の写真のシーケンス、ドライバーがマークする必要があります、 **KSSTREAM\_ヘッダー。OptionsFlags**で最後のフレームの**KSSTREAM\_ヘッダー\_OPTIONSF\_ENDOFPHOTOSEQUENCE**フラグ。 これにより、ドライバーに自動的に将来のフレームが期待どおりの時間経過後に、MF パイプラインにフレームを配信を停止しますが配信されたことが保証されます。 これは、効果的に、写真のシーケンスを停止し、写真のシーケンスの完了のアプリのクライアントに通知します。 これは、ドライバーでは、有限の変数の写真のシーケンスの最後のフレームのキャプチャが完了すると発生します。

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
