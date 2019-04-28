---
title: パケット トラフィックの生成
description: パケット トラフィックの生成
ms.assetid: 613C7E82-387D-47AE-A699-A799087D3C1D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ed5afb14e21e4d99530bc5496e6980ed4924eb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378244"
---
# <a name="originating-packet-traffic"></a>パケット トラフィックの生成


このトピックでは、HYPER-V の拡張機能が新しいパケットの発信元し、拡張可能スイッチのデータ パスに挿入する方法について説明します。

**注**  このページは、情報とでのダイアグラムに精通していることを前提としています。 [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)します。

 

**注**  、拡張可能スイッチのインターフェイスで NDIS フィルター ドライバーと呼ばれる*拡張可能スイッチの拡張機能*と呼ばれるドライバー スタック、*拡張可能スイッチ ドライバー スタック*. 拡張機能に関する詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ拡張機能](hyper-v-extensible-switch-extensions.md)します。

 

拡張可能スイッチの拡張機能は、拡張可能スイッチのイングレス データ パスに新しいパケットをのみ挿入できます。 これにより、拡張可能スイッチのインターフェイスがフィルター処理してこれらのパケットを正しく転送できます。 拡張機能は、受信データのパスに新しいパケットを挿入する次のガイドラインに従う必要があります。

-   拡張機能に割り当てる必要があります最初、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568389)新しいパケットの構造体。

-   拡張機能の割り当て後に、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568389)構造新しいパケットの場合は、呼び出す必要があります、 [ *AllocateNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598134)ハンドラー関数にパケットを転送の拡張可能スイッチのコンテキストを割り当てられません。

    転送コンテキストは、パケットの帯域外の (OOB) データに存在します。 その発信元ポートと 1 つまたは複数の宛先ポートの配列など、パケットの転送情報が含まれています。

    転送コンテキストに関する詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)します。

-   拡張機能の呼び出し後[ *AllocateNetBufferListForwardingContext*](https://msdn.microsoft.com/library/windows/hardware/hh598134)、パケットの発信元ポートに設定する**NDIS\_スイッチ\_既定\_ポート\_ID**します。 パケットの送信元ポートの識別子を**NDIS\_切り替える\_既定\_ポート\_ID**が信頼されており、アクセス制御リスト (Acl など、拡張可能スイッチ ポートのポリシーをバイパスします。) とサービスの品質 (QoS)。

    拡張機能は、特定のポートから送信されたかのように扱う場合にパケットを必要があります。 これにより、パケットに適用するには、そのポートのポリシーができます。 拡張機能の呼び出し[ *SetNetBufferListSource* ](https://msdn.microsoft.com/library/windows/hardware/hh598300)パケットの発信元ポートを変更します。

    ただし、ある可能性があります、拡張機能にパケットの送信元ポートの識別子を割り当てる必要のある状況**NDIS\_スイッチ\_既定\_ポート\_ID**します。 など、拡張機能に設定するソース ポート識別子**NDIS\_スイッチ\_既定\_ポート\_ID**でデバイスに送信されるパケットの独自のコントロール、外部ネットワークです。

-   転送拡張機能がイングレス データ パスが新しいパケットを送信する場合、パケットの宛先ポートそれを判断する必要があります。 この手順の詳細については、次を参照してください。[を追加する拡張可能なスイッチ宛先ポート データ パケットに](adding-extensible-switch-destination-port-data-to-a-packet.md)します。

    **注**  キャプチャまたは拡張機能をフィルター処理は、新しいパケットを新しい変換先のポートを追加できません。

     

-   パケット データがローカルである、拡張機能は、新しいパケットを作成するときまたは*信頼*HYPER-V 親パーティションの親のオペレーティング システムのメモリ。 このメモリは、子パーティションでアクセスできません。 そのためと見なされます「安全」同期されていない更新プログラムからによってそのパーティションで実行されるゲスト オペレーティング システム。

    拡張機能を取得する必要があります、 [ **NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)を使用して、新しいパケットの共用体、 [ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://msdn.microsoft.com/library/windows/hardware/hh598259)マクロ。 拡張機能を設定する必要があります、 **IsPacketDataSafe**メンバーを TRUE にします。 これは、信頼されているメモリ内のすべてのパケット データがあることを指定します。

-   拡張機能を呼び出すと[ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)イングレス データ パスにパケットを挿入することを設定する必要があります、*フラグ*拡張可能な適切なパラメーターフラグの設定を切り替えます。 これらの詳細については、フラグの設定を参照してください[HYPER-V 拡張可能スイッチの送信と受信フラグ](hyper-v-extensible-switch-send-and-receive-flags.md)します。

-   NDIS が、拡張機能を呼び出すときに[ *FilterSendNetBufferListsComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549967)新しいパケットの送信要求を完了する関数を拡張機能を呼び出す必要があります[ *FreeNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598153)を割り当てられた転送のコンテキストを解放します。 拡張機能を解放または再利用する前にこれにする必要があります、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568389)パケットの構造体。

拡張可能スイッチのイングレスおよびエグレス データ パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ データ パス](hyper-v-extensible-switch-data-path.md)します。

 

 





