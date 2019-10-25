---
title: RemoveConnectionFromSession
description: RemoveConnectionFromSession
ms.assetid: ae23713a-c75d-4669-a643-44e95dbb713c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 590e3ba7410419d1d9cd51f5b832e413c20218d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842714"
---
# <a name="removeconnectionfromsession"></a>RemoveConnectionFromSession


**Removeconnectionfromsession**メソッドは、ISCSI イニシエーター HBA を管理するミニポートドライバーに対して、ログオンセッションからの接続を削除するように指示します。

ISCSI イニシエーター (つまり、仮想ミニポートドライバー) は、複数の接続を持つセッションをサポートしていません。 ISCSI イニシエーターで**Removeconnectionfromsession**を使用しないでください。

**Removeconnectionfromsession**メソッドでは、セッションからの最後の接続は削除されません。 [Logoutfromtarget](logoutfromtarget.md)メソッドを使用して、単一の接続でセッションを閉じる必要があります。

**Removeconnectionfromsession**は、発行されていない[Msiscsi\_Operations WMI クラス](msiscsi-operations-wmi-class.md)に属しています。 **Removeconnectionfromsession**メソッドのパラメーターの説明については、「 [ **」の\_removeconnectionfromsession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_removeconnectionfromsession_in)のメンバーの説明を参照してください。また、 [**REMOVECONNECTIONFROMSESSION\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_removeconnectionfromsession_out)構造体を参照してください。

MSiSCSI\_Operations WMI クラスを実装するミニポートドライバーは、このメソッドをサポートしている必要があります。

 

 





