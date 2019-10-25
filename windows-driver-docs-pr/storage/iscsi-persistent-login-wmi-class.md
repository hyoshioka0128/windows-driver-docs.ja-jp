---
title: ISCSI\_永続的\_ログイン WMI クラス
description: ISCSI\_永続的\_ログイン WMI クラス
ms.assetid: ad00e6ed-adfa-4888-9386-51f937a278d8
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a15008e1fd8bde006f84850d3424c06743a014aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842263"
---
# <a name="iscsi_persistent_login-wmi-class"></a>ISCSI\_永続的\_ログイン WMI クラス


## <span id="ddk_iscsi_persistent_login_wmi_class_kr"></span><span id="DDK_ISCSI_PERSISTENT_LOGIN_WMI_CLASS_KR"></span>


ISCSI\_永続的な\_ログイン WMI クラスは、永続的なログオンを定義します。 ISCSI イニシエーターを管理するミニポートドライバーは、ストレージドライバースタックに読み込まれるとすぐに、永続的なログオン接続を自動的に確立します。 このタイミングによって、イニシエーターが永続的なログオンを保持するターゲットが、起動プロセスの早い段階でシステムで使用できるようになります。

ISCSI\_永続的な\_ログインクラスは発行されていないため、*操作 .mof*で定義されています。

WMI ツールスイートは、このクラス定義をコンパイルするときに、 [**ISCSI\_永続的な\_ログイン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_iscsi_persistent_login)データ構造を生成します。

 

 





