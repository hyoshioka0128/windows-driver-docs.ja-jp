---
title: 拡張可能スイッチ宛先ポートへのパケット配信の除外
description: 拡張可能スイッチ宛先ポートへのパケット配信の除外
ms.assetid: 04BF02A6-360F-482E-A86B-31232AFCB778
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4251c44daa9e71f74721830a8cd0b82b4dfff70c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391663"
---
# <a name="excluding-packet-delivery-to-extensible-switch-destination-ports"></a>拡張可能スイッチ宛先ポートへのパケット配信の除外


このトピックでは、HYPER-V 拡張可能スイッチの拡張機能が拡張可能スイッチのポートへのパケットの配信を除外する方法について説明します。 パケットの宛先ポートの帯域外 (OOB) 転送パケットの内のコンテキスト内で指定された[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 このコンテキストの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)します。

**注**このページは、情報とでのダイアグラムに精通していることを前提としています。 [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)します。


**注**、拡張可能スイッチのインターフェイスで NDIS フィルター ドライバーと呼ばれる*拡張可能スイッチの拡張機能*と呼ばれるドライバー スタック、*ドライバー スタックの拡張可能スイッチ*します。 拡張機能に関する詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ拡張機能](hyper-v-extensible-switch-extensions.md)します。

フィルター処理および転送拡張機能は、拡張可能スイッチのイングレスまたはエグレス データ パスで取得したパケットの配信を除外できます。 パケット配信の除外は、次の方法で実行できます。

-   拡張機能は、要求パケットかを示す値を実行して、パケットを削除できます。 これには、任意の拡張可能スイッチ ポートのパケットの配信が含まれません。 このメソッドは、1 つまたは複数の宛先ポートのパケットで使用できます。

    拡張可能スイッチのイングレス データ パス取得したパケットの場合、拡張機能は呼び出すことにより、パケットの送信要求を完了[ **NdisFSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562618)します。

    拡張機能を拡張可能スイッチのエグレス データ パス取得したパケットの場合は、パケットが完了すると通知を呼び出すことによって[ **NdisFReturnNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562613)します。

-   複数の宛先ポートを持つエグレス データ パス取得したパケットの場合、拡張機能は、宛先ポートを 1 つまたは複数のデータを変更することでパケット配信を除外できます。 拡張機能は設定によって、 **IsExcluded**の宛先ポートのメンバー [ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)いずれかの値構造体。 この方法により、これらのポートに配信元へのパケット**IsExcluded**値が 0 に設定されます。

    **注**イングレス データ パス取得したパケットには宛先ポートが含まれていません。 このデータは拡張可能スイッチが出口のデータ パスのパケットを転送した後にのみ使用できます。

拡張機能は、宛先ポートの変更後**IsExcluded**値、拡張機能に関連するエグレス データ パスにパケットを転送にする必要があります。 ただし場合、 **IsExcluded**パケットの宛先ポートのデータがドロップ パケットを実行して、パケットを転送するのではなくを示す値を受け取る 1、拡張機能に設定します。

**注**拡張機能は、宛先ポートの設定が後**IsExcluded**エグレス データ パス上の拡張機能に関連する 1 つは、値は 0 にこの値を変更することはできません。

**注**取得拡張機能で拡張可能スイッチ ポートにパケットを配信を除外できません。

フィルター処理および転送拡張機能は、拡張可能スイッチ ポートにパケット配信を除外するための次のガイドラインに従う必要があります。

-   拡張可能スイッチのイングレス データ パス フィルター処理および転送拡張機能は、パケットの発信元ポート、またはデータのポリシーの条件に基づいてパケット配信を除外できます。

    ソース ポートの情報が格納されている、 [ **NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)共用体のパケットの OOB データの[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 拡張機能を使用してデータを取得する、 [ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://msdn.microsoft.com/library/windows/hardware/hh598259)マクロ。

    場合は、拡張機能は、イングレス データのパスから取得したパケットの配信を除く、パケットの送信要求を完了してパケットを削除にする必要があります。

-   拡張可能スイッチのイングレス データ パスは、転送拡張機能は、パケットの宛先ポートを特定し、パケットの OOB データにこの情報を追加します。 拡張機能によって適用されるポリシーの条件に基づき、OOB データにその先のポート情報を追加しないポートへのパケット配信を除外できます。

    この手順の詳細については、次を参照してください。[を追加する拡張可能なスイッチ宛先ポート データ パケットに](adding-extensible-switch-destination-port-data-to-a-packet.md)します。

-   拡張可能スイッチのエグレス データ パス フィルター処理および転送拡張機能は、ポリシーの条件に基づいて、パケットの配信を除外できます。 たとえば、フィルター拡張機能は、パケットの発信元ポートまたは変換先のポートのポリシーの条件に基づいてパケット配信を除外できます。

    拡張機能は、次の手順に従って、パケットの宛先ポートへの配信を除外します。

    1.  拡張機能は呼び出すことによって、パケットの宛先ポートを取得[ *GetNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598157)します。 呼び出し、返される NDIS 場合\_状態\_成功した場合、*変換先*パラメーターにはへのポインターが含まれています、 [ **NDIS\_スイッチ\_転送\_移行先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造体。 この構造体には、パケットの拡張可能スイッチの宛先ポートを指定します。 各接続先ポートとして書式設定、 [ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)構造体。

        **注**場合、 **NumDestinations**のメンバー、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造には、ゼロの値が含まれる、パケットには、宛先ポートのデータがありません。

2.  拡張機能を設定して、拡張可能スイッチ ポートにパケット配信の除外、 **IsExcluded**の宛先ポートのメンバー [ **NDIS\_切り替える\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)いずれかの値構造体。

    **注**場合は、拡張機能を除外するすべての宛先ポートのパケットの配信、拡張機能によってパケットが破棄する必要があります、パケットの受信を示す値を完了しています。

3.  拡張機能には、パケットの 1 つまたはすべての宛先ポートへの配信が除外されて、いる場合は、以下を行うこと必要があります。

    -   拡張機能を呼び出す必要があります[ *UpdateNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598303)パケットの OOB データにこれらの変更をコミットします。

    -   拡張機能を呼び出す必要があります[ *ReportFilteredNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/hh598297)します。 この関数が呼び出されると、拡張可能スイッチのインターフェイスはカウンターをインクリメントし、パケットの除外されたイベント ログに記録します。 拡張機能は、パケットを取得して、拡張可能スイッチのデータ パスでパケットを転送する前に、この呼び出しを行う必要があります。

    同様に、拡張機能では、パケットのすべてのポートへの配信を除外するパケットの送信要求かを示す値が完了するも呼び出す必要があります[ *ReportFilteredNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/hh598297)します。

    **注**、拡張機能のリンク リストを作成できます[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)拡張機能を除外するパケットの構造体。 拡張機能を呼び出すと[ *ReportFilteredNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/hh598297)、設定、 *NetBufferLists*リンク リストへのポインターへのパラメーター。

拡張可能スイッチのイングレスおよびエグレス データ パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ データ パス](hyper-v-extensible-switch-data-path.md)します。