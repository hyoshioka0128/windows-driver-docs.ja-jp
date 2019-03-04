---
title: ドライバー スタック
description: デバイス ドライバーに送信される要求のほとんどは、I/O 要求パケット (IRP) にパッケージ化されます。
ms.assetid: 8D55CB83-C50A-48B8-9379-ECF2CF30AEE5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41d50497c8343d8ae5f7a54b77d97a86f06f0d2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518786"
---
# <a name="driver-stacks"></a>ドライバー スタック


デバイス ドライバーに送信される要求のほとんどは、[I/O 要求パケット](i-o-request-packets.md) (IRP) にパッケージ化されます。 個々のデバイスは、1 つのデバイス ノードで表され、各デバイス ノードには 1 つのデバイス スタックが含まれます。 詳しくは、「[デバイス ノードとデバイス スタック](device-nodes-and-device-stacks.md)」をご覧ください。 デバイスに対して読み取り、書き込み、または制御の要求を送るために、I/O マネージャーは、デバイスのデバイス ノードを探し、そのノードのデバイス スタックに IRP を送信します。 I/O 要求の処理に複数のデバイス スタックが関与する場合があります。 関与するデバイス スタックの数に関係なく、ある I/O 要求に関与するドライバー全体のシーケンスのことを、要求に対する*ドライバー スタック*と呼びます。 また、特定のテクノロジに対応してレイヤー化された一連のドライバーの表すときに、*ドライバー スタック*という用語を使うこともあります。

## <a name="span-idiorequeststhatareprocessedbyseveraldevicestacksspanspan-idiorequeststhatareprocessedbyseveraldevicestacksspanspan-idiorequeststhatareprocessedbyseveraldevicestacksspanio-requests-that-are-processed-by-several-device-stacks"></a><span id="I_O_requests_that_are_processed_by_several_device_stacks"></span><span id="i_o_requests_that_are_processed_by_several_device_stacks"></span><span id="I_O_REQUESTS_THAT_ARE_PROCESSED_BY_SEVERAL_DEVICE_STACKS"></span>複数のデバイス スタックで処理される I/O 要求


場合によっては、IRP の処理に複数のデバイス スタックが関与することがあります。 次の図は、1 つの IRP を処理するときに 4 つのデバイス スタックが関与する例を示しています。

![それぞれのノードにデバイス スタックを 1 つ含む 4 つのデバイス ノードの図](images/chain01.png)

以下では、図の中の番号が付いた各段階で、IRP がどのように処理されるかについて説明します。

1.  IRP は、My USB Storage Device ノードのデバイス スタックにあるファンクション ドライバーである Disk.sys によって作られます。 Disk.sys により、IRP が下のデバイス スタックである Usbstor.sys に渡されます。

2.  Usbstor.sys は My USB Storage Device ノードの PDO ドライバーと USB Mass Storage Device ノードの FDO ドライバーになっています。 この段階で、IRP が (PDO、Usbstor.sys) のペア、または (FDO、Usbstor.sys) のペアのいずれによって所有されているかを特定することはそれほど重要ではありません。 IRP は、Usbstor.sys ドライバーによって所有され、このドライバーは PDO と FDO の両方にアクセスします。
3.  Usbstor.sys が IRP の処理を終了すると、IRP は Usbhub.sys に渡されます。 Usbhub.sys は、USB Mass Storage Device ノードの PDO ドライバーと USB Root Hub ノードの FDO ドライバーになっています。 この段階で、IRP が (PDO、Usbhub.sys) のペア、または (FDO、Usbhub.sys) のペアのいずれによって所有されているかを特定することはそれほど重要ではありません。 IRP は、Usbhub.sys ドライバーによって所有され、このドライバーは PDO と FDO の両方にアクセスします。

4.  Usbhub.sys が IRP の処理を終了すると、IRP は (Usbuhci.sys、Usbport.sys) のペアに渡されます。

    Usbuhci.sys はミニポート ドライバー、Usbport.sys はポート ドライバーです。 (ミニポート、ポート) のペアは、1 つのドライバーの役割を果たします。 この場合は、ミニポート ドライバーとポート ドライバーの両方が Microsoft によって作られています。 (Usbuhci.sys、Usbport.sys) のペアは USB Root Hub ノードの PDO ドライバーであり、同時に (Usbuhci.sys、Usbport.sys) のペアは USB Host Controller ノードの FDO ドライバーでもあります。 (Usbuhci.sys、Usbport.sys) のペアは実際に、ホスト コントローラー ハードウェアと通信し、これを受けてホスト コントローラー ハードウェアは、物理的な USB ストレージ装置と通信します。

## <a name="span-idthedriverstackforaniorequestspanspan-idthedriverstackforaniorequestspanspan-idthedriverstackforaniorequestspanthe-driver-stack-for-an-io-request"></a><span id="The_driver_stack_for_an_I_O_request"></span><span id="the_driver_stack_for_an_i_o_request"></span><span id="THE_DRIVER_STACK_FOR_AN_I_O_REQUEST"></span>I/O 要求のドライバー スタック


前の図に示した I/O 要求に関与する 4 つのドライバーのシーケンスを考えてみましょう。 個々のデバイス ノードやそこに含まれる各デバイス スタックではなく、ドライバーそのものを重点的に捉えることにより、シーケンスを別の角度から見ることができます。 次の図に、ドライバーのシーケンスを上から下に見た状態を示します。 Disk.sys は、1 つのデバイス オブジェクトに関連付けられていますが、他の 3 つのドライバーは 2 つのデバイス オブジェクトに関連付けられています。

![ドライバー スタックの図 (最上段のドライバーが FDO だけに関連付けられ、他の 3 つはそれぞれ PDO と FDO に関連付けられている状態)](images/driverstack01.png)

I/O 要求に関与するドライバーのシーケンスは、"*I/O 要求のドライバー スタック*" と呼ばれます。 I/O 要求のドライバー スタックをわかりやすく説明するため、要求に関与する順序に従って各ドライバーを上から下に描いてみます。

I/O 要求のドライバー スタックは、デバイス ノードに対するデバイス スタックとはまったく異なることがわかります。 また、I/O 要求のドライバー スタックは必ずしも、デバイス ツリーの一部分で維持されるわけではありません。

## <a name="span-idtechnologydriverstacksspanspan-idtechnologydriverstacksspanspan-idtechnologydriverstacksspantechnology-driver-stacks"></a><span id="Technology_driver_stacks"></span><span id="technology_driver_stacks"></span><span id="TECHNOLOGY_DRIVER_STACKS"></span>テクノロジ ドライバー スタック


前の図に示した I/O 要求のドライバー スタックを考えてみましょう。 個々のドライバーにフレンドリ名を付け、図に多少の変更を加えることにより、Windows Driver Kit (WDK) ドキュメントに数多く見られるブロック図に似た図ができ上がります。

![フレンドリ名を付けたドライバーのドライバー スタックの図 (最上段に Disk クラス ドライバーがあり、以下 USB Storage ポート ドライバー、USB Hub ドライバーと (USB 2 ミニポート、USB ポート) ドライバーが続く状態)](images/driverstack02.png)

この図では、ドライバー スタックは 3 つのセクションに分かれています。 各セクションが特定のテクノロジ、またはオペレーティング システムに含まれる特定のコンポーネント、または部分に属するものと考えることができます。 たとえば、ドライバー スタックの最上段にある最初のセクションがボリューム マネージャーに属し、2 つ目のセクションがオペレーティング システムのストレージ コンポーネントに属し、3 つ目のセクションがオペレーティング システムの USB のコア部分に属していると考えることができます。

3 つ目のセクションのドライバーについて考えてみましょう。 各ドライバーは、多様な USB 要求や USB ハードウェアを処理するために Microsoft が提供している大規模な USB コア ドライバー群のサブセットに相当します。 次の図は、USB コアのブロック図全体がどのような状態になっているかを表したものです。

![考えられる USB コア ブロックのテクノロジ ドライバー スタックの図 ](images/technologystack01.png)

特定のテクノロジ、またはオペレーティング システムに含まれる特定のコンポーネントや部分に対するドライバーをすべて記載したブロック図のことを、"*テクノロジ ドライバー スタック*" と呼びます。 通常、テクノロジ ドライバー スタックには USB Core Driver Stack、Storage Stack、1394 Driver Stack、Audio Driver Stack などの名前が付けられています。

**注**  このトピックの USB コア ブロック図は、USB 1.0 と 2.0 のテクノロジ ドライバー スタックを表す各種の方法のうちの 1 つを表しています。 USB 1.0、2.0 と 3.0 のドライバー スタックの正式な図については、「[USB ドライバー スタック アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/hh406256)」をご覧ください。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバイス ノードとデバイス スタック](device-nodes-and-device-stacks.md)

[ミニドライバーとドライバーのペア](minidrivers-and-driver-pairs.md)

[すべてのドライバー開発者のための概念](concepts-and-knowledge-for-all-driver-developers.md)

 

 






