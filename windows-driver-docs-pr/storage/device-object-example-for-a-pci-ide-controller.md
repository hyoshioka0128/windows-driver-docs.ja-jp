---
title: PCI IDE コントローラーのデバイス オブジェクトの例
description: PCI IDE コントローラーのデバイス オブジェクトの例
ms.assetid: 7cb97da7-1d94-42a1-af3a-9085e68c8f28
keywords:
- ストレージ ドライバー WDK、デバイス オブジェクト
- デバイス オブジェクトの WDK ストレージ
- PCI の IDE コント ローラーの使用例 WDK ストレージ
- IDE コント ローラーの WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28748d270a4b8d06b8d4c7a65ea683546626b01d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331733"
---
# <a name="device-object-example-for-a-pci-ide-controller"></a>PCI IDE コントローラーのデバイス オブジェクトの例


## <span id="ddk_device_object_example_for_a_pci_ide_controller_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_A_PCI_IDE_CONTROLLER_KG"></span>


次の図は、システムの 1 つのチャネルと、IDE の CD-ROM に接続された 2 つの IDE ディスクのある PCI IDE コント ローラーを使用して作成されるデバイス オブジェクトに他のアタッチを示します。

![デバイス オブジェクトを 1 つのチャネル、もう一方に接続されている、IDE の CD-ROM に接続されている 2 つの IDE ディスクを持つ、PCI IDE コント ローラーを使用してシステム用に作成されます。](images/kg201-4.png)

CD-ROM と IDE コント ローラー上のディスク デバイスのデバイス オブジェクトのツリー

以降、図の下部では、次に示します各デバイス オブジェクトとその関連するドライバー。

1.  PCI バス ドライバーでは、PCI バス FDO を作成し、PCI バス (この図では表示されません)、PnP マネージャーによって作成された PDO にアタッチします。

2.  PCI バス ドライバーでは、アダプターと、すべて、IDE コント ローラーを含め、そのバス上のコント ローラーを列挙し、それぞれの PDO を作成します。

3.  IDE コント ローラー ミニドライバーと共に、IDE コント ローラー ドライバーでは、FDO を作成し、コント ローラーの PDO にアタッチします。

4.  IDE コント ローラーのドライバーは、コント ローラーのチャネルを「列挙」します。 実際には、これは、コント ローラーのチャネルごとに 1 つ、2 つの Pdo を作成して、接続されている意味両方チャネル Pdo FDO コント ローラーにします。

5.  IDE チャネルのドライバーでは、FDO を作成し、チャネルの PDO を結び付けます。

6.  IDE チャネルのドライバーでは、そのチャネル上のデバイスを列挙し、各デバイスの PDO を作成します。 IEEE 1394 のコント ローラー上の CD-ROM デバイスは、IDE チャネルのドライバーによって作成されたこのような 3 つの Pdo を示していますのデバイス オブジェクトのツリーを示す図コント ローラーの最初のチャネルのチャネルのドライバーによって作成された 2 つのハード ディスク ドライブ Pdo と。コント ローラーの 2 番目のチャネルのチャネルのドライバーによって作成された CD-ROM PDO します。

7.  ディスク クラス ドライバーが FDO を作成し、関連付けられているディスク、SCSI の場合同様に、PDO に接続されると、および、CD-ROM ドライバーは FDO を作成し、関連付けられている CD-ROM PDO にアタッチします。 PDO のデバイスとデバイス FDO の間は、SCSI のように、フィルター ドライバーを挿入することができますの操作を行います。 IEEE 1394 のコント ローラー上の CD-ROM デバイスでデバイス オブジェクト ツリーを示す図は、このを使用して、CD オーディオ フィルター CD-ROM PDO のすぐ上必要に応じて配置できるかを示しています。

 

 




