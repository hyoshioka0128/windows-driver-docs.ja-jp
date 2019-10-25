---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VIDEOSTABILIZATION
description: この拡張プロパティコントロールは、ドライバー\\MFT0 のデジタルビデオ安定化を制御するために使用されます。
ms.assetid: 60F7D1B2-02F1-459A-8F6A-FC61D65705E1
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOSTABILIZATION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOSTABILIZATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: e9c85ba2466499f5ccefe7633cbe13824ef37dd4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826200"
---
# <a name="ksproperty_cameracontrol_extended_videostabilization"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VIDEOSTABILIZATION

この拡張プロパティコントロールは、ドライバー\\MFT0 のデジタルビデオ安定化を制御するために使用されます。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

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

次のフラグは、KSCAMERA\_EXTENDEDPROP\_ヘッダーに配置できます。ドライバー\\MFT0 のデジタルビデオ安定化を制御するフラグフィールドフラグを指定します。 既定では、ドライバーはビデオが安定化されている必要があります。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_OFF       0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_ON        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_AUTO      0x0000000000000002
```

ドライバーがデジタルビデオ安定化をサポートしていない場合、ドライバーはこのコントロールを実装しないでください。

ドライバーがこのコントロールをサポートしている場合は、\\オフになっている VIDEOSTABILIZATION\_をサポートする必要があります。

このコントロールの SET 呼び出しは、ビデオの pin が KSK 状態\_停止状態よりも大きい状態にある場合は効果がありません。 ビデオの pin が停止状態ではない場合、ドライバーは受信した設定の呼び出しを拒否し、デバイス\_状態\_無効\_状態を返します。 GET 呼び出しでは、ドライバーは Flags フィールドの現在の設定を返します。

このコントロールがプロファイルのコンテキストで使用される場合、プロファイルは品質モードのドライバーのヒントとして機能します。 ドライバーは、選択したプロファイルに基づいてビデオの安定化が有効になっている場合、低待機時間と高品質のどちらを最適化するかを決定できます。たとえば、ビデオ会議や高品質のビデオ記録などです。

> [!NOTE]
> PROPSETID\_VIDCAP\_CAMERACONTROL\_VIDEO\_安定化は Windows 10 で非推奨となります。

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
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_OFF</p></td>
<td><p>これは必須の機能です。 指定した場合、driver\MFT0. でデジタルビデオ安定化が無効になります。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_ON</p></td>
<td><p>これは必須の機能です。 このオプションを指定すると、driver\MFT0 でデジタルビデオの安定化が有効になり、既定のオーバースキャンの設定はドライバーによって有効になります。 このフラグは、AUTO および OFF フラグと同時に指定することはできません。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_AUTO</p></td>
<td><p>この機能は省略可能です。 指定した場合、このような機能をサポートするドライバーは、ビデオ安定化を実行する必要があるかどうか、およびシーン分析とキャプチャシナリオに基づいて適用される安定化の量を決定します。 このフラグは、ON および OFF フラグと同時に指定することはできません。</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 実装によっては、過剰にスキャンされたバッファーが、内部的に、またはパイプラインによって、ドライバーによって割り当てられる場合があります。

過剰スキャンされたバッファーがドライバーによって割り当てられる場合、ドライバーは通常のメディアの種類と過剰にスキャンされたメディアの種類の両方をアドバタイズする必要があります。 MFT0 は、通常のメディアの種類をアドバタイズする必要があります。 MFT0 の出力メディアの種類で通常のメディアの種類を設定すると、ビデオ安定化が有効になっている場合、MFT0 は入力メディアの種類として、提供されたメディアの種類として、対応する過剰スキャンされたメディアの種類を選択する必要があります。 ビデオの安定化がオフになっている場合、MFT0 は入力メディアの種類として通常のメディアの種類を選択する必要があります。 MFT0 は、ビデオ安定化が有効になっているときに、過剰スキャンされたメディアの種類が出力メディアの種類として設定されている場合、MF\_E\_INVALIDMEDIATYPE を返します。

過剰スキャンされたバッファーがドライバーによって割り当てられている場合、ドライバーと MFT0 の両方が通常のメディアの種類をアドバタイズする必要があります。 MFT0 は、入力メディアの種類と出力メディアの種類の両方に通常のメディアの種類を設定する必要があります。

効果ベースのビデオ安定化をサポートするために (つまり、ドライバーでも MFT0 でもビデオの安定化が行われていません)、ドライバーと MFT0 はに関係なく、過剰にスキャンされたメディアの種類をさらにアドバタイズする必要があります。 この場合、通常のメディアと過剰にスキャンされたメディアの種類は、ドライバーと MFT0 によって公開されます。 次の規則が適用されて、効果ベースとドライバー\\MFT0 ベースのビデオ安定化が正常に機能していることを確認します。

-   ドライバー\\MFT0 based video 安定化がオンになっているときに、過剰スキャンされたメディアの種類が MFT0 の出力メディアの種類として設定されている場合、MFT0 はを\_\_返します。

-   通常のメディアの種類が MFT0 出力メディアの種類として設定されている場合、効果ベースのビデオ安定化が過剰にスキャンされたメディアの種類のみを使用できる場合、アプリは効果ベースのビデオ安定化をオンにしようとしてエラーを返します。

次の表には、ビデオ安定化コントロールを使用する場合の[KSCAMERA\_EXTENDEDPROP\_ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造フィールドの説明と要件が含まれています。

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
<td><p>は、ビデオ pin に関連付けられている Pin ID である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これは、前述のように、サポートされている KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_XXX フラグのビットごとの OR である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これには、上記で定義されている KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_XXX フラグのいずれかを指定できます。</p></td>
</tr>
</tbody>
</table>

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
