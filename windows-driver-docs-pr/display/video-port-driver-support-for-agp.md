---
title: AGP のビデオ ポート ドライバー サポート
description: AGP のビデオ ポート ドライバー サポート
ms.assetid: 445dbe4a-7f7b-4dcc-9891-17fd8fb03a6c
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、AGP
- AGP WDK ビデオのミニポート
- メモリ WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0170a9ebfc96a914200dfafbdf842e15c208983
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353823"
---
# <a name="video-port-driver-support-for-agp"></a>AGP のビデオ ポート ドライバー サポート


## <span id="ddk_video_port_driver_support_for_agp_gg"></span><span id="DDK_VIDEO_PORT_DRIVER_SUPPORT_FOR_AGP_GG"></span>


ビデオ ポート ドライバーでは、高速化グラフィックス ポート (AGP) をサポートするために、次の関数を実装します。

[**AgpReservePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_reserve_physical)

[**AgpCommitPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_commit_physical)

[**AgpReserveVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_reserve_virtual)

[**AgpCommitVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_commit_virtual)

[**AgpFreeVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_free_virtual)

[**AgpReleaseVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_release_virtual)

[**AgpFreePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_free_physical)

[**AgpReleasePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_release_physical)

[**AgpSetRate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_set_rate)

呼び出すことで関数ポインターを取得する必要があります、ビデオのミニポート ドライバーでは、関数を呼び出す上記の一覧で、前に[ **VideoPortQueryServices**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportqueryservices)します。 AGP 関数へのポインターを取得する方法の詳細については、次を参照してください。 [AGP ビデオ ポート ドライバーによって関数が実装されている](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/)します。

ビデオのミニポート ドライバーでは、予約し、ディスプレイ アダプターがシステム メモリをアクセス AGP aperture の一部をコミットするには、次の手順を実行します。

1.  呼び出す[ **AgpReservePhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_reserve_physical) AGP aperture の物理アドレスの連続する範囲を予約します。

2.  呼び出す[ **AgpCommitPhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_commit_physical)によって返されるアドレスの範囲の一部 (またはすべて) にマップする*AgpReservePhysical*システム メモリ内のページにします。 システム メモリ内のページは、ロックされたが、必ずしも連続していません。 ビデオのミニポート ドライバーが呼び出せる*AgpCommitPhysical*何回か 1 つの大きな 1 つではなく、いくつかの小規模なコミットメントを行う。 ただし、ドライバーは、既にコミットされている範囲をコミットする必要があります試行されません。

次に、表示され、システム メモリ内でコミットされたページを使用できるアプリケーションは、ビデオのミニポート ドライバーは、次の手順を実行します。

1.  呼び出す[ **AgpReserveVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_reserve_virtual)アプリケーションのアドレス空間内の仮想アドレスの範囲を予約します。 ビデオのミニポート ドライバーを渡す必要があります*AgpReserveVirtual*ハンドルによって以前返さを*AgpReservePhysical*予約済みの仮想アドレスの範囲を物理アドレスに関連付けできるように、によって作成された範囲*AgpReservePhysical*します。

2.  呼び出す[ **AgpCommitVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_commit_virtual)によって返される仮想アドレスの範囲の一部をマップする*AgpReserveVirtual*システム メモリ内のページにします。 ページを*AgpCommitVirtual*マップする必要がありますマップされている以前の呼び出しによって*AgpCommitPhysical*します。 によってさらに、そのマッピングが確立されている*AgpCommitPhysical*する必要がある現在; は、これらのページする必要がありますが解放されていない呼び出しによって[ **AgpFreePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_free_physical)。

**注**   AGP 関数を使用してコミットするか、(物理または仮想) のアドレス範囲を予約するたびに、範囲のサイズが 64 キロバイトの倍数をある必要があります。

 

ビデオのミニポート ドライバーは予約されている、次の関数を呼び出すことでコミットことのすべてのメモリを解放するためです。

-   [**AgpFreeVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_free_virtual)前回の呼び出しによって、システム メモリにマップされている仮想アドレスの割り当てを解除[ **AgpCommitVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_commit_virtual)します。

-   [**AgpReleaseVirtual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_release_virtual)前回の呼び出しによって予約されている仮想アドレスの解放[ **AgpReserveVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_reserve_virtual)します。

-   [**AgpFreePhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_free_physical)前回の呼び出しによって、システム メモリにマップされている物理アドレスの割り当てを解除[ **AgpCommitPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_commit_physical)します。

-   [**AgpReleasePhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_release_physical)前回の呼び出しによって予約されている物理アドレスを解放[ **AgpReservePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/videoagp/nc-videoagp-pagp_reserve_physical)します。

 

 





