---
title: AGP のビデオ ポート ドライバー サポート
description: AGP のビデオ ポート ドライバー サポート
ms.assetid: 445dbe4a-7f7b-4dcc-9891-17fd8fb03a6c
keywords:
- ビデオミニポートドライバー WDK Windows 2000、AGP
- AGP WDK ビデオミニポート
- メモリ WDK ビデオミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dc7eef25283568b407dc5d62b08cfcb3d8882a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825278"
---
# <a name="video-port-driver-support-for-agp"></a>AGP のビデオ ポート ドライバー サポート


## <span id="ddk_video_port_driver_support_for_agp_gg"></span><span id="DDK_VIDEO_PORT_DRIVER_SUPPORT_FOR_AGP_GG"></span>


ビデオポートドライバーは、高速グラフィックスポート (AGP) をサポートするために、次の機能を実装しています。

[**AgpReservePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_physical)

[**AgpCommitPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_physical)

[**AgpReserveVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_virtual)

[**AgpCommitVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_virtual)

[**AgpFreeVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_free_virtual)

[**AgpReleaseVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_release_virtual)

[**AgpFreePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_free_physical)

[**AgpReleasePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_release_physical)

[**AgpSetRate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_set_rate)

ビデオミニポートドライバーは、前の一覧の関数を呼び出す前に、 [**Videoportqueryservices**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportqueryservices)を呼び出して関数ポインターを取得する必要があります。 AGP 関数へのポインターの取得の詳細については、「[ビデオポートドライバーによって実装される Agp 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/)」を参照してください。

ビデオミニポートドライバーは、ディスプレイアダプターがシステムメモリにアクセスできるようにするために、次の手順を実行して AGP アパーチャの一部を予約およびコミットします。

1.  [**AgpReservePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_physical)を呼び出して、AGP アパーチャに連続した範囲の物理アドレスを予約します。

2.  *AgpReservePhysical*によって返されるアドレス範囲の一部 (またはすべて) をシステムメモリ内のページにマップするには、 [**Agpcommitphysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_physical)を呼び出します。 システムメモリ内のページはロックされていますが、必ずしも連続しているわけではありません。 ビデオミニポートドライバーは、 *Agpcommitphysical*を複数回呼び出して、1つの大きなものではなく、いくつかの小さなコミットメントを行うことができます。 ただし、ドライバーは既にコミットされている範囲をコミットしようとすることはできません。

その後、アプリケーションがコミットされたページをシステムメモリ内で表示して使用できるようにするために、ビデオミニポートドライバーは次の手順を実行します。

1.  [**AgpReserveVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_virtual)を呼び出して、アプリケーションのアドレス空間に仮想アドレスの範囲を予約します。 ビデオミニポートドライバーは、 *AgpReservePhysical*によって以前に返されたハンドルを*AgpReserveVirtual*に渡す必要があります。これにより、予約済みの仮想アドレス範囲を*AgpReservePhysical*によって作成された物理アドレス範囲に関連付けることができます。

2.  *AgpReserveVirtual*によって返された仮想アドレス範囲の一部をシステムメモリ内のページにマップするには、 [**Agpcommitvirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_virtual)を呼び出します。 *Agpcommitvirtual* map のページは、 *Agpcommitvirtual*への呼び出しによって以前にマップされている必要があります。 さらに、 *Agpcommitphysical*によって確立されたマッピングは、現在も最新である必要があります。つまり、これらのページは、 [**Agpfreephysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_free_physical)の呼び出しによって解放されていない必要があります。

**  、** AGP 機能を使用してアドレス範囲 (物理または仮想) をコミットまたは予約するたびに、範囲のサイズは64キロバイトの倍数である必要があります。

 

ビデオミニポートドライバーは、次の関数を呼び出すことによって予約およびコミットされたすべてのメモリの解放と解放を担当します。

-   [**Agpfreevirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_virtual)の前の呼び出しによってシステムメモリにマップされた[**agpfreevirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_free_virtual)解除の仮想アドレス。

-   [**Agpreleasevirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_release_virtual)は、 [**AgpReserveVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_virtual)の前の呼び出しで予約された仮想アドレスを解放します。

-   [**Agpfreephysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_commit_physical)の前の呼び出しによってシステムメモリにマップされた[**agpfreephysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_free_physical)解除物理アドレス。

-   [**Agpreleasephysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_release_physical) 、 [**AgpReservePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/videoagp/nc-videoagp-pagp_reserve_physical)の前の呼び出しで予約された物理アドレスを解放します。

 

 





