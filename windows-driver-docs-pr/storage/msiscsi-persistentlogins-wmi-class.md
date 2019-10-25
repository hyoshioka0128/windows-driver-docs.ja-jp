---
title: MSiSCSI\_PersistentLogins WMI クラス
description: MSiSCSI\_PersistentLogins WMI クラス
ms.assetid: 259220f8-af38-42b4-a0e3-88b4c396173d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2293665cfd03300d93f758f58351c1cd0a1eb532
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845338"
---
# <a name="msiscsi_persistentlogins-wmi-class"></a>MSiSCSI\_PersistentLogins WMI クラス


## <span id="ddk_msiscsi_persistentlogins_wmi_class_kr"></span><span id="DDK_MSISCSI_PERSISTENTLOGINS_WMI_CLASS_KR"></span>


MSiSCSI\_PersistentLogins WMI クラスは、指定されたイニシエーターインスタンスの永続的なターゲットログオンセッションの一覧を報告します。 特定の永続ログオンセッションに関連付けられている情報は、 [ISCSI\_永続的な\_ログイン WMI クラス](iscsi-persistent-login-wmi-class.md)によって定義されます。

HBA イニシエーターを管理するミニポートドライバーは、MSiSCSI\_PersistentLogins WMI クラスを実装するために必要です。

MSiSCSI\_PersistentLogins クラスは発行されていないため、*操作 .mof*で定義されています。

WMI ツールスイートは、このクラス定義をコンパイルするときに、 [**Msiscsi\_PersistentLogins**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_msiscsi_persistentlogins)データ構造体を生成します。

 

 





