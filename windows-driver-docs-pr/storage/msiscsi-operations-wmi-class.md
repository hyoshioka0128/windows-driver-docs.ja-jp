---
title: MSiSCSI\_操作 WMI クラス
description: MSiSCSI\_操作 WMI クラス
ms.assetid: 993118db-cddf-438a-8fdd-566353a6246b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5c1750284c9eb452d5af8eac6d9f0a6062d1eeb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536511"
---
# <a name="msiscsioperations-wmi-class"></a>MSiSCSI\_操作 WMI クラス


## <span id="ddk_msiscsi_operations_wmi_class_kr"></span><span id="DDK_MSISCSI_OPERATIONS_WMI_CLASS_KR"></span>


MSiSCSI\_操作 WMI クラスは、iSCSI イニシエーター サービスが HBA イニシエーターとの通信に使用する WMI メソッドを提供します。

このクラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付けられているため、ミニポート ドライバーは、ミニポート ドライバーを管理する特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要があります。

この WMI クラスには、データのブロック; がありません。そのため、WMI ツールのスイートでは、このクラスの定義をコンパイルするときに、クラスに対応する構造体の宣言を生成しません。 コンパイルは、クラスのメソッドに関連付けられている構造体の宣言を生成し、クラスのメソッドのリファレンス ページで、それらについて説明します。

メソッドのリファレンス ページは、このクラスに属している各メソッドの管理オブジェクト フォーマット (MOF) 構文を説明します。 次のトピックでは、これらのメソッドとそれらに付随する構造体について説明します。

[AddConnectionToSession](addconnectiontosession.md)

[AddRADIUSServer](addradiusserver.md)

[DeleteInitiatorNodeName](deleteinitiatornodename.md)

[LoginToTarget](logintotarget.md)

[LogoutFromTarget](logoutfromtarget.md)

[RemoveConnectionFromSession](removeconnectionfromsession.md)

[RemovePersistentLogin](removepersistentlogin.md)

[RemoveRADIUSServer](removeradiusserver.md)

[**ScsiInquiry**](scsiinquiry.md)

[**ScsiReadCapacity**](scsireadcapacity.md)

[**ScsiReportLuns**](scsireportluns.md)

[SendTargets](sendtargets.md)

[SetCHAPSharedSecret](setchapsharedsecret.md)

[SetInitiatorNodeName](setinitiatornodename.md)

[SetRADIUSSharedSecret](setradiussharedsecret.md)

 

 





