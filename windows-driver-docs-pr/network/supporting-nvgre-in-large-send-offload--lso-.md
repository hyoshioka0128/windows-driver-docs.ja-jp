---
title: Large Send Offload (LSO) での NVGRE のサポート
description: このセクションでは、NVGRE で Large Send Offload (LSO) のサポートについて説明します
ms.assetid: 1EB1B8C2-85C1-4256-BE96-C8B9F1D222B6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 833c4ca772178774ad31b040effd5e41183400fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574040"
---
# <a name="supporting-nvgre-in-large-send-offload-lso"></a>Large Send Offload (LSO) での NVGRE のサポート


NDIS 6.30 (Windows Server 2012) が導入されています[Network Virtualization using Generic Routing Encapsulation (NVGRE)](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)します。 NDIS ミニポート、プロトコル、およびフィルター ドライバーおよび大きなを実行するための Nic は、NVGRE をサポートするための方法で実行する必要がありますオフロード (LSO) バージョン 2 (LSOV2) を送信します。

**注**  このページは、内の情報に精通していることを前提としています。 [、セグメント化の大きな TCP パケットのオフロード](offloading-the-segmentation-of-large-tcp-packets.md)します。

 

場合[ **NDIS\_TCP\_送信\_オフロード\_補助的な\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/jj991957).**IsEncapsulatedPacket**は**TRUE**と**TcpIpChecksumNetBufferListInfo**アウト オブ バンド (OOB) の情報が有効でこれを示すその NVGREサポートが必要ですし、NIC は、次の条件と、NVGRE でフォーマットされたパケットの LSOV2 オフロードを実行する必要があります。

-   値のみ、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567882).**LsoV2Transmit**構造が無効です。 NIC とミニポート ドライバーが必要があります内の値を参照していません、 **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**.**LsoV1Transmit**構造体。
-   [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567882).**LsoV2Transmit**.**TcpHeaderOffset**メンバーに適切なオフセット値がないと、NIC またはミニポート ドライバーでは使用しないでください。

LSOV2 で NVGRE をサポートするには、プロトコルとフィルター ドライバーは、次の変更を加える必要があります。

-   削減、 **MSS**値、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567882).**LsoV2Transmit**新しい GRE ヘッダーに対応する構造体。
-   送信 TCP ペイロードの長さの短縮ができない可能性があるダウン**MSS**値。
-   調整、 **InnerFrameOffset**、 **TransportIpHeaderRelativeOffset**、および**TcpHeaderRelativeOffset**値、 [ **NDIS\_TCP\_送信\_オフロード\_補助的な\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/jj991957) GRE に対応する構造体ヘッダー。

Nic とミニポート ドライバーを使用して、可能性があります、 **InnerFrameOffset**、 **TransportIpHeaderRelativeOffset**、および**TcpHeaderRelativeOffset** で提供される値[ **NDIS\_TCP\_送信\_オフロード\_補助的な\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/jj991957)構造体。 NIC またはミニポート ドライバーでは、トンネル (外部) の IP ヘッダーまたはこれらのオフセットを検証する後続のヘッダーで、必要なヘッダーのチェックを実行できます。

ミニポート ドライバーは、ケースを処理する必要があります、 [ **NDIS\_TCP\_送信\_オフロード\_補助的な\_NET\_バッファー\_ボックスの一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/jj991957).**InnerFrameOffset**パケットの先頭よりも、別のスキャッター/ギャザー リストがあります。 すべてのカプセル化の先頭に追加されたヘッダー (ETH、IP、GRE) が物理的に連続できるようになり、パケットの最初の MDL になります、プロトコルのドライバーが保証されます。

プロトコルとフィルター ドライバーは、TCP ペイロード長さの合計が、制限の倍数であることを確認しない**MSS**値。 このため、ミニポート ドライバーと Nic は、トンネル (外部) の IP ヘッダーを更新する必要があります。 Nic がに基づいて、削減できるだけ多くのフル サイズのセグメントを生成する必要が**MSS**値、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567882).**LsoV2Transmit** OOB 情報。 1 つだけ sub -**MSS**セグメントを生成することが LSOv2 送信ごと。

ミニポート ドライバーでは、次の操作を行う必要があります。

-   トンネル (外部) の IP ヘッダーのチェックサムを計算します。
-   IP id (IP ID) がすべてのパケットのトンネル (外側) IP ヘッダーの値をインクリメントします。 最初のパケットは、元のトンネル (外側) IP ヘッダーで IP ID を使用する必要があります。
-   すべてのパケットのトランスポート (内部) の IP ヘッダーの IP の ID をインクリメントします。 最初のパケットは、元のトランスポート (内部) IP ヘッダーで IP ID を使用する必要があります。
-   TCP ヘッダーとトランスポート (内部) の IP ヘッダーのチェックサムを計算します。
-   生成されたすべてのパケットをカプセル化トンネル (外側) ヘッダーを含む、完全なヘッダーが追加されたことを確認します。

## <a name="related-topics"></a>関連トピック


[大きな TCP パケットのセグメント化をオフロード](offloading-the-segmentation-of-large-tcp-packets.md)

 

 






