---
title: IEEE 1394 コント ローラーのデバイス オブジェクトの例
description: IEEE 1394 コント ローラーのデバイス オブジェクトの例
ms.assetid: 9a83786b-8821-43b7-bf86-c85f2dcb9749
keywords:
- ストレージ ドライバー WDK、デバイス オブジェクト
- デバイス オブジェクトの WDK ストレージ
- コント ローラーの例の IEEE 1394 WDK ストレージ
- WDK ストレージ PCI IEEE 1394 のコント ローラーの例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77a6f784544a26f8a37010986f0f6d2fd9e23fc8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553751"
---
# <a name="device-object-example-for-an-ieee-1394-controller"></a>IEEE 1394 コント ローラーのデバイス オブジェクトの例


## <span id="ddk_device_object_example_for_an_ieee_1394_controller_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_AN_IEEE_1394_CONTROLLER_KG"></span>


次の図には、IEEE 1394 接続されている CD-ROM で PCI IEEE 1394 コント ローラーのシステムに対して作成されたデバイス オブジェクトが表示されます。 SCSI アダプターに接続されているデバイスのデバイス オブジェクトが記載されて[SCSI HBA のデバイス オブジェクトの例](device-object-example-for-a-scsi-hba.md)します。

![デバイス オブジェクトのシステムでは、IEEE 1394 接続されている CD-ROM PCI IEEE 1394 コント ローラーで作成されます。](images/kg201-3.png)

IEEE 1394 のコント ローラー上の CD-ROM デバイス用のデバイス オブジェクトのツリー

以降、図の下部では、次に示します各デバイス オブジェクトとその対応するドライバー。

1.  Pdo のアダプターの最大記憶域バス FDO から、デバイス ツリーの説明は、[SCSI HBA のデバイス オブジェクトの例](device-object-example-for-a-scsi-hba.md)を参照してください。

2.  IEEE 1394 ドライバー スタックの最上位のドライバーでは、SBP2 ディスク デバイス PDO を作成します。 最終的には、IEEE 1394 のドライバー スタックは、IEEE 1394 バス上のターゲットの CD-ROM デバイスに SBP2 コマンドを発行します。

3.  IEEE 1394 記憶域のシステムが指定したポート ドライバーは、フィルター操作を作成し、PDO SBP2 ディスク デバイスにアタッチします。 フィルター ドライバーとして実装されます。 記憶域の IEEE 1394 ポート ドライバーでは、基になる IEEE 1394 ドライバー スタックに発行された SBP2 コマンドに CD-ROM クラス ドライバーからされる Srb を変換します。 このドライバーは次の下位の記憶装置ドライバーをインターフェイスで説明されている SCSI ポート/ミニポート ドライバーによって表示されるのと同じ[SCSI HBA のデバイス オブジェクトの例](device-object-example-for-a-scsi-hba.md)します。

4.  CD-ROM クラス ドライバーが FDO を作成しは SBP2 ポート フィルターは次の下位のデバイス オブジェクトにアタッチまたは別のフィルター、介在するフィルター ドライバーによってスタックに接続しないでください。 クラスのドライバーでは、下位のドライバーのデバイス オブジェクトを使用してデバイスをすべての後続の要求を発行します。

 

 




