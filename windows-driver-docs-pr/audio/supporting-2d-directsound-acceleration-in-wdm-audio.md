---
title: WDM オーディオでの 2D DirectSound アクセラレータのサポート
description: WDM オーディオでの 2D DirectSound アクセラレータのサポート
ms.assetid: dbbb2416-8928-41ee-90d5-b3b77d23c251
keywords:
- ハードウェア高速化 WDK DirectSound、2D ミキシング
- 2D 混合 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 489213d8eaec5c02c744bc37cd89f3c917ac6535
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830101"
---
# <a name="supporting-2d-directsound-acceleration-in-wdm-audio"></a>WDM オーディオでの 2D DirectSound アクセラレータのサポート


## <span id="supporting_2d_directsound_acceleration_in_wdm_audio"></span><span id="SUPPORTING_2D_DIRECTSOUND_ACCELERATION_IN_WDM_AUDIO"></span>


DirectSound は、次の要件を満たす WDM オーディオミニポートドライバー用のハードウェアアクセラレータの2D 混合を公開します。

-   ミニポートドライバーには、IRP シンク (KSPIN\_通信\_シンク) であるピンファクトリが含まれています。また、kspin\_データフロー\_の kspin [ **\_データフロー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)の方向があり、データ範囲を公開します (ksk によって[ **\_AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)指定子 (**DataFormat**) を持つ構造体。**指定子**メンバー) は KSDATAFORMAT\_指定子\_DSOUND に設定されています。

-   Pin ファクトリの[**Ksk プロパティ\_ピン\_cinstances**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-cinstances)ハンドラーは、 **KSPIN\_cinstances**構造体の**PossibleCount**メンバーを2以上の値に設定します (最初の pin は常に KMixer に予約されています)。 **PossibleCount**値は、現在ピンファクトリからインスタンス化できるピンインスタンスの数を指定します。

-   Pin ファクトリは、 [**Ksk プロパティ\_AUDIO\_cpu\_resources**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-cpu-resources)プロパティをサポートしている必要があります。また、ハードウェアアクセラレーションであるすべてのノードに対して、ホスト\_CPU\_ない\_CPU\_リソースをレポートする必要があります。

-   Pin は[DirectSound ノード順序の要件](directsound-node-ordering-requirements.md)を満たしている必要があります。

 

 




