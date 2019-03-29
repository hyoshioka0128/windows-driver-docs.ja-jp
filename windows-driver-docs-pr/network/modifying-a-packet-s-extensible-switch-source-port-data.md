---
title: パケットの拡張可能スイッチの発信元ポート データの変更
description: パケットの拡張可能スイッチの発信元ポート データの変更
ms.assetid: 44338441-160C-4CD1-8C0B-27CFBE136910
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47a352c08500542cb8e00e62ea7d79d692ce7c04
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579638"
---
# <a name="modifying-a-packets-extensible-switch-source-port-data"></a>パケットの拡張可能スイッチの発信元ポート データの変更


HYPER-V 拡張可能スイッチの発信元ポートが指定された、 **SourcePortId**内のメンバー、 [ **NDIS\_切り替える\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)構造体。 この構造体の帯域外 (OOB) コンテキストのパケットの転送に含まれている[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 このコンテキストの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)します。

拡張可能スイッチ拡張機能は、パケットの送信元ポートの識別子を変更するための次のガイドラインに従う必要があります。

-   拡張可能スイッチ拡張機能を呼び出す必要があります[ *SetNetBufferListSource* ](https://msdn.microsoft.com/library/windows/hardware/hh598300)パケットの発信元ポートを変更します。 拡張機能が直接変更する必要があります、 **SourcePortId**のメンバー、 [ **NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)構造体。

-   呼び出す必要がありますが、拡張機能を作成または、パケットを複製する場合、 [ *AllocateNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598134)関数の呼び出し後[ **NdisAllocateNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561609). この関数は、OOB データ パケットの情報を転送するために使用されるコンテキスト スイッチの拡張可能な領域を割り当てます。

    拡張機能を呼び出すと[ *AllocateNetBufferListForwardingContext*](https://msdn.microsoft.com/library/windows/hardware/hh598134)、 **SourcePortId**に設定されているメンバー **NDIS\_スイッチ\_既定の\_ポート\_ID**します。 これは、パケットが、拡張可能スイッチ ポートに到着するのではなく、拡張機能から発信されたことを指定します。

    パケットの発信元ポートと**NDIS\_切り替える\_既定\_ポート\_ID**は拡張可能スイッチ拡張機能のデータ パス特権によって扱われ、信頼されています。 このようなトラフィックは、その他の発信元ポートからのパケットに適用されるポリシーに従う必要はありません。 たとえば、パケットの送信元ポート識別子を**NDIS\_切り替える\_既定\_ポート\_ID**基になるで適用される拡張可能スイッチの組み込みポリシーをバイパス拡張可能スイッチのミニポート エッジです。 これらのポリシーは、アクセス制御リスト (Acl) とサービスの品質 (QoS)。

    発信元ポートを使用すると、拡張機能には、トラフィックのパケットが発信、 **NDIS\_スイッチ\_既定\_ポート\_ID**注意して慎重にします。 ほとんどの場合、拡張機能は拡張可能スイッチのアクティブなポートに送信元ポートの識別子を変更する必要があります。 これにより、パケットに適用するには、そのポートのポリシーができます。

    ただし、場合があります、拡張機能が、発信元ポートを使用して、 **NDIS\_スイッチ\_既定\_ポート\_ID**パケットの発生元します。 たとえば、拡張機能を使用する、物理または仮想ネットワーク上の宛先に送信する必要のあるコントロールのパケットの発生元**NDIS\_スイッチ\_既定\_ポート\_ID**ソース ポートの識別子。 こうこと、パケットはいないフィルター処理され、拡張可能スイッチ ドライバー スタック内の基になる拡張機能によって拒否されます。

 

 





