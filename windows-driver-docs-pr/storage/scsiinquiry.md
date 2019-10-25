---
title: ScsiInquiry
description: ScsiInquiry
ms.assetid: a4f6f21c-b096-4a2f-a207-e8618682e780
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26d3c6f47a20fd6e90d546e96dc9313556d06df9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842650"
---
# <a name="scsiinquiry"></a>ScsiInquiry


**ScsiInquiry**メソッドは、ISCSI イニシエーター HBA を管理するミニポートドライバーに対して、ターゲットの論理ユニットに SCSI 照会コマンドを発行し、結果を返すように指示します。

この WMI メソッドは、発行されていない[Msiscsi\_OPERATIONS WMI クラス](msiscsi-operations-wmi-class.md)に属しています。 **ScsiInquiry**メソッドのパラメーターの説明については、「」および「 [**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体」の「メンバーの[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in)説明」を参照してください。

MSiSCSI\_Operations WMI クラスを実装するミニポートドライバーは、 **ScsiInquiry**をサポートしている必要があります。

 

 





