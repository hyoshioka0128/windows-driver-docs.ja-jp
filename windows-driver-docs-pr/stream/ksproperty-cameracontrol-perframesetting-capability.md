---
title: KSPROPERTY\_CAMERACONTROL\_PERフレーム設定\_機能
description: Ksk プロパティ\_CAMERACONTROL\_PERFRAME 設定\_、KSK プロパティ\_CAMERACONTROL\_PERフレーム設定\_プロパティを使用して、ドライバーからフレームごとの機能を取得します。
ms.assetid: 9EB8AB4C-56C0-4F70-AFFE-76444FAADFF8
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CAPABILITY ストリーミングメディアデバイス
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
ms.openlocfilehash: 715305b681160e7c733ed434e56b77e5ef87c3f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842494"
---
# <a name="ksproperty_cameracontrol_perframesetting_capability"></a>KSPROPERTY\_CAMERACONTROL\_PERフレーム設定\_機能

Ksk プロパティ **\_CAMERACONTROL\_PERフレーム設定\_の機能**プロパティ ID を指定します。この ID は、 [**KSK プロパティ\_CAMERACONTROL\_PERフレーム設定\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_perframesetting_property)を使用してフレームごとに取得します。ドライバーの機能。 これは GET のみの制御です。ドライバーは、すべての SET 呼び出しを失敗させる必要があります。

## <a name="usage-summary"></a>使用状況の概要

ドライバーを使用してフレーム設定機能ごとにクエリを実行するには、 **Ksk プロパティ\_CAMERACONTROL\_PERフレーム設定\_機能**プロパティコントロールが、データバッファーと共にドライバーに送信されます。 GET 呼び出しでは、ドライバーは、以下で指定された書式レイアウトを使用して提供されるデータバッファー内のフレーム設定機能ペイロードごとに値を設定します。

-   機能ヘッダー ([**KSCAMERA\_PERフレーム設定\_CAP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header))

-   項目ヘッダー ([**KSCAMERA\_PERフレーム設定\_CAP\_項目\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header))

-   項目ヘッダー ([**KSCAMERA\_PERフレーム設定\_CAP\_項目\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header))

-   項目のペイロード ([**ksk プロパティ\_ステップ実行\_LONG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long)または[**KSK プロパティ\_ステップ\_longlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_longlong))

機能ペイロードは、機能ヘッダーで始める必要があります。 各機能項目は、項目ヘッダーで始める必要があります。 機能項目にペイロードが含まれている場合は、項目ヘッダーの後に対応する項目ペイロードが必要です。

GET 呼び出しでは、機能ペイロード全体を保持するために必要なデータバッファーサイズを確認するために、最初にゼロ長のバッファーがドライバーに送信されます。 呼び出しへの応答として、ドライバーは、少なくとも[**KSCAMERA\_PERフレーム設定\_CAP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)のサイズ以上である必要な機能バッファーサイズを使用して、**状態\_バッファー\_オーバーフロー**を返す必要があります。

次に示すのは、 **KSCAMERA\_PERフレーム設定\_item\_TYPE 列挙型**に定義されている項目の種類のコンテキストにおける、 **KSCAMERA\_perフレーム設定\_CAP\_ヘッダー**フィールドの説明です。 ペイロードフィールドは、 **KSCAMERA\_PERフレーム設定\_CAP\_item\_HEADER**構造体の後にある項目のペイロード構造を表します。


**露出時間項目**  

**サイズ**

手動モードがサポートされている場合は、 **KSCAMERA\_PERフレーム設定\_CAP\_ヘッダー**構造のサイズと、 **ksproperty のサイズ\_ステップ実行\_longlong**構造体です。

**型**

**\_PERフレーム設定\_項目\_露出\_時間**にする必要があります。

**示す**

これには、使用可能なフラグが含まれます。 このフィールドには、ksmedia. h に定義されているフラグのビット単位またはフラグを指定することによって使用可能なフラグが含まれている必要があります。

```cpp
#define KSCAMERA_PERFRAMESETTING_AUTO       0x0000000100000000
#define KSCAMERA_PERFRAMESETTING_MANUAL     0x0000000200000000
```

**ペイ**

ドライバーが手動モードをサポートしている場合は、範囲ペイロードを KSK プロパティに指定して、ステップ実行\_LONGLONG に\_する必要があります。SignedMaxmum および KSK プロパティ\_ステップ実行\_LONGLONG の\\。SteppingDelta

**Flash 項目**  

**サイズ**

これは、 [**KSCAMERA\_PERフレーム設定\_CAP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)構造のサイズです。

**型**

**\_PERフレーム設定\_項目\_型である必要があります。KSCAMERA\_PERフレーム設定\_項目\_FLASH**

**示す**

これには、使用可能なフラグが含まれます。 このフィールドには、次の ksmedia. h で指定されている、ビット単位またはフラッシュフラグを使用して利用可能なフラグが含まれている必要があります。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_OFF                                 0x0000000000000000  
#define KSCAMERA_EXTENDEDPROP_FLASH_ON                                  0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_FLASH_ON_ADJUSTABLEPOWER                  0x0000000000000002  
#define KSCAMERA_EXTENDEDPROP_FLASH_AUTO                                0x0000000000000004  
#define KSCAMERA_EXTENDEDPROP_FLASH_AUTO_ADJUSTABLEPOWER                0x0000000000000008  
#define KSCAMERA_EXTENDEDPROP_FLASH_REDEYEREDUCTION                     0x0000000000000010
```

**ペイ**

Flash 項目にペイロードがありません。 KSCAMERA\_EXTENDEDPROP\_FLASH\_ON\_ADJUSTABLEPOWER または KSCAMERA\_EXTENDEDPROP\_FLASH\_AUTO\_ADJUSTABLEPOWER がフラグに指定されている場合、power パラメーターは 0 ~ 100 の範囲内です。

**露出補正項目**  

**サイズ**

これは、手順がサポートされている場合に **\_ヘッダー構造\_CAP ヘッダー**構造のサイズと**ksk プロパティのサイズ\_ステップ実行\_長い**構造体の\_です。

**型**

**\_PERフレーム設定\_項目\_型である必要があります。KSCAMERA\_PERフレーム設定\_項目\_露出\_補正**

**示す**

これには、使用可能なフラグが含まれます。 このフィールドには、次の手順で定義されている、ksmedia .h または次のように定義されている自動フラグを使用して使用可能なフラグが含まれている必要があります ksk media\_phone .h です。

```cpp
#define KSCAMERA_PERFRAMESETTING_AUTO               0x0000000100000000
#define KSCAMERA_EXTENDEDPROP_EVCOMP_SIXTHSTEP      0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_QUARTERSTEP    0x0000000000000002  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_THIRDSTEP      0x0000000000000004  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_HALFSTEP       0x0000000000000008  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_FULLSTEP       0x0000000000000010
```

**ペイ**

ドライバーが auto モードのみをサポートしている場合は、ペイロードは含まれません。 それ以外の場合は、範囲ペイロードを指定する必要があります[**Ksk プロパティ\_ステップ\_長い**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long)構造体です。 EV 補正の最小値と最大値は、絶対 EV 補正値であり、\_ステップ実行\_の Ksk プロパティから決定され**ます。Bounds. SignedMinimum**と KSK プロパティ\_ステップ実行\_LONG です。境界. SignedMaximum。 EV 補正のステップは、float に対応する最も低い EVCOMP ステップフラグのステップサイズによって決まります (たとえば1/6、KSCAMERA\_EXTENDEDPROP\_EVCOMP\_SIXTHSTEP)。

**ISO の速度項目**  

**サイズ**

これは、手動モードがサポートされている場合に、\_CAP\_ヘッダー構造のサイズと、 **\_を\_ステップ**実行するための **\_perフレーム設定**のサイズです。

**型**

**\_PERフレーム設定\_項目\_型である必要があります。KSCAMERA\_PERフレーム設定\_項目\_ISO**

**示す**

このフィールドには、使用可能なフラグが含まれています。 このフィールドには、次のように指定されている ISO フラグを使用して使用可能なフラグを含める必要があります、ksmedia .h と ksk メディア\_します。 フレームごとの ISO がサポートされている場合、ドライバーは、iso\_AUTO および ISO\_MANUAL の少なくとも1つの機能をサポートする必要があります。 iso\_AUTO は必須です。 ISO\_MANUAL が提供されている場合は、サポートされている ISO speed min\\max\\の最大ステップを Ksk プロパティ\_ステップ実行\_にさらにアドバタイズする必要があり**ます。Iso\_マニュアル**は、iso を手動で使用する必要がある場合にサポートする必要があります。

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_MANUAL    0x0080000000000000
```

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_AUTO      0x0000000000000001
```

**ペイ**

ドライバーが auto モードのみをサポートしている場合は、ペイロードは含まれません。 それ以外の場合は、範囲ペイロードを指定する必要があります**Ksk プロパティ\_ステップ\_長い**構造体です。 ISO 速度の最小値、最大値、および手順は、 **Ksk プロパティ\_ステップ実行\_の長さによって決まります。Bounds。 UnsignedMinimum**、K**sproperty\_ステップ実行\_LONG です。範囲。 UnsignedMaximum**、および**ksk プロパティ\_ステップ実行\_LONG です。SteppingDelta**。 整数の手動 ISO をサポートするドライバーでは、iso\_手動で、サポートされている ISO 速度範囲 (最小/最大/ステップ) のみを提供する必要があります。 数値 ISO\_Xxx プリセットは、フレームごとの ISO ではサポートされていません。

**フォーカス項目**  

**サイズ**

これは、 **KSCAMERA\_PERフレーム設定\_CAP\_ヘッダー**構造のサイズと、 **\_ステップ実行\_長い**構造体のサイズです。

**型**

[ **\_PERフレーム設定\_項目\_型である必要があります。KSCAMERA\_PERフレームの設定\_項目\_フォーカス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_perframesetting_item_type#kscamera-perframesetting-item-focus)します。

**示す**

これには、使用可能なフラグが含まれます。 このフィールドを設定するには、ksmedis で以下のように定義されているフラグを指定する必要があります。

```cpp
#define KSCAMERA_PERFRAMESETTING_MANUAL     0x0000000200000000
```

**ペイ**

範囲ペイロードは、\_長い構造体をステップ実行\_に、KSK プロパティに指定する必要があります。 レンズ位置の最小値、最大値、および手順は、 **Ksk プロパティ\_ステップ実行\_の長さによって決まります。範囲。 UnsignedMinimum**、 **ksk プロパティ\_ステップ\_LONG です。範囲。 UnsignedMaximum**、および**ksk プロパティ\_ステップ実行\_LONG です。SteppingDelta**。 フレームごとの設定フォーカスの動作と、グローバルフォーカス設定との相互作用のしくみは、次のように定義されています。

1.  レンズの位置は固定されています。ただし、フォーカスコマンドはありません。 グローバル設定で連続自動フォーカス (CAF) が選択されている場合、CAF 操作は、指定されたフレームに対してのみオーバーライドされます。 CAF は、手動フォーカスを指定した後、レンズ位置 (通常はフルスイープの後) を移動します。

2.  グローバルフォーカス設定は、PFS の手動設定で明示的にオーバーライドされない限り、常に想定されます。

3.  グローバル AF はワンショットで、手動オーバーライドが指定されていない場合は最初のフレームにのみ適用されます。

4.  グローバル CAF は、PFS によって明示的にオーバーライドされない限り、すべてのフレームに適用されます。

5.  グローバルな手動フォーカス設定は、手動の PFS (レンズの位置のまま) の後には戻りません。

**確認の画像の種類** 

**サイズ**

これは、 **KSCAMERA\_PERフレーム設定\_CAP\_ヘッダー**構造のサイズです。

**型**

**\_PERフレーム設定\_項目\_型である必要があります。KSCAMERA\_PERフレーム設定\_項目\_PHOTOCONFIRMATION**です。

**示す**

Flags フィールドは使用されません。

**ペイ**

この項目にはペイロードがありません。


**カスタムプロパティ項目**  

**サイズ**

これは、 **KSCAMERA\_PERフレーム設定\_CAP\_ヘッダー**構造のサイズと GUID のサイズです。

**型**

**\_PERフレーム設定\_項目\_型である必要があります。KSCAMERA\_PERフレームの設定\_項目\_カスタム**です。

**示す**

Flags フィールドは使用されません。

**ペイ**

これはカスタムプロパティ GUID です。

## <a name="requirements"></a>前提条件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Ksmedia. h</td>
</tr>
</tbody>
</table>
