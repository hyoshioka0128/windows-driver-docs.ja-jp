---
title: Windows Vista SP1 と Windows Server 2008 での WFP の変更
description: Windows Vista SP1 と Windows Server 2008 での WFP の変更
ms.assetid: c901dbed-639d-473b-aaf0-8470e9c04009
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c91c52c7d9b8acf0cf695be38e811e25d96c1ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841700"
---
# <a name="wfp-changes-for-windows-vista-sp1-and-windows-server-2008"></a>Windows Vista SP1 と Windows Server 2008 での WFP の変更


Windows Vista Service Pack 1 (SP1) および Windows Server 2008 以降では、Windows フィルタリングプラットフォームの使用可能な機能と動作にいくつかの変更が加えられています。 多くの場合、新しい機能を利用するには、NTDDI\_VERSION マクロが NTDDI\_WIN6SP1 に設定されているコールアウトドライバーをコンパイルまたは再コンパイルする必要があります。

-   新しい関数: [**FwpsConstructIpHeaderForTransportPacket0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsconstructipheaderfortransportpacket0)
    [**FwpsReassembleForwardFragmentGroup0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreassembleforwardfragmentgroup0)
-   FwpsStreamInjectAsync0 に記述されている新しい FWPS\_STREAM\_FLAG\_RECEIVE\_PUSH フラグオプション[](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)

-   フィルター条件の更新および名前変更 ([各フィルター処理レイヤーで使用可能なフィルター](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-conditions-available-at-each-filtering-layer)条件に記載されています)

-   FWPS\_レイヤーに追加されたデータフィールド識別子を更新および名前変更しました。\_ALE\_AUTH\_RECV\_ACCEPT\_*XXX*および fwps\_LAYER\_受信\_ICMP\_エラー\_*XXX*層 ([データフィールド識別子](https://docs.microsoft.com/windows-hardware/drivers/network/data-field-identifiers)に一覧表示) と動作の変更

-   各フィルターレイヤーの[メタ](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields)データフィールドおよび[メタデータフィールド](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields-at-each-filtering-layer)に表示される追加のメタデータフィールド識別子

-   次のドキュメントのトピックが新しく追加されています。
    -   [IPsec と互換性のあるコールアウトドライバーの開発](developing-ipsec-compatible-callout-drivers.md)
    -   [コールアウトを非同期に分類する処理](processing-classify-callouts-asynchronously.md)
-   次のトピックには、追加の更新プログラムが含まれています。[処理の通知吹き出し](processing-notify-callouts.md)
    [ストリーム検査](stream-inspection.md)
    [**FwpsFlowAssociateContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowassociatecontext0)
    [**FwpsFlowRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowremovecontext0)
    [*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)
    [*Notifyfn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)
    [**FWPS\_CALLOUT0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout0_)
    [**FWPS\_受信\_メタデータ\_VALUES0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)

 

 





