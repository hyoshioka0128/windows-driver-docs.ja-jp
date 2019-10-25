---
title: MSiSCSI\_LUNMappingInformation WMI クラス
description: MSiSCSI\_LUNMappingInformation WMI クラス
ms.assetid: 646add52-f946-4169-9f6b-974253ec30af
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 35fa9621b173a2980b79736b5ae1423f4fbdd50a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845347"
---
# <a name="msiscsi_lunmappinginformation-wmi-class"></a>MSiSCSI\_LUNMappingInformation WMI クラス


## <span id="ddk_msiscsi_lunmappinginformation_wmi_class_kr"></span><span id="DDK_MSISCSI_LUNMAPPINGINFORMATION_WMI_CLASS_KR"></span>


MSiSCSI\_LUNMappingInformation クラスは、オペレーティングシステムが特定の論理ユニットに割り当てる SCSI アドレス情報を公開します。 SCSI アドレス情報は、 [msiscsi\_TargetMappings WMI クラス](msiscsi-targetmappings-wmi-class.md)が報告する情報と一致している必要があります。

ミニポートドライバーは、論理ユニットに関連付けられている各物理デバイスオブジェクト (PDO) に対して、MSiSCSI\_LUNMappingInformation WMI クラスのインスタンスを1つ作成する必要があります。

このクラスは特定の LUN に関連付けられているため、HBA を管理するミニポートドライバーは、LUN の PDO の名前を使用してこのクラスを登録する必要があります。

MSiSCSI\_LUNMappingInformation クラスは発行されていないため、*操作 .mof*で定義されています。

WMI ツールスイートは、このクラス定義をコンパイルするときに、 [**Msiscsi\_LUNMappingInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_msiscsi_lunmappinginformation)データ構造を生成します。

MSiSCSI\_LUNMappingInformation によって公開される SCSI アドレス情報は、論理ユニットの列挙中に、イニシエーターのミニポートドライバーによってポートドライバーに提供された情報と一致している必要があります。

MSiSCSI\_LUNMappingInformation クラスを実装するには、イニシエーターが必要です。

イニシエーターは、論理ユニットの PDO の名前を使用して、MSiSCSI\_LUNMappingInformation クラスを登録する必要があります。

イニシエーターは、列挙する論理ユニットごとに、MSiSCSI\_LUNMappingInformation クラスのインスタンスを1つ作成する必要があります。

 

 





