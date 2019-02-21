---
title: ISCSI\_永続的な\_Login WMI クラス
description: ISCSI\_永続的な\_Login WMI クラス
ms.assetid: ad00e6ed-adfa-4888-9386-51f937a278d8
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 96badd06cbd1ec2fb4f135ae9828f6978ffd828c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558676"
---
# <a name="iscsipersistentlogin-wmi-class"></a>ISCSI\_永続的な\_Login WMI クラス


## <span id="ddk_iscsi_persistent_login_wmi_class_kr"></span><span id="DDK_ISCSI_PERSISTENT_LOGIN_WMI_CLASS_KR"></span>


ISCSI\_持続\_ログイン WMI クラスは永続的なログオンを定義します。 ISCSI イニシエーターを自動的に管理するミニポート ドライバーは、記憶域ドライバー スタックにロードされるとすぐに永続的なログオンの接続を確立します。 このタイミングでは、ターゲットがイニシエーターは永続的なログオンをできるだけスタートアップ プロセスの早い段階でのシステムで使用可能になることが保証されます。

ISCSI\_持続\_ログイン クラスは発行されませんしで定義されている*Operations.mof*します。

WMI ツールのスイートでは、このクラスの定義をコンパイルするときに生成、 [ **ISCSI\_持続\_ログイン**](https://msdn.microsoft.com/library/windows/hardware/ff561553)データ構造体。

 

 





