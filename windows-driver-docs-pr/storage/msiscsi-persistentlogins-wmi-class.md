---
title: MSiSCSI\_PersistentLogins WMI クラス
description: MSiSCSI\_PersistentLogins WMI クラス
ms.assetid: 259220f8-af38-42b4-a0e3-88b4c396173d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5d1ace4416d8bda33a14adece82d90fe59f7efbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385825"
---
# <a name="msiscsipersistentlogins-wmi-class"></a>MSiSCSI\_PersistentLogins WMI クラス


## <span id="ddk_msiscsi_persistentlogins_wmi_class_kr"></span><span id="DDK_MSISCSI_PERSISTENTLOGINS_WMI_CLASS_KR"></span>


MSiSCSI\_PersistentLogins WMI クラスは、指定されたイニシエーターのインスタンスのログオン セッションを永続的なターゲットの一覧を報告します。 特定の永続的なログオン セッションごとに関連付けられている情報がによって定義されている、 [ISCSI\_永続的な\_ログイン WMI クラス](iscsi-persistent-login-wmi-class.md)します。

HBA イニシエーターを管理するミニポート ドライバーが、MSiSCSI を実装するために必要な\_PersistentLogins WMI クラスです。

MSiSCSI\_PersistentLogins クラスは発行されませんしで定義されている*Operations.mof*します。

WMI ツールのスイートでは、このクラスの定義をコンパイルするときに生成、 [ **MSiSCSI\_PersistentLogins** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_msiscsi_persistentlogins)データ構造体。

 

 





