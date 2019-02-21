---
title: KSPROPSETID\_SoundDetector
description: .
ms.assetid: FC4A354B-D42C-4199-B613-1E1B75A600C6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f43a3289241254c514a0b1ae2964e04fd225f74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549703"
---
# <a name="kspropsetidsounddetector"></a>KSPROPSETID\_SoundDetector


`KSPROPSETID_SoundDetector`プロパティ セットには、検出機能をサポートするオーディオ キャプチャ デバイス用のフィルターの登録に使用されるプロパティが含まれています。 フィルターがピン留めするカテゴリをある KS pin ファクトリ**KSNODETYPE\_オーディオ\_KEYWORDDETECTOR**します。 KS フィルター インスタンスでこの KS 暗証番号 (pin) カテゴリを持つ 1 つ以上のピン留めするファクトリを設定することはできません。

このセット内のプロパティ項目がで指定された[ **KSPROPERTY\_SOUNDDETECTOR** ](ksproperty-sounddetector.md)列挙値、ヘッダー ファイルで定義されている*ksmedia.h*します。

ヘッダー ファイルの定義、 **KSPROPSETID\_SoundDetector**プロパティを次のように設定します。

``` syntax
#define STATIC_KSPROPSETID_SoundDetector\
    0x113c425e, 0xfd17, 0x4057, 0xb4, 0x22, 0xed, 0x40, 0x74, 0xf1, 0xaf, 0xdf
DEFINE_GUIDSTRUCT("113C425E-FD17-4057-B422-ED4074F1AFDF", KSPROPSETID_SoundDetector);
#define KSPROPSETID_SoundDetector DEFINE_GUIDNAMED(KSPROPSETID_SoundDetector)
```

`KSPROPSETID_SoundDetector`プロパティ セットには、次のプロパティが含まれています。

-   [**KSPROPERTY\_SOUNDDETECTOR\_故障**](ksproperty-sounddetector-armed.md)

-   [**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

-   [**KSPROPERTY\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)

-   [**KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md)

 

 





