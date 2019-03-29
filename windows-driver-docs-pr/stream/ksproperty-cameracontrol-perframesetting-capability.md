---
title: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_機能
description: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_KSPROPERTY で定義されている機能のプロパティ ID\_CAMERACONTROL\_PERFRAMESETTING\_プロパティを使用して、取得、フレームごとのドライバーから機能します。
ms.assetid: 9EB8AB4C-56C0-4F70-AFFE-76444FAADFF8
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CAPABILITY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CAPABILITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 605f647216d8ca92bf86ab16caf3892ef323b965
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580289"
---
# <a name="kspropertycameracontrolperframesettingcapability"></a>KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_機能

**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_機能**で定義されているプロパティ ID [ **KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_perframesetting_property)ドライバーからフレームごとの機能を取得するために使用します。 これは GET のみコントロールです。ドライバーには、一連の呼び出しが失敗する必要があります。

## <a name="usage-summary"></a>使用状況の概要

クエリのドライバーと設定機能をフレームごとに、 **KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_機能**プロパティ コントロールをデータ バッファーと共にドライバーに送信します。 GET 呼び出しで、ドライバーが表示されます、以下で指定した形式のレイアウトを使用して提供するデータ バッファー内のフレーム設定機能ペイロードごと。

-   機能のヘッダー ([**KSCAMERA\_PERFRAMESETTING\_CAP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header))

-   項目ヘッダー ([**KSCAMERA\_PERFRAMESETTING\_CAP\_項目\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header))

-   項目ヘッダー ([**KSCAMERA\_PERFRAMESETTING\_CAP\_項目\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header))

-   項目のペイロード ([**KSPROPERTY\_ステッピング\_長い**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_stepping_long)または[ **KSPROPERTY\_ステッピング\_LONGLONG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_stepping_longlong))

機能ペイロードは、機能のヘッダーで開始する必要があります。 各機能項目が項目ヘッダーを使って開始する必要があります。 機能の項目のペイロードに項目ヘッダーは必要があります、対応する項目のペイロード続きます。

GET 呼び出しで 0 個の長バッファーには全体の機能のペイロードを保持するために必要なデータ バッファーのサイズを調べるに最初に、ドライバーに送信されます。 呼び出しに応答して、ドライバーを返す必要があります**状態\_バッファー\_OVERFLOW**以上のサイズにする必要があるバッファー サイズが必要な機能[ **KSCAMERA\_PERFRAMESETTING\_CAP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)します。

説明を次に、 **KSCAMERA\_PERFRAMESETTING\_CAP\_ヘッダー**で定義されている項目の種類のコンテキスト内のフィールド、 **KSCAMERA\_PERFRAMESETTING\_項目\_型**列挙体。 ペイロード フィールドは、後の項目のペイロード構造を表す、 **KSCAMERA\_PERFRAMESETTING\_CAP\_項目\_ヘッダー**構造体。


**公開時の項目**  

**Size**

これは、サイズの**KSCAMERA\_PERFRAMESETTING\_CAP\_ヘッダー**構造 + のサイズ、 **KSPROPERTY\_ステッピング\_LONGLONG**手動モードがサポートされている場合に構造体します。

**型**

これでなければなりません**KSCAMERA\_PERFRAMESETTING\_項目\_露出\_時間**します。

**フラグ**

これには、使用可能なフラグが含まれています。 このフィールドは、積の手順を実行して、または ksmedia.h で定義されているフラグの使用可能なフラグを含める必要があります。

```cpp
#define KSCAMERA_PERFRAMESETTING_AUTO       0x0000000100000000
#define KSCAMERA_PERFRAMESETTING_MANUAL     0x0000000200000000
```

**ペイロード**

KSPROPERTY で範囲のペイロードを指定する必要があります、ドライバーは、手動モードをサポートする場合\_ステッピング\_LONGLONG します。Bounds.SignedMinimum\\SignedMaxmum と KSPROPERTY\_ステッピング\_LONGLONG します。SteppingDelta

**フラッシュ項目**  

**Size**

これは、サイズの[ **KSCAMERA\_PERFRAMESETTING\_CAP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)構造体。

**型**

これでなければなりません**KSCAMERA\_PERFRAMESETTING\_項目\_型。KSCAMERA\_PERFRAMESETTING\_項目\_フラッシュ**

**フラグ**

これには、使用可能なフラグが含まれています。 このフィールドは、積の手順を実行して、または FLASH ksmedia.h で以下に定義されたフラグの使用可能なフラグを含める必要があります。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_OFF                                 0x0000000000000000  
#define KSCAMERA_EXTENDEDPROP_FLASH_ON                                  0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_FLASH_ON_ADJUSTABLEPOWER                  0x0000000000000002  
#define KSCAMERA_EXTENDEDPROP_FLASH_AUTO                                0x0000000000000004  
#define KSCAMERA_EXTENDEDPROP_FLASH_AUTO_ADJUSTABLEPOWER                0x0000000000000008  
#define KSCAMERA_EXTENDEDPROP_FLASH_REDEYEREDUCTION                     0x0000000000000010
```

**ペイロード**

フラッシュの項目には、ペイロードがありません。 場合 KSCAMERA\_EXTENDEDPROP\_FLASH\_ON\_ADJUSTABLEPOWER または KSCAMERA\_EXTENDEDPROP\_FLASH\_自動\_ADJUSTABLEPOWER がで指定されました。power パラメーターが 0 と 100 の範囲内では、フラグです。

**露出の補正項目**  

**Size**

これは、サイズの**KSCAMERA\_PERFRAMESETTING\_CAP\_ヘッダー**構造 + のサイズ、 **KSPROPERTY\_ステッピング\_時間の長い**手順がサポートされている場合に構造体します。

**型**

これでなければなりません**KSCAMERA\_PERFRAMESETTING\_項目\_型。KSCAMERA\_PERFRAMESETTING\_項目\_露出\_補正**

**フラグ**

これには、使用可能なフラグが含まれています。 このフィールドは、ビットごとの手順を実行して使用可能なフラグを含める必要がありますまたは、EVCOMP の ksmedia.h または自動フラグの下で定義されているフラグの下で定義 ksmedia\_phone.h します。

```cpp
#define KSCAMERA_PERFRAMESETTING_AUTO               0x0000000100000000
#define KSCAMERA_EXTENDEDPROP_EVCOMP_SIXTHSTEP      0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_QUARTERSTEP    0x0000000000000002  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_THIRDSTEP      0x0000000000000004  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_HALFSTEP       0x0000000000000008  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_FULLSTEP       0x0000000000000010
```

**ペイロード**

ドライバーは、自動モードのみをサポートする場合は、ペイロードは含まれません。 それ以外の場合、範囲のペイロードを指定する必要があります、 [ **KSPROPERTY\_ステッピング\_長い**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_stepping_long)構造体。 絶対 EV 報酬値から決定されます、min および max EV 補正の**KSPROPERTY\_ステッピング\_長。Bounds.SignedMinimum**と KSPROPERTY\_ステッピング\_長。Bounds.SignedMaximum します。 EV 補正の手順は、浮動小数点数に対応するフラグの最も低い EVCOMP 手順のステップのサイズによって決まります (たとえば、1/6 KSCAMERA\_EXTENDEDPROP\_EVCOMP\_進み)。

**ISO 速度項目**  

**Size**

これは、サイズの**KSCAMERA\_PERFRAMESETTING\_CAP\_ヘッダー**構造 + のサイズ、 **KSPROPERTY\_ステッピング\_時間の長い**手動モードがサポートされている場合に構造体します。

**型**

これでなければなりません**KSCAMERA\_PERFRAMESETTING\_項目\_型。KSCAMERA\_PERFRAMESETTING\_項目\_ISO**

**フラグ**

このフィールドには、使用可能なフラグが含まれています。 このフィールドは、ビットごとの手順を実行して、または ksmedia.h と ksmedia 以下に定義された ISO フラグの使用可能なフラグを含める必要があります\_phone.h します。 ドライバーが次の機能では、ISO の少なくとも 1 つをサポートする必要があります、フレームごとの ISO がサポートされている場合\_自動と ISO\_手動どの iso、\_自動は必須です。 場合 ISO\_手動が提供される、さらに、ドライバーはサポートされている ISO 速度の最小値を提供する可能性があります\\max\\ステップ**KSPROPERTY\_ステッピング\_長い。ISO\_手動**手動 ISO が必要な場合にサポートする必要があります。

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_MANUAL    0x0080000000000000
```

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_AUTO      0x0000000000000001
```

**ペイロード**

ドライバーは、自動モードのみをサポートする場合は、ペイロードは含まれません。 それ以外の場合、範囲のペイロードを指定する必要があります、 **KSPROPERTY\_ステッピング\_長い**構造体。 Min、max、および ISO 速度の手順はから決定**KSPROPERTY\_ステッピング\_長。Bounds.UnsignedMinimum**、K**SPROPERTY\_ステッピング\_長。Bounds.UnsignedMaximum**、および**KSPROPERTY\_ステッピング\_長。Bounds.SteppingDelta**します。 整数手動 ISO をサポートしているドライバーが ISO をアドバタイズする必要がありますのみ\_ISO 速度がサポートされているマニュアルの範囲 (最小/最大/ステップ)。 数値の ISO\_Xxx プリセットは、フレームごとの ISO のサポートされていません。

**フォーカスの項目**  

**Size**

これは、サイズの**KSCAMERA\_PERFRAMESETTING\_CAP\_ヘッダー**構造 + のサイズ、 **KSPROPERTY\_ステッピング\_時間の長い**構造体。

**型**

これでなければなりません[ **KSCAMERA\_PERFRAMESETTING\_項目\_型。KSCAMERA\_PERFRAMESETTING\_項目\_フォーカス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-kscamera_perframesetting_item_type#kscamera-perframesetting-item-focus)します。

**フラグ**

これには、使用可能なフラグが含まれています。 または ksmedis.h で以下に定義されたフラグのビットの手順を実行して、このフィールドを設定する必要があります。

```cpp
#define KSCAMERA_PERFRAMESETTING_MANUAL     0x0000000200000000
```

**ペイロード**

範囲のペイロードは、KSPROPERTY で指定する必要があります\_ステッピング\_時間構造体します。 Min、max、およびレンズの位置のステップはから決定**KSPROPERTY\_ステッピング\_長。Bounds.UnsignedMinimum**、 **KSPROPERTY\_ステッピング\_長。Bounds.UnsignedMaximum**、および**KSPROPERTY\_ステッピング\_長。SteppingDelta**します。 フォーカスをフレームごとの設定とグローバルのフォーカス設定を使用する方法、interworks の動作の定義は次のとおりです。

1.  レンズの位置が固定されます。フォーカス コマンドはありません。 継続的な自動フォーカス (カフェ) は、グローバル設定で選択されている場合は、指定したフレームに対してのみカフェ操作がオーバーライドされ、カフェが手動の指定したフォーカス後 (可能性があります全体を調べる) した後、レンズ位置に移動可能性があります。

2.  PFS で手動で設定を明示的にオーバーライドされない限り、グローバルのフォーカスの設定は常と見なされます。

3.  グローバル AF は、1 回限り手動オーバーライドが指定されていない場合に、最初のフレームにのみ適用されます。

4.  グローバルのカフェは、PFS で明示的にオーバーライドされない限り、すべてのフレームに適用されます。

5.  グローバルの手動フォーカス設定は、手動の PFS (レンズの位置のまま) 後に戻りません。

**イメージの種類の確認** 

**Size**

これは、サイズの**KSCAMERA\_PERFRAMESETTING\_CAP\_ヘッダー**構造体。

**型**

これでなければなりません**KSCAMERA\_PERFRAMESETTING\_項目\_型。KSCAMERA\_PERFRAMESETTING\_項目\_PHOTOCONFIRMATION**します。

**フラグ**

Flags フィールドには使用されません。

**ペイロード**

この項目のペイロードはありません。


**カスタム プロパティの項目**  

**Size**

これは、サイズの**KSCAMERA\_PERFRAMESETTING\_CAP\_ヘッダー**構造 + GUID のサイズ。

**型**

これでなければなりません**KSCAMERA\_PERFRAMESETTING\_項目\_型。KSCAMERA\_PERFRAMESETTING\_項目\_カスタム**します。

**フラグ**

Flags フィールドには使用されません。

**ペイロード**

これは、カスタム プロパティの GUID です。

## <a name="requirements"></a>必要条件

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
