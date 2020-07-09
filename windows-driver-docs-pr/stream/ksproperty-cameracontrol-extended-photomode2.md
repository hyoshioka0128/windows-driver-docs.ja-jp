---
title: KSK プロパティ \_ CAMERACONTROL \_ 拡張 \_ photomode (submode)
description: KSK プロパティ \_ CAMERACONTROL \_ 拡張 photomode プロパティを使用すると、 \_ サブモードを構成できます。
ms.assetid: B5BE7B11-66FD-476C-8141-C2210B21133C
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: b8a6d32664d43cd069c47ec0fe0350e6f6bf0cbd
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128889"
---
# <a name="ksproperty_cameracontrol_extended_photomode-submode"></a>KSK プロパティ \_ CAMERACONTROL \_ 拡張 \_ photomode (submode)

KSK プロパティ \_ CAMERACONTROL \_ 拡張 photomode プロパティを使用すると、 \_ サブモードを構成できます。

## <a name="usage-summary"></a>使用状況の概要

次のサブモードは、次のように定義されています。

```cpp
#define KSCAMERA_EXTENDEDPROP_PHOTOMODE_SEQUENCE_SUB_NONE       0x00000000
#define KSCAMERA_EXTENDEDPROP_PHOTOMODE_SEQUENCE_SUB_VARIABLE   0x00000001
```

KSCAMERA \_ extendedprop \_ photomode \_ sequence \_ SUB \_ NONE は、通常の写真シーケンスで使用されます。

KSCAMERA \_ extendedprop \_ photomode \_ シーケンス \_ サブ \_ 変数は、写真シーケンスが可変であることを示すために使用されます。 フレームごとの設定を指定すると、 \_ \_ \_ \_ \_ 項目設定が指定されていない場合でも、KSCAMERA extendedprop photomode 構造の submode フィールドに KSCAMERA extendedprop photomode シーケンスサブ変数フラグが指定されて、 \_ \_ 変数の写真シーケンスが示されます (項目数はすべてのフレームに対して0になります)。 フレーム数が1で、項目数が0の場合、変数 photo sequence はグローバル設定を使用して1つのフレーム変数の写真シーケンスに減らされます。

次に、 \_ \_ ksmedia. h で定義されている KSCAMERA extendedprop photomode 構造の定義を示します。

```cpp
typedef struct tagKSCAMERA_EXTENDEDPROP_PHOTOMODE {  
    ULONG       RequestedHistoryFrames;  
    ULONG       MaxHistoryFrames;  
    ULONG       SubMode;  
    ULONG       Reserved;  
} KSCAMERA_EXTENDEDPROP_PHOTOMODE, *PKSCAMERA_EXTENDEDPROP_PHOTOMODE;
```

可変フォトシーケンスモードには、写真シーケンスに対して次のような固有の特性があります。

- 常に有限の写真シーケンスを使用します。

- フレームごとの設定は、フレーム数が0より大きい場合に適用されます。

- ドライバーは、 \_ \_ ループ数が0より大きい場合に KS videocontrolflag StopPhotoSequenceCapture トリガーを使用しなくても、最後に写真シーケンスを自動的に停止します。

- 最後のサンプルは、KSK ストリーム \_ ヘッダー \_ オプション sf ENDOFPHOTOSEQUENCE フラグでマークされている必要があり \_ ます。

- キャプチャパイプラインはドライバーからサンプルを削除しません。

- パイプラインとドライバー MFT0 のいずれも、写真のサムネイルは生成されません \\ 。

このプロパティは非同期であり、キャンセルできません。

## <a name="requirements"></a>必要条件

**ヘッダー:** Ksmedia .h (Ksk を含む)
