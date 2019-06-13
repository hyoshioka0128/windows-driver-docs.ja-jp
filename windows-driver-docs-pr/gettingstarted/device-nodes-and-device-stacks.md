---
title: デバイス ノードとデバイス スタック
description: Windows では、デバイスはプラグ アンド プレイ (PnP) デバイス ツリーのデバイス ノードによって表されます。
ms.assetid: 7bf38b3b-72ba-461c-b9e2-68b697359b37
keywords:
- デバイス ノード
- デバイス スタック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 693337e45cc83ba7443a1e0f1910aaa24c605591
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63371516"
---
# <a name="device-nodes-and-device-stacks"></a>デバイス ノードとデバイス スタック


Windows では、デバイスはプラグ アンド プレイ (PnP) デバイス ツリーのデバイス ノードによって表されます。 通常、デバイスに I/O 要求が送られると、複数のドライバーがその要求の処理をサポートします。 これらのドライバーはそれぞれデバイス オブジェクトに関連付けられ、デバイス オブジェクトはスタックに配置されます。 デバイス オブジェクトとデバイス オブジェクトに関連付けられているドライバーのシーケンスをデバイス スタックと呼びます。 デバイス ノードにはそれぞれ、独自のデバイス スタックがあります。

## <a name="span-iddevicenodesandtheplugandplaydevicetreespanspan-iddevicenodesandtheplugandplaydevicetreespanspan-iddevicenodesandtheplugandplaydevicetreespandevice-nodes-and-the-plug-and-play-device-tree"></a><span id="Device_nodes_and_the_Plug_and_Play_device_tree"></span><span id="device_nodes_and_the_plug_and_play_device_tree"></span><span id="DEVICE_NODES_AND_THE_PLUG_AND_PLAY_DEVICE_TREE"></span>デバイス ノードとプラグ アンド プレイ デバイス ツリー


Windows では、デバイスを "*プラグ アンド プレイ デバイス ツリー*" または単に "*デバイス ツリー*" と呼ばれるツリー構造にまとめます。 一般に、デバイス ツリーのノードは、1 つのデバイスまたは複合デバイス上の個々の機能を表します。 ただし、物理デバイスと関係のないソフトウェア コンポーネントを表すノードもあります。

デバイス ツリーのノードを、*デバイス ノード*と呼びます。 デバイス ツリーのルート ノードは、*ルート デバイス ノード*と呼びます。 規則によって、ルート デバイス ノードは、次の図に示すようにデバイス ツリーの下部に描画されます。

![デバイス ノードを表示するデバイス ツリーの図](images/devicetree01.png)

デバイス ツリーは、PnP 環境に固有の親/子関係を表します。 デバイス ツリーの一部のノードは、子デバイスが接続されたバスを表します。 たとえば、PCI バス ノードはマザーボード上の物理 PCI バスを表します。 起動時に、PnP マネージャーは PCI バス ドライバーに PCI バスに接続されているデバイスを列挙するように求めます。 これらのデバイスは、PCI バス ノードの子ノードとして表されます。 この図では、PCI バス ノードには、PCI バスに接続されている複数のデバイス (USB ホスト コントローラー、オーディオ コントローラー、PCI Express ポートなど) の子ノードがあります。

PCI バスに接続されているデバイスの一部は、それら自体がバスです。 PnP マネージャーはこれらの各バスに、接続されているデバイスを列挙するように求めます。 この図では、オーディオ コントローラーはオーディオ デバイスが接続されているバスです。 また、PCI Express ポートはディスプレイ アダプターが接続されているバスで、ディスプレイ アダプターは 1 台のモニターが接続されているバスです。

ノードがデバイスを表すと考えるかバスを表すと考えるかは、ユーザーの観点によって異なります。 たとえば、ディスプレイ アダプターは、画面に表示されるフレームの作成に重要な役割を果たすデバイスであると考えることができます。 しかし、同じディスプレイ アダプターを接続されているモニターを検出、列挙するバスと考えることもできます。

## <a name="span-iddeviceobjectsanddevicestacksspanspan-iddeviceobjectsanddevicestacksspanspan-iddeviceobjectsanddevicestacksspandevice-objects-and-device-stacks"></a><span id="Device_objects_and_device_stacks"></span><span id="device_objects_and_device_stacks"></span><span id="DEVICE_OBJECTS_AND_DEVICE_STACKS"></span>デバイス オブジェクトとデバイス スタック


"*デバイス オブジェクト*" は、[**DEVICE\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff543147) 構造のインスタンスです。 PnP デバイス ツリーの各デバイス ノードには順序が付けられたデバイス オブジェクトの一覧があり、これらの各デバイス オブジェクトはドライバーに関連付けられています。 順序が付けられたデバイス オブジェクトの一覧と、関連付けられているドライバーを、デバイス ノードの*デバイス スタック*と呼びます。

デバイス スタックは、いく通りかに考えることができます。 正式な意味では、デバイス スタックは順序が付けられた (デバイス オブジェクト、ドライバー) のペアです。 ただし、特定のコンテキストでは、デバイス スタックを順序が付けられたデバイス オブジェクトの一覧と考えると便利です。 また、他のコンテキストでは、デバイス スタックを順序が付けられたドライバーの一覧と考えると便利です。

規則では、デバイス スタックには上部と下部があります。 最初のデバイス オブジェクトはデバイス スタックの最下部に作られ、最後のデバイス オブジェクトはデバイス スタックの最上部に作られてアタッチされます。

次の図では、Proseware Gizmo デバイス ノードに 3 つの (デバイス オブジェクト、ドライバー) のペアを含むデバイス スタックがあります。 最上部のデバイス オブジェクトはドライバー AfterThought.sys に、中間のデバイス オブジェクトはドライバー Proseware.sys に、最下部のデバイス オブジェクトはドライバー Pci.sys に関連付けられています。 図の中央にある PCI バス ノードには、Pci.sys に関連付けられているデバイス オブジェクトと Acpi.sys に関連付けられているデバイス オブジェクトの 2 つの (デバイス オブジェクト、ドライバー) のペアを含むデバイス スタックがあります。

![Proseware Gizmo デバイス ノードと PCI デバイス ノードのデバイス スタックに並べられたデバイス オブジェクトを示す図](images/prosewaredevicenode01.png)

## <a name="span-idhowdoesadevicestackgetconstructedspanspan-idhowdoesadevicestackgetconstructedspanspan-idhowdoesadevicestackgetconstructedspanhow-does-a-device-stack-get-constructed"></a><span id="How_does_a_device_stack_get_constructed_"></span><span id="how_does_a_device_stack_get_constructed_"></span><span id="HOW_DOES_A_DEVICE_STACK_GET_CONSTRUCTED_"></span>デバイス スタックはどのように構築されるか


起動時に、PnP マネージャーは各バスのドライバーに、バスに接続されている子デバイスを列挙するように求めます。 たとえば、PnP マネージャーは PCI バス ドライバー (Pci.sys) に PCI バスに接続されているデバイスを列挙するように求めます。 この要求に応えて、Pci.sys は PCI バスに接続されている各デバイスのデバイス オブジェクトを作ります。 これらの各デバイス オブジェクトを、*物理デバイス オブジェクト* (PDO) と呼びます。 Pci.sys が PDO のセットを作成した直後のデバイス ツリーは次の図にようになります。

![PCI ノードと子デバイスの物理デバイス オブジェクトの図](images/prosewaredevicenode04.png)

PnP マネージャーはデバイス ノードを新たに作成した各 PDO に関連付け、レジストリを調べてどのドライバーがノードのデバイス スタックに含まれる必要があるかを判断します。 デバイス スタックには 1 つ (1 つのみ) の*ファンクション ドライバー*が必要で、オプションで 1 つ以上の*フィルター ドライバー*を持つことができます。 ファンクション ドライバーはデバイス スタックの主要ドライバーで、読み取り要求、書き込み要求、デバイス制御要求を処理します。 フィルター ドライバーは、読み取り要求、書き込み要求、デバイス制御要求を処理するうえで補助的な役割を果たします。 ファンクション ドライバーとフィルター ドライバーが読み込まれると、デバイス オブジェクトが作られ、デバイス スタックにアタッチされます。 ファンクション ドライバーによって作成されるデバイス オブジェクトを "*ファンクショナル デバイス オブジェクト*" (FDO) と呼び、フィルター ドライバーによって作成されるデバイス オブジェクトを "*フィルター デバイス オブジェクト*" (Filter DO) と呼びます。 デバイス ツリーは次の図のようになります。

![フィルター、機能、物理デバイス オブジェクトが表示された Proseware Gizmo デバイス ノードのデバイス ツリーの図](images/prosewaredevicenode02.png)

この図では、あるノードではフィルター ドライバーはファンクション ドライバーの上にあり、別のノードではフィルター ドライバーはファンクション ドライバーの下にあります。 デバイス スタックでファンクション ドライバーの上にあるフィルター ドライバーを、*上位フィルター ドライバー*と呼びます。 ファンクション ドライバーの下にあるフィルター ドライバーを、*下位フィルター ドライバー*と呼びます。

PDO は常にデバイス スタックの最下部のデバイス オブジェクトです。 これは、デバイス スタックが構築される方法によるもので、 PDO が最初に作られ、追加のデバイス オブジェクトがスタックにアタッチされるときには、既にあるスタックの上にアタッチされるためです。

**注**  デバイスのドライバーがインストールされると、インストーラーでは、情報 (INF) ファイルの情報を使って、どのドライバーがファンクション ドライバーで、どのドライバーがフィルター ドライバーかが判断されます。 通常、INF ファイルは Microsoft またはハードウェア ベンダーによって提供されます。 デバイスのドライバーがインストールされた後、PnP マネージャーはレジストリを調べて、デバイスのファンクション ドライバーとフィルター ドライバーを判断できます。

 

## <a name="span-idbusdriversspanspan-idbusdriversspanspan-idbusdriversspanbus-drivers"></a><span id="Bus_drivers"></span><span id="bus_drivers"></span><span id="BUS_DRIVERS"></span>バス ドライバー


この図では、ドライバー Pci.sys は 2 つの役割を果たしています。 まず、Pci.sys は PCI バス デバイス ノードの FDO に関連付けられています。 実際に、Pci.sys は PCI バス デバイス ノードの FDO を作成しました。 このため、Pci.sys は PCI バスのファンクション ドライバーです。 次に、Pci.sys は PCI バス ノードのそれぞれの子の PDO に関連付けられています。 Pci.sys が子デバイスの PDO を作成したことを思い出してください。 デバイス ノードの PDO を作成するドライバーを、ノードの "*バス ドライバー*" と呼びます。

PCI バスを基準とする場合、Pci.sys はファンクション ドライバーです。 しかし、Proseware Gizmo デバイスを基準とする場合、Pci.sys はバス ドライバーです。 PnP デバイス ツリーでは、このような 2 つの役割があることは一般的です。 バスのファンクション ドライバーとして機能するドライバーは、そのバスの子デバイスのバス ドライバーとしても機能します。

## <a name="span-iduser-modedevicestacksspanspan-iduser-modedevicestacksspanspan-iduser-modedevicestacksspanuser-mode-device-stacks"></a><span id="User-mode_device_stacks"></span><span id="user-mode_device_stacks"></span><span id="USER-MODE_DEVICE_STACKS"></span>ユーザー モード デバイス スタック


ここまで、カーネル モード デバイス スタックについて説明しました。 カーネル モード デバイス スタックでは、スタックのドライバーはカーネル モードで実行され、デバイス オブジェクトはシステム空間にマップされます。システム空間は、カーネル モードで実行するコードでのみ使用可能なアドレス空間です。 カーネル モードとユーザー モードの違いについて詳しくは、「[ユーザー モードとカーネル モード](user-mode-and-kernel-mode.md)」をご覧ください。

デバイスが、カーネル モード デバイス スタックのほかにユーザー モード デバイス スタックを持つこともあります。 ほとんどのユーザー モード ドライバーは、[Windows Driver Framework (WDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/) によって提供されるドライバー モデルの 1 つであるユーザー モード ドライバー フレームワーク (UMDF) に基づいています。 UMDF では、ドライバーはユーザー モード DLL で、デバイス オブジェクトは IWDFDevice インターフェイスを実装する COM オブジェクトです。 UMDF デバイス スタックのデバイス オブジェクトを、"*WDF デバイス オブジェクト*" (WDF DO) と呼びます。

次の図は、USB-FX-2 デバイスのデバイス ノード、カーネル モード デバイス スタック、ユーザー モード デバイス スタックを示しています。 ユーザー モード スタックとカーネル モード スタック両方のドライバーが、USB-FX-2 デバイス宛ての I/O 要求に関連しています。

![ユーザー モード デバイス スタックとカーネル モード デバイス スタックを示す図](images/userandkerneldevicestacks01.png)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[すべてのドライバー開発者のための概念](concepts-and-knowledge-for-all-driver-developers.md)

[ドライバー スタック](driver-stacks.md)

 

 






