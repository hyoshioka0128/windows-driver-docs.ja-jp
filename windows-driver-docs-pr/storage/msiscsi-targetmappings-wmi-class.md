---
title: MSiSCSI\_TargetMappings WMI クラス
description: MSiSCSI\_TargetMappings WMI クラス
ms.assetid: 12bfe80a-8431-4607-99f5-ddd6815aecc6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 106ace48cc639d24bbbc3d7c7679463e47801a17
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384665"
---
# <a name="msiscsitargetmappings-wmi-class"></a>MSiSCSI\_TargetMappings WMI クラス


## <span id="ddk_msiscsi_targetmappings_wmi_class_kr"></span><span id="DDK_MSISCSI_TARGETMAPPINGS_WMI_CLASS_KR"></span>


MSiSCSI\_TargetMappings WMI クラスには、一連セッションに関連付けられている iSCSI の論理ユニット番号 (LUN) マッピングにはが含まれています。 イニシエーターが確立されているログインのセッションによって公開される各 LUN のマッピングがあります。 各セッションのマッピングがのインスタンスによって説明されている、 [ISCSI\_TargetMapping WMI クラス](iscsi-targetmapping-wmi-class.md)、MSiSCSI 内で埋め込みクラスは\_TargetMappings WMI クラスです。

すべての iSCSI イニシエーターは、MSiSCSI を実装する必要があります\_TargetMappings クラス。 ISCSI イニシエーター サービスは、HBA イニシエーターと通信するには、このクラスに依存します。

1 つのインスタンス、MSiSCSI の必要があります\_HBA イニシエーターを管理するミニポート ドライバーの読み込まれた各インスタンスについて TargetMappings WMI クラスです。 ミニポート ドライバーは、MSiSCSI を登録する必要があります\_TargetMappings クラスのミニポート ドライバーを管理する特定の物理デバイス オブジェクト (PDO) の名前を使用します。

MSiSCSI\_TargetMappings クラスは発行されませんしで定義されている*Operations.mof*します。

WMI ツールのスイートでは、このクラスの定義をコンパイルするときに生成、 [ **MSiSCSI\_TargetMappings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_msiscsi_targetmappings)データ構造体。

イニシエーターは、MSiSCSI を実装する必要は\_TargetMappings クラス。

ISCSI イニシエーター サービスが依存、MSiSCSI\_HBA イニシエーターとの通信に TargetMappings クラス。 HBA イニシエーターを管理するミニポート ドライバーは、MSiSCSI の 1 つのインスタンスを実装する必要があります\_HBA あたり TargetMappings クラス。

イニシエーターは、MSiSCSI を登録する必要があります\_TargetMappings クラスの HBA の PDO の名前を使用します。

 

 





