---
title: MSiSCSI\_LUNMappingInformation WMI クラス
description: MSiSCSI\_LUNMappingInformation WMI クラス
ms.assetid: 646add52-f946-4169-9f6b-974253ec30af
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7dfc7dc88017bf152120bf2746d4bdf20bdcedde
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353507"
---
# <a name="msiscsilunmappinginformation-wmi-class"></a>MSiSCSI\_LUNMappingInformation WMI クラス


## <span id="ddk_msiscsi_lunmappinginformation_wmi_class_kr"></span><span id="DDK_MSISCSI_LUNMAPPINGINFORMATION_WMI_CLASS_KR"></span>


MSiSCSI\_LUNMappingInformation クラスは、特定の論理ユニットに、オペレーティング システムを代入する SCSI アドレス情報を公開します。 SCSI アドレス情報を一貫性のある情報を使用する必要がありますが、 [MSiSCSI\_TargetMappings WMI クラス](msiscsi-targetmappings-wmi-class.md)レポートします。

ミニポート ドライバーは、MSiSCSI の 1 つのインスタンスを作成する必要があります\_論理ユニットに関連付けられている各物理デバイス オブジェクト (PDO) LUNMappingInformation WMI クラスです。

このクラスが特定の LUN に関連付けられるため、HBA を管理するミニポート ドライバーは、LUN の PDO の名前を使用してこのクラスを登録する必要があります。

MSiSCSI\_LUNMappingInformation クラスは発行されませんしで定義されている*Operations.mof*します。

WMI ツールのスイートでは、このクラスの定義をコンパイルするときに生成、 [ **MSiSCSI\_LUNMappingInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_msiscsi_lunmappinginformation)データ構造体。

SCSI アドレス情報をその MSiSCSI\_LUNMappingInformation 公開は、イニシエーターのミニポート ドライバーが提供される情報と一致する必要があります、論理ユニットの列挙中にポート ドライバーにします。

イニシエーターは、MSiSCSI を実装する必要は\_LUNMappingInformation クラス。

イニシエーターは、MSiSCSI を登録する必要があります\_LUNMappingInformation のクラスに論理ユニットの PDO の名前を使用します。

イニシエーターは、MSiSCSI の 1 つのインスタンスを作成する必要があります\_が列挙された論理ユニットごとの LUNMappingInformation クラス。

 

 





