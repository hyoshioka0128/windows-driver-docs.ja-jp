---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_ISO\_[詳細設定]
description: KSPROPERTY\_CAMERACONTROL\_拡張\_ISO\_[詳細設定] は、拡張プロパティのコントロールにより、多くのグローバルの ISO コントロールをより細かくをします。
ms.assetid: A9327DB8-422B-410C-8766-D70811BA5C73
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO_ADVANCED ストリーミング メディア デバイス
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
ms.openlocfilehash: f0e610c54c38102ed21ee52e4a8284c2c75dc5d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558736"
---
# <a name="kspropertycameracontrolextendedisoadvanced"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_ISO\_[詳細設定]

KSPROPERTY\_CAMERACONTROL\_拡張\_ISO\_[詳細設定] は、拡張プロパティのコントロールにより、多くのグローバルの ISO コントロールをより細かくをします。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<td><p>Pin (写真)</p></td>
<td><p>非同期</p></td>
</tr>
</tbody>
</table>

新しい KSCAMERA\_EXTENDEDPROP\_ISO\_ksmedia で手動のフラグが定義されている\_phone.h として次のとおりです。

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_MANUAL          0x0080000000000000
```

次の表には、説明と要件が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)フィールドを構造体、KSPROPERTY\_CAMERACONTROL\_拡張\_ISO\_高度な制御。

Windows 8.1 の KS\_CAMERACONTROL\_拡張\_整数手動 ISO のサポートがない場合は ISO 変更されません。 ドライバーは新しい KSPROPERTY のみをサポートする必要があります\_CAMERACONTROL\_拡張\_ISO\_高度な制御。 これらのコントロールの両方がサポートされている場合、パイプラインは、KSPROPERTY 既定\_CAMERACONTROL\_拡張\_ISO\_高度な制御。

場合、KSPROPERTY\_CAMERACONTROL\_拡張\_ISO\_高度な制御がサポートされている、ドライバーが提供できるようにするだけの機能が次に示します。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_自動

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手動

-   KSCAMERA\_EXTENDEDPROP\_CAP\_ASYNCCONTROL

ドライバーは、KSCAMERA を通知する場合\_EXTENDEDPROP\_ISO\_手動機能フラグを KSCAMERA の最小/最大/ステップ値でサポートされている ISO 範囲をアドバタイズする必要がありますも\_拡張\_PROP\_VIDEOPROCSETTING プロパティ。 ドライバーは、0 の最小値と最大値は 0、またはステップ値が 1 未満のアドバタイズ、コントロールは使用不可としてフラグが設定され、パイプラインによって拒否されます。

ドライバーが両方 KSPROPERTY をサポートしている場合\_CAMERACONTROL\_拡張\_ISO\_ADVANCED および KSPROPERTY\_CAMERACONTROL\_拡張\_ISO、ドライバーの必要がありますアドバタイズ KSCAMERA\_EXTENDEDPROP\_ISO\_両方 KSPROPERTY の自動\_CAMERACONTROL\_拡張\_ISO\_KSPROPERTYし、[詳細設定]\_CAMERACONTROL\_拡張\_ISO です。 それ以外の場合、両方の ISO コントロールは、使用できなくなると、MF パイプラインによって拒否されたフラグされます。

場合は、ドライバーのアドバタイズ KSCAMERA\_EXTENDEDPROP\_ISO\_KSPROPERTY で手動\_CAMERACONTROL\_拡張\_ISO\_ADVANCED および数値 KSCAMERA\_EXTENDEDPROP\_ISO\_KSPROPERTY XXX 値\_CAMERACONTROL\_拡張\_ISO、数値の KSCAMERA\_EXTENDEDPROP\_ISO\_XXX の値でアドバタイズされた KSPROPERTY\_CAMERACONTROL\_拡張\_ISO が KSCAMERA によってサポートされている手動 ISO 範囲でなければなりません\_EXTENDEDPROP\_ISO\_手動。 さらに、すべての数値 KSCAMERA\_EXTENDEDPROP\_ISO\_KSPROPERTY によってサポートされている手動の範囲で XXX の値を提供する\_CAMERACONTROL\_拡張\_ISO です。 それ以外の場合、両方の ISO コントロールは、使用できなくなると、MF パイプラインによって拒否されたフラグ可能性があります。

たとえば、次のいずれかの機能は、重大なエラーとして扱うことができ、MF パイプラインによってコントロールが拒否されます。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手動 (最小値 = 40、240 の最大値 = ステップ = 20)、KSCAMERA\_EXTENDEDPROP\_ISO\_50

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手動 (最小値 = 40、240 の最大値 = ステップ = 20)、KSCAMERA\_EXTENDEDPROP\_ISO\_80

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手動 (最小値 = 40、240 の最大値 = ステップ = 20)、KSCAMERA\_EXTENDEDPROP\_ISO\_400

次のいずれかの機能は、MF パイプラインによって受け入れられます。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手動 (最小値 = 40、240 の最大値 = ステップ = 20)、KSCAMERA\_EXTENDEDPROP\_ISO\_80、KSCAMERA\_EXTENDEDPROP\_ISO\_100、KSCAMERA\_EXTENDEDPROP\_ISO\_200

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手動 (最小値 = 40、240 の最大値 = ステップ = 20)

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
<td><p>これは、1、</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>これには、写真の暗証番号 (pin) に関連付けられた暗証番号 (pin) の ID があります。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>Sizeof(KSCAMERA_EXTENDEDPROP_HEADER)+sizeof(KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING)、必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これには、最後の設定操作のエラーの結果が含まれています。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これは、ビット単位の KSCAMERA_EXTENDEDPROP_ISO_AUTO または施した KSCAMERA_EXTENDEDPROP_ISO_MANUAL、および KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL フラグである必要があります。 このコントロールは非同期である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 上記で定義された KSCAMERA_EXTENDEDPROP_ISO_XXX フラグのいずれかを指定できます。</p></td>
</tr>
</tbody>
</table>

 

次の表は、説明と要件、KSCAMERA\_EXTENDEDPROP\_ISO DDI VIDEOPROCSETTING 構造のフィールド。 この構造体は、ksmedia.h で定義されます。

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
<td><p>Mode</p></td>
<td><p>これにより、使用されておらず、0 にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/ステップ</p></td>
<td><p>最小/最大/ステップには、最小/最大/の増分カメラ ドライバーでサポートされる手動の ISO 速度が含まれています。 手動 ISO がサポートされている場合は、ドライバーはこれらの GET 操作で返す必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>KSCAMERA_EXTENDEDPROP_HEADER の Flags フィールドに指定すると、手動、VideoProc.Value.ul は最小/最大/ステップ パラメーターによって示された範囲内の現在の ISO 速度値を指定する必要があります。</p>
<p>設定操作で、手動以外のフラグが指定されている場合、VideoProc フィールドは無視されます。 GET 操作の場合、ドライバー返す必要があります常に ISO の現在の速度に関係なく。</p></td>
</tr>
<tr class="even">
<td><p>予約済み</p></td>
<td><p>これは使用されません。 これは、ドライバーによって無視する必要があります。</p></td>
</tr>
</tbody>
</table>

 

**呼び出しを取得します。**

ドライバーは KSCAMERA でその機能を提供する必要があります\_EXTENDEDPROP\_ヘッダー。KSCAMERA でドライバーのフラグの機能と現在の ISO\_EXTENDEDPROP\_ヘッダー。設定の呼び出しはこれまで発行されていない Flags.Â 場合、Get 呼び出しの前にドライバーは、KSCAMERA でその既定値を返す必要があります\_EXTENDEDPROP\_ヘッダー。フラグを設定します。

場合、KSCAMERA\_EXTENDEDPROP\_ISO\_手動フラグはさらに、ドライバーは KSCAMERA でサポートされている範囲を提供する可能性があります機能フィールドに、アドバタイズ\_EXTENDEDPROP\_VIDEOPROCSETTING します。最小/最大/ステップ。

ドライバーは KSCAMERA で使用されている現在の ISO 速度を報告する必要がありますも\_EXTENDEDPROP\_VIDEOPROCSETTING します。VideoProc.Value.ul します。 設定の呼び出しはこれまで発行されていない場合、GET 呼び出しの前に、ドライバーは、KSCAMERA で、現在の ISO 速度を返す必要があります\_EXTENDEDPROP\_VIDEOPROCSETTING します。VideoProc.Value.ul します。

**設定の呼び出し**

KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING します。VideoProc.Value.ul には、目的の整数手動 ISO 速度が含まれる場合 KSCAMERA\_EXTENDEDPROP\_ISO\_KSCAMERA で手動が指定された\_EXTENDEDPROP\_ヘッダー。フラグを設定します。

場合、KSCAMERA\_EXTENDEDPROP\_ISO\_KSCAMERA で自動フラグが指定された\_EXTENDEDPROP\_ヘッダー。フラグ、KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING します。VideoProc.Value.ul は無視されます。

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
