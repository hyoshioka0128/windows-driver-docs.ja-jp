---
title: ScsiReadCapacity
description: ScsiReadCapacity
ms.assetid: ee4a0d3f-028b-4d25-badf-393198da3191
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a5c8934bc35a74d89a03e860ca8019757bdecb46
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842636"
---
# <a name="scsireadcapacity"></a>ScsiReadCapacity


**ScsiReadCapacity**メソッドは、ISCSI イニシエーター HBA を管理するミニポートドライバーに対して、ターゲットにログオンし、SCSI 読み取り容量コマンドをターゲットの論理ユニットに発行し、結果を返すように指示します。

この WMI メソッドは、発行されていない[Msiscsi\_OPERATIONS WMI クラス](msiscsi-operations-wmi-class.md)に属しています。 **ScsiReadCapacity**メソッドのパラメーターの説明については、「」および「 [**ScsiReadCapacity\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsireadcapacity_out)構造体」の「メンバーの[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsireadcapacity_in)説明」を参照してください。

MSiSCSI\_Operations WMI クラスを実装するミニポートドライバーは、 **ScsiReadCapacity**をサポートしている必要があります。

 

 





