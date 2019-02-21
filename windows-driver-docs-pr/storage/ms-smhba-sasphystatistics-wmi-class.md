---
title: MS\_SMHBA\_SASPHYSTATISTICS WMI クラス
description: MS\_SMHBA\_SASPHYSTATISTICS WMI クラス
ms.assetid: 72afc856-8232-492f-b8d2-4e88dd9fe723
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 57f77419a5dab6d18461bbe37a3eb83b3d744ae8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530798"
---
# <a name="mssmhbasasphystatistics-wmi-class"></a>MS\_SMHBA\_SASPHYSTATISTICS WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SMHBA\_SASPHYSTATISTICS クラスは、アダプターのポートに関連付けられている統計情報を公開します。 このクラスの各ポートの 1 つのインスタンスが必要です。

MS\_SMHBA\_SASPHYSTATISTICS クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SMHBA_SASPHYSTATISTICS
{
    [WmiDataId(1)]
    sint64 SecondsSinceLastReset;

    [WmiDataId(2)]
    sint64 TxFrames;

    [WmiDataId(3)]
    sint64 TxWords;

    [WmiDataId(4)]
    sint64 RxFrames;

    [WmiDataId(5)]
    sint64 RxWords;

    [WmiDataId(6)]
    sint64 InvalidDwordCount;

    [WmiDataId(7)]
    sint64 RunningDisparityErrorCount;

    [WmiDataId(8)]
    sint64 LossofDwordSyncCount;

    [WmiDataId(9)]
    sint64 PhyResetProblemCount;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_SASPHYSTATISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff563175)

この WMI クラスに関連付けられているメソッドはありません。

 

 





