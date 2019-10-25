---
title: ClearCache
description: ClearCache
ms.assetid: b332d9ce-baee-4742-8e8b-370f5be94a3c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ff8e09afe574eb2fa5e9d816a73f1f824e3e8178
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844383"
---
# <a name="clearcache"></a>ClearCache


**Clearcache**メソッドは、iSCSI 認証と事前共有キーのキャッシュをクリアするようイニシエーター HBA に指示します。 このメソッドでは、その他の永続的な情報をクリア*しない*でください。 特に、永続的なログオンは削除しないでください。

**Clearcache**は、発行されていない[Msiscsi\_SECURITYCONFIGOPERATIONS WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)に属しています。 **Clearcache**メソッドのパラメーターの説明については、 [**CLEARCACHE\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_clearcache_out)構造体のメンバーの説明を参照してください。

 

 





