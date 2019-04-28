---
title: メモリ セグメントの種類の構成
description: メモリ セグメントの種類の構成
ms.assetid: a1fed4d6-60ae-42f2-9be0-98b667953606
keywords:
- メモリ セグメント WDK の表示を構成します。
- メモリのセグメントの種類、WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 070df4408d3e0f6474cb31e79b01940e6087dfe6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373006"
---
# <a name="configuring-memory-segment-types"></a>メモリ セグメントの種類の構成


## <span id="ddk_configuring_memory_segment_types_gg"></span><span id="DDK_CONFIGURING_MEMORY_SEGMENT_TYPES_GG"></span>


ビデオ メモリ マネージャーとディスプレイ ハードウェア、ディスプレイのミニポート ドライバーが構成できるは、これらの型のセグメントのみであるために、メモリのセグメントの特定の種類をのみサポートします。 ディスプレイのミニポート ドライバーには、メモリ空間セグメントには、メディア、aperture 領域セグメントは、仮想アドレス空間割り当てのビットを保持するのでは、異なるメモリ領域と aperture 領域のセグメントを構成できます。 メモリ スペースのセグメント内の範囲が割り当てられると、実際のメモリが割り当てられます。 Aperture 領域、セグメント内の範囲が割り当てられると、仮想アドレス空間は、いずれかのビデオ メモリ プールまたはシステム メモリから個別に割り当てられている物理ページにリダイレクトされます。

ディスプレイのミニポート ドライバーでは、次の種類のメモリのセグメントを構成できます。

-   [セグメントの線形のメモリ領域](linear-memory-space-segments.md)

-   [セグメントの線形 Aperture 領域](linear-aperture-space-segments.md)

-   [AGP 型 Aperture 領域セグメント](agp-type-aperture-space-segments.md)

 

 





