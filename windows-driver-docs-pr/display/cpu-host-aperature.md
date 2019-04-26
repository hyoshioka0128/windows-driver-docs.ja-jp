---
title: CPU ホスト アパーチャ
description: 32 ビットの OS の個別のグラフィックス処理ユニット (Gpu) バーのサイズをサポートしていないか、バーが失敗したときにバッファー フレームのサイズ変更、Windows Display Driver Model (WDDM) v2 では提供される独立した GPU VRAM 効率的にアクセスできる代替手段. Gpu で、アドレス スペース バーのプログラミング可能なサポート、新しい CPU ホスト Aperture 機能はその機能を抽象化する WDDM v2 で導入されました。
ms.assetid: 0E4D01E4-93AF-4205-A360-0CA3470716D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c745c74a503fef51b1e5557e60b1618a051c8fe2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346961"
---
# <a name="cpu-host-aperture"></a>CPU ホスト アパーチャ


32 ビットの OS の個別のグラフィックス処理ユニット (Gpu) バーのサイズをサポートしていないか、バーが失敗したときにバッファー フレームのサイズ変更、Windows Display Driver Model (WDDM) v2 では提供される独立した GPU VRAM 効率的にアクセスできる代替手段. Gpu で、アドレス スペース バーのプログラミング可能なサポート、新しい CPU ホスト Aperture 機能はその機能を抽象化する WDDM v2 で導入されました。

CPU ホスト開口部を公開するときに、カーネル モード ドライバーが、新しい入力[ **DXGK\_CPUHOSTAPERTURE** ](https://msdn.microsoft.com/library/windows/hardware/dn894624) CPU ホスト開口部をサポートしている、すべてのセグメントの構造の上限を設定します。 これにより、いくつか、バーの内部用に予約するドライバーをホストの CPU 開口部のサイズ定義します。 ページ サイズは、メモリのセグメントの GPU のページと同じです。

カーネル モード ドライバーが 2 つ (Ddi) を具体的には、バーのアドレス空間を管理する新しいデバイス ドライバー インターフェイスを公開し[ *DxgkDdiMapCpuHostAperture* ](https://msdn.microsoft.com/library/windows/hardware/dn906340)と[ *DxgkDdiUnmapCpuHostAperture*](https://msdn.microsoft.com/library/windows/hardware/dn906344)します。

ホストの CPU 開口部の背後にあるページ テーブルのメモリは、ドライバーの初期化中に早期ドライバーとセットアップによって管理されます。 両方[ *DxgkDdiMapCpuHostAperture* ](https://msdn.microsoft.com/library/windows/hardware/dn906340)と[ *DxgkDdiUnmapCpuHostAperture* ](https://msdn.microsoft.com/library/windows/hardware/dn906344)後すぐに運用を予定しています。列挙体をセグメント化し、ビデオ メモリ マネージャーの初期化中にページ ディレクトリおよびシステムのページングのプロセスのページ テーブル アダプターの初期化中に CPU 仮想アドレスにマップするために使用します。

メモリのセグメントに CPU へのアクセスが必要な場合は、ビデオ メモリ マネージャーは、CPU ホスト開口部にページを予約ししてメモリ セグメントのページにマップします。 これは、次に示します。

![cpu ホスト aperture セグメントへのマッピング](images/cpu-host-aperture.1.png)

リンクの表示でアダプター構成の処理は、次を除くようなります。

-   *既定の*または*LinkMirrored*割り当ては、常に GPU0 にマッピングします。
-   *LinkInstanced*割り当ての仮想アドレスの範囲がある**AllocationSize**\***NumberOfGPUInLink**さまざまなパーツとそれらに関連付けられた割り当て中のさまざまな GPU にマップされます。

これを次に示します: ![cpu ホスト aperture セグメント マッピングは、リンクされたディスプレイ アダプターの構成](images/cpu-host-aperture.2.png)

 

 





