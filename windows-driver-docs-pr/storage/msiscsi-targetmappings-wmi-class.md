---
title: MSiSCSI\_TargetMappings WMI クラス
description: MSiSCSI\_TargetMappings WMI クラス
ms.assetid: 12bfe80a-8431-4607-99f5-ddd6815aecc6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 73aeb9a6f69518a8b8775ce96ac69c5c383437e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838871"
---
# <a name="msiscsi_targetmappings-wmi-class"></a>MSiSCSI\_TargetMappings WMI クラス


## <span id="ddk_msiscsi_targetmappings_wmi_class_kr"></span><span id="DDK_MSISCSI_TARGETMAPPINGS_WMI_CLASS_KR"></span>


MSiSCSI\_TargetMappings WMI クラスには、セッションに関連付けられている一連の iSCSI 論理ユニット番号 (LUN) マッピングが含まれています。 イニシエーターが確立したログインセッションによって公開されている各 LUN のマッピングがあります。 各セッションのマッピングは、MSiSCSI\_Targetmapping WMI クラス内の埋め込みクラスである[ISCSI\_TargetMapping wmi クラス](iscsi-targetmapping-wmi-class.md)のインスタンスによって記述されます。

すべての iSCSI イニシエーターは、MSiSCSI\_TargetMappings クラスを実装する必要があります。 ISCSI イニシエーターサービスは、このクラスを使用して HBA イニシエーターと通信します。

開始側 HBA を管理するミニポートドライバーの各インスタンスに対して、MSiSCSI\_TargetMappings WMI クラスのインスタンスが1つ存在する必要があります。 ミニポートドライバーは、ミニポートドライバーが管理する特定の物理デバイスオブジェクト (PDO) の名前を使用して、MSiSCSI\_TargetMappings クラスを登録する必要があります。

MSiSCSI\_TargetMappings クラスは発行されていないため、*操作 .mof*で定義されています。

WMI ツールスイートは、このクラス定義をコンパイルするときに、 [**msiscsi\_TargetMappings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_msiscsi_targetmappings)データ構造を生成します。

MSiSCSI\_TargetMappings クラスを実装するには、イニシエーターが必要です。

ISCSI イニシエーターサービスは、MSiSCSI\_TargetMappings クラスに依存して、HBA イニシエーターと通信します。 HBA イニシエーターを管理するミニポートドライバーは、HBA ごとに MSiSCSI\_TargetMappings クラスの1つのインスタンスを実装する必要があります。

イニシエーターは、HBA の PDO の名前を使用して、MSiSCSI\_TargetMappings クラスを登録する必要があります。

 

 





