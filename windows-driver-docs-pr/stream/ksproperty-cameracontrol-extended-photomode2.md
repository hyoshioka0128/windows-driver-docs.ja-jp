---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE
description: KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE プロパティは、構成するサブモードを使用します。
ms.assetid: B5BE7B11-66FD-476C-8141-C2210B21133C
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: dc6d1c9c9a16088fb7579f9e7fd8c7ba85d2af60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570337"
---
# <a name="kspropertycameracontrolextendedphotomode"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE

KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE プロパティは、構成するサブモードを使用します。

## <a name="usage-summary"></a>使用状況の概要

次のサブモードの定義は次のとおりです。

```cpp
#define KSCAMERA_EXTENDEDPROP_PHOTOMODE_SEQUENCE_SUB_NONE       0x00000000
#define KSCAMERA_EXTENDEDPROP_PHOTOMODE_SEQUENCE_SUB_VARIABLE   0x00000001
```

KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_シーケンス\_SUB\_NONE が標準のフォト シーケンスで使用します。

KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_シーケンス\_SUB\_変数を使用して、写真のシーケンスが変数であることを示します。 フレームごとの設定を指定する場合、KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_シーケンス\_SUB\_変数のフラグは、KSCAMERA のサブモード フィールドで指定\_EXTENDEDPROP\_項目の設定が指定されていない場合でも写真シーケンスの変数を示し、PHOTOMODE 構造 (項目の数はすべてのフレームの場合は 0)。 フレームの数が 1 と項目 count が 0、グローバル設定を使用して 1 つのフレーム変数の写真のシーケンスに変数の写真のシーケンスが軽減されます。

次に、定義、KSCAMERA の\_EXTENDEDPROP\_ksmedia.h で定義されている PHOTOMODE 構造体

```cpp
typedef struct tagKSCAMERA_EXTENDEDPROP_PHOTOMODE {  
    ULONG       RequestedHistoryFrames;  
    ULONG       MaxHistoryFrames;  
    ULONG       SubMode;  
    ULONG       Reserved;  
} KSCAMERA_EXTENDEDPROP_PHOTOMODE, *PKSCAMERA_EXTENDEDPROP_PHOTOMODE;
```

変数写真シーケンス モードでは、写真のシーケンスの次の固有の特性があります。

-   写真の有限のシーケンスが常に使用します。

-   フレームごとのフレーム数が 0 より大きい場合、設定は適用されます。

-   ドライバーは、KS を必要としない最後に、写真のシーケンスを自動的に停止\_VideoControlFlag\_ループ カウントを 0 より大きい場合に、StopPhotoSequenceCapture トリガーを指定します。

-   前回のサンプルは、KSSTREAM と共に設定されなければなりません\_ヘッダー\_OPTIONSF\_ENDOFPHOTOSEQUENCE フラグ。

-   キャプチャ パイプラインは、ドライバーから任意のサンプルを削除できません。

-   パイプラインも、ドライバーでもない\\MFT0 任意の写真の縮小表示を生成します。

このプロパティは、非同期キャンセルできません。

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
