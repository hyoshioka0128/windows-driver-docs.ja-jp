---
title: CPU ホスト アパーチャ
description: サイズ変更可能なバーをサポートしていない32ビット OS の個別のグラフィックスプロセッシングユニット (Gpu)、またはフレームバッファーバーのサイズ変更が失敗した場合、Windows Display Driver Model (WDDM) v2 は、個別の GPU VRAM を効率的にアクセスできるようにするための別のメカニズムを提供します. プログラム可能なバーのアドレス空間をサポートする Gpu の場合は、その機能を抽象化するために、新しい CPU ホスト絞り機能が WDDM v2 で導入されています。
ms.assetid: 0E4D01E4-93AF-4205-A360-0CA3470716D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e1d599eba770d452e481b1584ece7bb2c696752
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839782"
---
# <a name="cpu-host-aperture"></a>CPU ホスト アパーチャ


サイズ変更可能なバーをサポートしていない32ビット OS の個別のグラフィックスプロセッシングユニット (Gpu)、またはフレームバッファーバーのサイズ変更が失敗した場合、Windows Display Driver Model (WDDM) v2 は、個別の GPU VRAM を効率的にアクセスできるようにするための別のメカニズムを提供します. プログラム可能なバーのアドレス空間をサポートする Gpu の場合は、その機能を抽象化するために、新しい CPU ホスト絞り機能が WDDM v2 で導入されています。

CPU ホストのアパーチャを公開すると、カーネルモードドライバーは、CPU ホストのアパーチャをサポートするすべてのセグメントについて、新しい[**DXGK\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_cpuhostaperture) CPU ホストアパーチャキャップの構造を入力します。 これにより、CPU ホストのアパーチャのサイズが定義されます。これにより、ドライバーは内部目的でバーの一部を予約できます。 ページサイズは、メモリセグメントの GPU ページと同じです。

次に、カーネルモードドライバーが2つの新しいデバイスドライバーインターフェイス (DDIs) を公開し、バーのアドレス空間を管理します (特に[*DxgkDdiMapCpuHostAperture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_mapcpuhostaperture)と[*DxgkDdiUnmapCpuHostAperture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_unmapcpuhostaperture))。

CPU ホストアパーチャの背後にあるページテーブルのメモリはドライバーによって管理され、ドライバーの初期化時に初期設定されます。 [*DxgkDdiMapCpuHostAperture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_mapcpuhostaperture)と[*DxgkDdiUnmapCpuHostAperture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_unmapcpuhostaperture)は、どちらもセグメント列挙の直後に動作し、ビデオメモリマネージャーの初期化時に CPU 仮想アドレスをページにマップするために使用されます。アダプターの初期化中にシステムのページングプロセスのディレクトリとページテーブル。

メモリセグメントへの CPU アクセスが必要な場合は、ビデオメモリマネージャーによって CPU ホストの絞りのページが予約され、メモリセグメントのページがマップされます。 次に例を示します。

![cpu ホストのアパーチャセグメントのマッピング](images/cpu-host-aperture.1.png)

リンクされたディスプレイアダプターの構成は、次の点を除けば似ています。

-   *既定値*または*linkmirrored*の割り当ては常に GPU0 にマップされます。
-   *Linkinstanced*割り当てには、割り当て**サイズ**\***numberofgpuinlink**の仮想アドレス範囲が割り当てられています。これに関連付けられているアロケーションのさまざまな部分が、異なる GPU にマップされています。

次に示すのは、リンクされたディスプレイアダプター構成の ![cpu ホストのアパーチャセグメントマッピング](images/cpu-host-aperture.2.png)

 

 





