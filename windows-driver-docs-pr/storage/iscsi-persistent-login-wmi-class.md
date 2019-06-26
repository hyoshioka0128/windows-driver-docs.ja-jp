---
title: ISCSI\_永続的な\_Login WMI クラス
description: ISCSI\_永続的な\_Login WMI クラス
ms.assetid: ad00e6ed-adfa-4888-9386-51f937a278d8
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 69affbc9b69b4192b0c05baa8be72ba8a1b545b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378438"
---
# <a name="iscsipersistentlogin-wmi-class"></a>ISCSI\_永続的な\_Login WMI クラス


## <span id="ddk_iscsi_persistent_login_wmi_class_kr"></span><span id="DDK_ISCSI_PERSISTENT_LOGIN_WMI_CLASS_KR"></span>


ISCSI\_持続\_ログイン WMI クラスは永続的なログオンを定義します。 ISCSI イニシエーターを自動的に管理するミニポート ドライバーは、記憶域ドライバー スタックにロードされるとすぐに永続的なログオンの接続を確立します。 このタイミングでは、ターゲットがイニシエーターは永続的なログオンをできるだけスタートアップ プロセスの早い段階でのシステムで使用可能になることが保証されます。

ISCSI\_持続\_ログイン クラスは発行されませんしで定義されている*Operations.mof*します。

WMI ツールのスイートでは、このクラスの定義をコンパイルするときに生成、 [ **ISCSI\_持続\_ログイン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_iscsi_persistent_login)データ構造体。

 

 





