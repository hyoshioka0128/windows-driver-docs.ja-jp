---
title: MS\_SMHBA\_SASPHYSTATISTICS WMI クラス
description: MS\_SMHBA\_SASPHYSTATISTICS WMI クラス
ms.assetid: 72afc856-8232-492f-b8d2-4e88dd9fe723
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7aa2011419a088058d243cdbbbf0a4e2643448ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844526"
---
# <a name="ms_smhba_sasphystatistics-wmi-class"></a>MS\_SMHBA\_SASPHYSTATISTICS WMI クラス


Storage Management API をサポートする HBA ミニポートドライバーは、MS\_SMHBA\_SASPHYSTATISTICS クラスを使用して、アダプターポートに関連付けられている統計情報を公開します。 各ポートには、このクラスのインスタンスが1つ存在する必要があります。

MS\_SMHBA\_SASPHYSTATISTICS クラスは、 *Hbaapi .mof*で次のように定義されています。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_SASPHYSTATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_sasphystatistics)

この WMI クラスに関連付けられているメソッドはありません。

 

 





