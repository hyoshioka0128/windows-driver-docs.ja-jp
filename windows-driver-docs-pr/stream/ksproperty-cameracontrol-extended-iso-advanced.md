---
title: KSK プロパティ\_CAMERACONTROL\_拡張\_ISO\_詳細設定
description: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_ISO\_ADVANCED は拡張プロパティコントロールであり、より詳細なグローバル ISO 制御を可能にします。
ms.assetid: A9327DB8-422B-410C-8766-D70811BA5C73
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO_ADVANCED ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO_ADVANCED
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6a9a564ba778461221d1af59b4b98d5c80595bb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841600"
---
# <a name="ksproperty_cameracontrol_extended_iso_advanced"></a>KSK プロパティ\_CAMERACONTROL\_拡張\_ISO\_詳細設定

KSK プロパティ\_CAMERACONTROL\_EXTENDED\_ISO\_ADVANCED は拡張プロパティコントロールであり、より詳細なグローバル ISO 制御を可能にします。

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
<td><p>Pin (写真)</p></td>
<td><p>非同期</p></td>
</tr>
</tbody>
</table>

新しい KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL フラグは、次のように、ksmedia\_phone. h で定義されています。

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_MANUAL          0x0080000000000000
```

次の表に、CAMERACONTROL\_拡張\_ISO\_高度なコントロールの KSK プロパティ\_の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造フィールドの説明と要件を示します。

Windows 8.1 KS\_CAMERACONTROL\_拡張\_ISO は、整数の手動 ISO をサポートせずに変更されていません。 このドライバーでサポートされているのは、新しい KSK プロパティ\_CAMERACONTROL\_拡張\_ISO\_高度なコントロールのみです。 これらのコントロールの両方がサポートされている場合、パイプラインは既定で KSK プロパティ\_CAMERACONTROL\_拡張\_ISO\_高度なコントロールになります。

拡張\_ISO\_拡張コントロール\_\_KSK プロパティがサポートされている場合、ドライバーが提供できる機能は次のとおりです。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_AUTO

-   KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL

-   KSCAMERA\_EXTENDEDPROP\_CAPS\_ASYNCCONTROL

ドライバーが KSCAMERA\_EXTENDEDPROP\_ISO\_手動機能フラグをアドバタイズしている場合、サポートされている ISO の範囲を、KSCAMERA\_EXTENDED\_PROP\_VIDEO 設定の最小/最大/ステップ値でアドバタイズする必要があります。". ドライバーが最小値0および最大値0をアドバタイズした場合、またはステップ値が1未満の場合、コントロールは使用不可としてフラグが設定され、パイプラインによって拒否されます。

ドライバーが KSK プロパティ\_CAMERACONTROL\_拡張\_ISO\_ADVANCED および KSPROPERTY\_CAMERACONTROL\_拡張\_ISO の両方をサポートしている場合、ドライバーは KSCAMERA\_EXTENDEDPROP をアドバタイズする必要があり\_ISO\_CAMERACONTROL の両方に対して AUTO プロパティ\_CAMERACONTROL\_拡張\_ISO\_ADVANCED および KSK プロパティ\_\_拡張\_ISO。 それ以外の場合、両方の ISO コントロールは使用不可としてフラグが設定され、MF パイプラインによって拒否されます。

ドライバーが KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL の\_を KSK プロパティにアドバタイズした場合\_拡張\_ISO\_詳細および数値 KSCAMERA\_EXTENDEDPROP\_ISO\_XXXKSK プロパティの値\_CAMERACONTROL\_EXTENDED\_ISO、数値の KSCAMERA\_EXTENDEDPROP\_CAMERACONTROL でアドバタイズされた\_ISO\_XXX 値\_拡張\_ISOは、KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL が提供する、サポートされている手動 ISO 範囲に含まれている必要があります。 また、サポートされている手動の範囲のすべての数値 KSCAMERA\_EXTENDEDPROP\_ISO\_XXX 値は、KSK プロパティ\_CAMERACONTROL\_拡張\_ISO によってアドバタイズされる必要があります。 それ以外の場合、両方の ISO コントロールは使用不可としてフラグが設定され、MF パイプラインによって拒否されることがあります。

たとえば、次のいずれかの機能が致命的なエラーとして扱われ、そのコントロールが MF パイプラインによって拒否される場合があります。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL (最小 = 40、最大 = 240、ステップ = 20)、KSCAMERA\_EXTENDEDPROP\_ISO\_50

-   KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL (最小 = 40、最大 = 240、ステップ = 20)、KSCAMERA\_EXTENDEDPROP\_ISO\_80

-   KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL (最小 = 40、最大 = 240、ステップ = 20)、KSCAMERA\_EXTENDEDPROP\_ISO\_400

次のいずれかの機能は、MF パイプラインで受け入れられます。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL (最小 = 40、最大 = 240、ステップ = 20)、KSCAMERA\_EXTENDEDPROP\_ISO\_80、KSCAMERA\_EXTENDEDPROP\_ISO\_100、KSCAMERA\_EXTENDEDPROP\_ISO\_200

-   KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL (最小 = 40、最大値 = 240、ステップ = 20)

-   KSCAMERA\_EXTENDEDPROP\_ISO\_80、KSCAMERA\_EXTENDEDPROP\_ISO\_200

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
<td><p>これは、フォト pin に関連付けられている Pin ID である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これには、最後の設定操作のエラー結果が含まれます。 設定操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これは、KSCAMERA_EXTENDEDPROP_ISO_AUTO 施し KSCAMERA_EXTENDEDPROP_ISO_MANUAL と KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL フラグのビット単位で指定する必要があります。 このコントロールは非同期である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これは、上記で定義されている KSCAMERA_EXTENDEDPROP_ISO_XXX フラグのいずれかになります。</p></td>
</tr>
</tbody>
</table>

 

次の表に、ISO DDI の KSCAMERA\_EXTENDEDPROP\_VIDEOの設定の構造フィールドの説明と要件を示します。 この構造体は、ksmedia. h で定義されています。

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
<td><p>[モード]</p></td>
<td><p>これは使用されておらず、0である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/ステップ</p></td>
<td><p>Min/Max/Step には、カメラドライバーでサポートされている ISO の手動速度の最小/最大/増分が含まれます。 手動 ISO がサポートされている場合、ドライバーは GET 操作のためにこれらを返す必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>KSCAMERA_EXTENDEDPROP_HEADER の Flags フィールドで MANUAL を指定する場合は、Min/Max/Step パラメーターによって示される範囲内で、現在の ISO 速度の値を指定する必要があります。</p>
<p>Manual 以外のフラグが指定されている場合、設定操作では、VideoProc フィールドは無視されます。 GET 操作の場合、ドライバーはに関係なく、常に現在の ISO 速度を返す必要があります。</p></td>
</tr>
<tr class="even">
<td><p>予約済み</p></td>
<td><p>これは使用されません。 これは、ドライバーによって無視される必要があります。</p></td>
</tr>
</tbody>
</table>

 

**通話の取得**

ドライバーは、KSCAMERA\_EXTENDEDPROP\_ヘッダーで機能を提供する必要があります。機能と、KSCAMERA\_EXTENDEDPROP\_ヘッダーのドライバーでの現在の ISO フラグ。フラグ。 Get 呼び出しの前に設定呼び出しが実行されていない場合、ドライバーは、KSCAMERA\_EXTENDEDPROP\_ヘッダーで既定値を返します。示す.

機能 フィールドに KSCAMERA\_EXTENDEDPROP\_ISO\_手動フラグが提供されている場合、ドライバーは、サポートされている範囲を KSCAMERA\_EXTENDEDPROP\_VIDEOの設定でさらにアドバタイズする必要があります。Min/Max/Step。

また、ドライバーは、KSCAMERA\_EXTENDEDPROP\_VIDEOの設定で使用されている現在の ISO 速度を報告する必要があります。値を指定します。 GET 呼び出しの前に SET 呼び出しが実行されていない場合、ドライバーは、KSCAMERA\_EXTENDEDPROP\_VIDEOの設定で現在の ISO 速度を返します。値を指定します。

**呼び出しの設定**

KSCAMERA\_EXTENDEDPROP\_VIDEOを設定します。KSCAMERA\_EXTENDEDPROP\_ISO\_MANUAL が KSCAMERA\_EXTENDEDPROP\_ヘッダーで指定されている場合は、必要な整数の手動 ISO 速度を含む値を指定します。示す.

KSCAMERA\_EXTENDEDPROP\_ISO\_AUTO フラグが KSCAMERA\_EXTENDEDPROP\_ヘッダーで指定されている場合。フラグ、KSCAMERA\_EXTENDEDPROP\_VIDEOを設定します。VideoProc. 値. ul は無視されます。

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
