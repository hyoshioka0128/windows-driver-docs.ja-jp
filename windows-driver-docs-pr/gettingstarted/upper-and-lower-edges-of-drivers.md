---
title: ドライバーの上端と下端
description: I/O 要求に関与するドライバーのシーケンスは、要求のドライバー スタックと呼ばれます。
ms.assetid: EA1C36F4-B9BD-4A9E-A6D4-6B4EC5455030
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ea0ac828ce26598c847b125aa1686145415a188
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518593"
---
# <a name="upper-and-lower-edges-of-drivers"></a>ドライバーの上端と下端


I/O 要求に関与するドライバーのシーケンスは、要求のドライバー スタックと呼ばれます。 ドライバーは、スタックの下位ドライバーの上端を呼び出すことができます。 ドライバーは、スタックの上位ドライバーの下端も呼び出すことができます。

このトピックを読む前にまず、「[デバイス ノードとデバイス スタック](device-nodes-and-device-stacks.md)」と「[ドライバー スタック](driver-stacks.md)」で説明する概念について理解しておく必要があります。

I/O 要求は、まずドライバー スタックの一番上のドライバーにより処理された後、次にその下のドライバーというように、要求が完全に処理されるまで順番に処理されます。

上位ドライバーが呼び出すことができる一連の関数がドライバーに実装された場合、その一連の関数はドライバーの*上端*またはドライバーの*上端インターフェイス*と呼ばれます。

下位ドライバーが呼び出すことができる一連の関数がドライバーに実装された場合、その一連の関数はドライバーの*下端*またはドライバーの*下端インターフェイス*と呼ばれます。

### <a name="span-idaudioexamplespanspan-idaudioexamplespanspan-idaudioexamplespanaudio-example"></a><span id="Audio_example"></span><span id="audio_example"></span><span id="AUDIO_EXAMPLE"></span>オーディオの例

ドライバー スタックにおいて、オーディオ ポート ドライバーの下にあるオーディオ ミニポート ドライバーについて考えます。 ポート ドライバーは、ミニポート ドライバーの上端を呼び出します。 ミニポート ドライバーは、ポート ドライバーの下端を呼び出します。

![ミニポート ドライバーの上にあるオーディオ ポート ドライバーの図](images/audiodrvstack.png)

上の図は、ドライバー スタックにおいて、ミニポート ドライバーの上にポート ドライバーがあることを考えると役に立つ場合があることを示しています。 I/O 要求は、ポート ドライバー、ミニポート ドライバーの順に処理されるため、ポート ドライバーがミニポート ドライバーの上にあると考えるのが適切です。 ただし、次の図に示すように、(ミニポート、ポート) ドライバー ペアは通常デバイス スタックの単一のレベルに存在することを念頭に置いてください。

![(ミニポート/ポート) ペアがあるデバイス スタックの図](images/upperloweredge01.png)

*デバイス スタック*は、*ドライバー スタック*と同じものではない点に注意してください。 これらの用語の定義と、デバイス スタックの 1 つのレベルに存在する単一の WDM ドライバーがドライバーのペアによってどのように形成されるかの説明については、「[ミニドライバーとドライバーのペア](minidrivers-and-driver-pairs.md)」をご覧ください。

同じデバイス ノードとデバイス スタックを別の方法で表した図を次に示します。

![ミニポートの上にポート ドライバーがあるデバイス スタックの図](images/upperloweredge02.png)

上の図では、(ミニポート、ポート) ペアによって、デバイス スタック内の単一のデバイス オブジェクト (FDO) に関連付けられた単一の WDM ドライバーが形成されているのがわかります。つまり、(ミニポート、ポート) ペアがデバイス スタック内の 1 つのレベルにのみ存在しています。 しかし、ミニポート ドライバーとポート ドライバーの縦の関係もわかります。 ポート ドライバーが最初に I/O 要求を処理した後、ミニポート ドライバーを呼び出して追加の処理を行うことを示すため、ポート ドライバーはミニポート ドライバーの上に表示されています。

重要なポイントは、ポート ドライバーがミニポート ドライバーの上端インターフェイスを呼び出すということは、I/O 要求をデバイス スタックの下方に渡すことと同じではないという点です。 ドライバー スタック (デバイス スタックではなく) では、ポート ドライバーをミニポート ドライバーの上に配置することを選ぶことができますが、これはデバイス スタックにおいてポート ドライバーがミニポート ドライバーの上にあることを意味するわけではありません。

### <a name="span-idndisexamplespanspan-idndisexamplespanspan-idndisexamplespanndis-example"></a><span id="NDIS_example"></span><span id="ndis_example"></span><span id="NDIS_EXAMPLE"></span>NDIS の例

場合によっては、ドライバーが下位ドライバーの上端を間接的に呼び出すことがあります。 たとえば、ドライバー スタックにおいて、[TCP/IP プロトコル ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff556929)が [NDIS](https://msdn.microsoft.com/library/windows/hardware/ff565448) ミニポート ドライバーの上にある場合について考えてみます。 ミニポート ドライバーは、ミニポート ドライバーの上端を形成する一連の *MiniportXxx* 関数を実装しています。 TCP/IP プロトコル ドライバーが、NDIS ミニポート ドライバーの上端に*バインド*しているとします。 しかし、TCP/IP ドライバーは *MiniportXxx* 関数を直接呼び出すわけではありません。 代わりに、NDIS ライブラリ内の関数を呼び出し、それらの関数が *MiniportXxx* 関数を呼び出します。

![TCP/IP と NDIS ミニポート スタックの図](images/upperloweredge03.png)

上の図は、ドライバー スタックを示しています。 同じドライバーの別のビューを次に示します。

![ネットワーク カードのデバイス スタックの図](images/upperloweredge04.png)

上の図は、ネットワーク インターフェイス カード (NIC) のデバイス ノードを示します。 デバイス ノードは、プラグ アンド プレイ (PnP) デバイス ツリーに存在します。 NIC のデバイス ノードには、3 つのデバイス オブジェクトを持つデバイス スタックがあります。 NDIS ミニポート ドライバーと NDIS ライブラリはペアとして機能する点に注目してください。 このペア (MyMiniport.sys、Ndis.sys) は、ファンクショナル デバイス オブジェクト (FDO) により表される単一の WDM ドライバーを形成します。

また、プロトコル ドライバー Tcpip.sys は NIC のデバイス スタックの一部ではない点にも注目してください。 実際に、Tcpip.sys は PnP デバイス ツリーのどの部分でもありません。

## <a name="span-idsummaryspanspan-idsummaryspanspan-idsummaryspansummary"></a><span id="Summary"></span><span id="summary"></span><span id="SUMMARY"></span>まとめ


*上端*および*下端*という用語は、スタック内のドライバーが互いにやり取りするために使うインターフェイスを表すために使われています。 [  *ドライバー スタック*](driver-stacks.md)は、[*デバイス スタック*](device-nodes-and-device-stacks.md)と同じものではありません。 ドライバー スタックで縦に並んでいる 2 つのドライバーは、デバイス スタックの単一のレベルに存在するドライバー ペアを形成することがあります。 ドライバーによっては、PnP デバイス ツリーの一部ではない場合があります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[すべてのドライバー開発者のための概念](concepts-and-knowledge-for-all-driver-developers.md)

[デバイス ノードとデバイス スタック](device-nodes-and-device-stacks.md)

[ドライバー スタック](driver-stacks.md)

[オーディオ デバイス](https://msdn.microsoft.com/library/windows/hardware/ff537760)

[Windows Vista 以降のネットワーク ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff570021)

 

 






