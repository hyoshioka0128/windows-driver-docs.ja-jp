---
title: KSPROPERTY_CAMERACONTROL_EXTENDED_RELATIVEPANELOPTIMIZATION
description: KSPROPERTY_CAMERACONTROL_EXTENDED_RELATIVEPANELOPTIMIZATION は、アプリケーションのアクティブな表示に対して、カメラが前面に向かっているかどうかをドライバーに通知するために使用されるプロパティ ID です。
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_CAMERACONTROL_EXTENDED_RELATIVEPANELOPTIMIZATION
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_RELATIVEPANELOPTIMIZATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 04/21/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: dc0ea2a841ac1c89235f2194e459a60a48c1e4f4
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270443"
---
# <a name="ksproperty_cameracontrol_extended_relativepaneloptimization"></a>KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ RELATIVEPANELOPTIMIZATION

**Ksproperty \_CAMERACONTROL \_ EXTENDED \_ RELATIVEPANELOPTIMIZATION**は、アプリケーションのアクティブなディスプレイを基準にして、カメラが前面に表示されるかどうかをドライバーに通知するために使用されるプロパティ ID です。 Windows は、新しい WinRT API プロパティの [Panel] を設定したときにプロパティを設定します。

Ksk プロパティコントロールの設定例については、GitHub の[Avstream カメラサンプルドライバー](https://github.com/microsoft/Windows-driver-samples/tree/master/avstream/avscamera)を参照してください。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 取得 | オン | 移行先 | プロパティ記述子の型 | プロパティ値の型 |
| --- | --- | --- | --- | --- |
| はい | はい | Assert | [KSPROPERTY](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)) | [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)|

## <a name="remarks"></a>Remarks

プロパティ要求には、 [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体と[KSCAMERA_EXTENDEDPROP_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体が含まれています。

プロパティデータの合計サイズが `sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)` です。

[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**サイズ**メンバーは、この合計プロパティデータサイズに設定されます。

KSCAMERA_EXTENDEDPROP_HEADER に配置できるフラグを次に示し**ます。フラグ**と**KSCAMERA_EXTENDEDPROP_HEADER。機能**フィールド。

| 相対パネルの最適化モード | 説明 |
| --- | --- |
| KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ OFF | カメラは通常モードの操作を使用します  |
| KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ ON  | カメラは、値フィールドに記述されている位置に対して、最適化を使用します。 |
| KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ 動的 | ストリームを glitching せずにストリーミングするときに、カメラの位置のヒントを動的に調整できます |

**KSCAMERA_EXTENDEDPROP_RELATIVEPANELOPTIMIZATION**は常に同期コントロールです。

どのアプリでもプロパティを読み取ることができますが、排他アクセス用にカメラを開いたアプリのみがプロパティ値に書き込むことができます。

排他モードアクセスを使用せずにプロパティを書き込もうとした場合は、適切なエラーコードが返されます。

この DDI を Panel Basedoptimizationcontrol にマッピングすることに関して、Panel Basedoptimizationcontrol を使用するアプリケーションでは、パネル値が設定されます。この値は、Windows がペイロードの[**KSCAMERA_EXTENDEDPROP_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)フィールドをプログラミングするために内部的に使用します。

**機能**と**フラグ**フィールドは、Windows によって制御されます。

カメラデバイスがストリーミング中で、 *KSCAMERA \_ extendedprop \_ RELATIVEPANELOPTIMIZATION \_ DYNAMIC** フラグが設定されていないときに、ドライバーが設定操作を受け取ると、ドライバーは状態ベースのエラーを返します。

次の表に、メタデータコントロールを使用する場合の[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造のフィールドの要件を示します。

| メンバー | 説明 |
| --- | --- |
| Version | これは1である必要があります。 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) |
| サイズ | これは sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) である必要があります |
| 結果 | 最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。 |
| 機能 | **は**、上記で定義されている、サポートされている***KSCAMERA_EXTENDEDPROP_RELATIVEPANELOPTIMIZATION_XXX***フラグのビット単位である必要があります。 |
| Flags | これは、読み取り/書き込みフィールドです。 これは、上で定義された**KSCAMERA_EXTENDEDPROP_RELATIVEPANELOPTIMIZATION_ON**または**KSCAMERA_EXTENDEDPROP_RELATIVEPANELOPTIMIZATION_OFF**フラグのいずれかになります。 |

**KSCAMERA \_ extendedprop \_ RELATIVEPANELOPTIMIZATION \_ ON**が[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**フィールドに指定されている場合は、この**ul**フィールドで、カメラが現在接続している相対的な方向の pld を指定する必要があります。

これは ACPI PLD の列挙値のいずれかにすることができますが、最も頻繁に使用されるのは、 **Front**、 **Back** 、または**Unknown**です。

**KSCAMERA \_ extendedprop \_ RELATIVEPANELOPTIMIZATION \_ OFF**が指定されている場合、設定操作では、**値**フィールドは無視されます。

GET 操作の場合、ドライバーはカメラが現在プログラミングされている方向を返す必要があります。

**KSCAMERA \_ extendedprop \_ RELATIVEPANELOPTIMIZATION \_ OFF**が指定されている場合、または値が設定されていない場合は、デバイスの既定の pld が返される必要があります。

**KSCAMERA \_ extendedprop \_ RELATIVEPANELOPTIMIZATION \_ ON**が指定されている場合は、最後に設定された値が返される必要があります。

## <a name="requirements"></a>必要条件

| &nbsp; | &nbsp; |
| --- | --- |
| ヘッダー | ksmedia .h (Ksk を含む) |
