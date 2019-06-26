---
title: Windows Vista SP1 と Windows Server 2008 での WFP の変更
description: Windows Vista SP1 と Windows Server 2008 での WFP の変更
ms.assetid: c901dbed-639d-473b-aaf0-8470e9c04009
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c032d9458e1998905a38c9856fa515456c335af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357009"
---
# <a name="wfp-changes-for-windows-vista-sp1-and-windows-server-2008"></a>Windows Vista SP1 と Windows Server 2008 での WFP の変更


使用可能な関数と、Windows フィルタ リング プラットフォームを開始するには、Windows Vista Service Pack 1 (SP1)、Windows Server 2008 の動作では、いくつかの変更が加えられました。 多くの場合、新しい機能を利用する必要がありますのコンパイル時またはを持つ、NTDDI コールアウト ドライバーを再コンパイル\_バージョン マクロ設定 NTDDI\_WIN6SP1 します。

-   新しい関数:[**FwpsConstructIpHeaderForTransportPacket0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsconstructipheaderfortransportpacket0)
    [**FwpsReassembleForwardFragmentGroup0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsreassembleforwardfragmentgroup0)
-   新しい FWPS\_ストリーム\_フラグ\_受信\_に記載されているプッシュ フラグ オプション[ **FwpsStreamInjectAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)

-   更新に記載のフィルタ リング条件の名前を変更[で各層をフィルター処理に使用できる条件をフィルター処理](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-conditions-available-at-each-filtering-layer)

-   更新し、FWPS に追加されたデータ フィールドの識別子の名前を変更\_レイヤー\_ALE\_AUTH\_RECV\_ACCEPT\_*XXX*と FWPS\_レイヤー\_受信\_ICMP\_エラー\_*XXX*記載レイヤー[データ フィールドの識別子](https://docs.microsoft.com/windows-hardware/drivers/network/data-field-identifiers)と共に動作変更

-   追加のメタデータ フィールドの識別子、記載[メタデータ フィールド](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields)と[各層をフィルター処理でのメタデータ フィールド](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields-at-each-filtering-layer)

-   新しいドキュメントの次のトピックを示します。
    -   [IPsec と互換性のあるコールアウト ドライバーの開発](developing-ipsec-compatible-callout-drivers.md)
    -   [処理がコールアウトを非同期的に分類します。](processing-classify-callouts-asynchronously.md)
-   次のトピックには、追加の更新プログラムが含まれます。[処理通知コールアウト](processing-notify-callouts.md)
    [Stream 検査](stream-inspection.md)
    [**FwpsFlowAssociateContext0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsflowassociatecontext0) 
     [**FwpsFlowRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsflowremovecontext0)
    [*classifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) 
     [ *notifyFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)
    [**FWPS\_CALLOUT0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_callout0_)
    [**FWPS\_受信\_メタデータ\_VALUES0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)

 

 





