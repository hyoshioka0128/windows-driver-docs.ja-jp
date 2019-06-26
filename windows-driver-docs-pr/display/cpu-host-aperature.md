---
title: CPU ホスト アパーチャ
description: 32 ビットの OS の個別のグラフィックス処理ユニット (Gpu) バーのサイズをサポートしていないか、バーが失敗したときにバッファー フレームのサイズ変更、Windows Display Driver Model (WDDM) v2 では提供される独立した GPU VRAM 効率的にアクセスできる代替手段. Gpu で、アドレス スペース バーのプログラミング可能なサポート、新しい CPU ホスト Aperture 機能はその機能を抽象化する WDDM v2 で導入されました。
ms.assetid: 0E4D01E4-93AF-4205-A360-0CA3470716D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b526b75ec8d2160fb63dcde27f395ebd50463ec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370242"
---
# <a name="cpu-host-aperture"></a>CPU ホスト アパーチャ


32 ビットの OS の個別のグラフィックス処理ユニット (Gpu) バーのサイズをサポートしていないか、バーが失敗したときにバッファー フレームのサイズ変更、Windows Display Driver Model (WDDM) v2 では提供される独立した GPU VRAM 効率的にアクセスできる代替手段. Gpu で、アドレス スペース バーのプログラミング可能なサポート、新しい CPU ホスト Aperture 機能はその機能を抽象化する WDDM v2 で導入されました。

CPU ホスト開口部を公開するときに、カーネル モード ドライバーが、新しい入力[ **DXGK\_CPUHOSTAPERTURE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_cpuhostaperture) CPU ホスト開口部をサポートしている、すべてのセグメントの構造の上限を設定します。 これにより、いくつか、バーの内部用に予約するドライバーをホストの CPU 開口部のサイズ定義します。 ページ サイズは、メモリのセグメントの GPU のページと同じです。

カーネル モード ドライバーが 2 つ (Ddi) を具体的には、バーのアドレス空間を管理する新しいデバイス ドライバー インターフェイスを公開し[ *DxgkDdiMapCpuHostAperture* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_mapcpuhostaperture)と[ *DxgkDdiUnmapCpuHostAperture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_unmapcpuhostaperture)します。

ホストの CPU 開口部の背後にあるページ テーブルのメモリは、ドライバーの初期化中に早期ドライバーとセットアップによって管理されます。 両方[ *DxgkDdiMapCpuHostAperture* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_mapcpuhostaperture)と[ *DxgkDdiUnmapCpuHostAperture* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_unmapcpuhostaperture)後すぐに運用を予定しています。列挙体をセグメント化し、ビデオ メモリ マネージャーの初期化中にページ ディレクトリおよびシステムのページングのプロセスのページ テーブル アダプターの初期化中に CPU 仮想アドレスにマップするために使用します。

メモリのセグメントに CPU へのアクセスが必要な場合は、ビデオ メモリ マネージャーは、CPU ホスト開口部にページを予約ししてメモリ セグメントのページにマップします。 これは、次に示します。

![cpu ホスト aperture セグメントへのマッピング](images/cpu-host-aperture.1.png)

リンクの表示でアダプター構成の処理は、次を除くようなります。

-   *既定の*または*LinkMirrored*割り当ては、常に GPU0 にマッピングします。
-   *LinkInstanced*割り当ての仮想アドレスの範囲がある**AllocationSize**\***NumberOfGPUInLink**さまざまなパーツとそれらに関連付けられた割り当て中のさまざまな GPU にマップされます。

これを次に示します: ![cpu ホスト aperture セグメント マッピングは、リンクされたディスプレイ アダプターの構成](images/cpu-host-aperture.2.png)

 

 





