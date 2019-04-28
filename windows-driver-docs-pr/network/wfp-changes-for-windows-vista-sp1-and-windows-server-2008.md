---
title: Windows Vista SP1 と Windows Server 2008 での WFP の変更
description: Windows Vista SP1 と Windows Server 2008 での WFP の変更
ms.assetid: c901dbed-639d-473b-aaf0-8470e9c04009
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 209bab48526a194e9c2a57143a461939bb83b6ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365703"
---
# <a name="wfp-changes-for-windows-vista-sp1-and-windows-server-2008"></a>Windows Vista SP1 と Windows Server 2008 での WFP の変更


使用可能な関数と、Windows フィルタ リング プラットフォームを開始するには、Windows Vista Service Pack 1 (SP1)、Windows Server 2008 の動作では、いくつかの変更が加えられました。 多くの場合、新しい機能を利用する必要がありますのコンパイル時またはを持つ、NTDDI コールアウト ドライバーを再コンパイル\_バージョン マクロ設定 NTDDI\_WIN6SP1 します。

-   新しい関数:[**FwpsConstructIpHeaderForTransportPacket0**](https://msdn.microsoft.com/library/windows/hardware/ff551154)
    [**FwpsReassembleForwardFragmentGroup0**](https://msdn.microsoft.com/library/windows/hardware/ff551205)
-   新しい FWPS\_ストリーム\_フラグ\_受信\_に記載されているプッシュ フラグ オプション[ **FwpsStreamInjectAsync0**](https://msdn.microsoft.com/library/windows/hardware/ff551213)

-   更新に記載のフィルタ リング条件の名前を変更[で各層をフィルター処理に使用できる条件をフィルター処理](https://msdn.microsoft.com/library/windows/hardware/ff549939)

-   更新し、FWPS に追加されたデータ フィールドの識別子の名前を変更\_レイヤー\_ALE\_AUTH\_RECV\_ACCEPT\_*XXX*と FWPS\_レイヤー\_受信\_ICMP\_エラー\_*XXX*記載レイヤー[データ フィールドの識別子](https://msdn.microsoft.com/library/windows/hardware/ff546312)と共に動作変更

-   追加のメタデータ フィールドの識別子、記載[メタデータ フィールド](https://msdn.microsoft.com/library/windows/hardware/ff559174)と[各層をフィルター処理でのメタデータ フィールド](https://msdn.microsoft.com/library/windows/hardware/ff559179)

-   新しいドキュメントの次のトピックを示します。
    -   [IPsec と互換性のあるコールアウト ドライバーの開発](developing-ipsec-compatible-callout-drivers.md)
    -   [処理がコールアウトを非同期的に分類します。](processing-classify-callouts-asynchronously.md)
-   次のトピックには、追加の更新プログラムが含まれます。[処理通知コールアウト](processing-notify-callouts.md)
    [Stream 検査](stream-inspection.md)
    [**FwpsFlowAssociateContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551165) 
     [**FwpsFlowRemoveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551169)
    [*classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890) 
     [ *notifyFn*](https://msdn.microsoft.com/library/windows/hardware/ff568803)
    [**FWPS\_CALLOUT0**](https://msdn.microsoft.com/library/windows/hardware/ff551224)
    [**FWPS\_受信\_メタデータ\_VALUES0**](https://msdn.microsoft.com/library/windows/hardware/ff552397)

 

 





