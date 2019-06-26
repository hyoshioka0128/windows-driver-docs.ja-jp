---
title: RemoveConnectionFromSession
description: RemoveConnectionFromSession
ms.assetid: ae23713a-c75d-4669-a643-44e95dbb713c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 50fae22920c87ed5f8924a8b9c9e9591f3d7d3b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368954"
---
# <a name="removeconnectionfromsession"></a>RemoveConnectionFromSession


**RemoveConnectionFromSession**メソッド iSCSI イニシエーター ログオン セッションからの接続を削除する HBA を管理するミニポート ドライバーに指示します。

ISCSI イニシエーター (つまり、仮想ミニポート ドライバー) は、複数の接続セッションをサポートしていません。 使用しない**RemoveConnectionFromSession**の iSCSI イニシエーター。

**RemoveConnectionFromSession**メソッドでは、最後の接続、セッションから削除されません。 1 つの接続とセッションを閉じる必要があります、 [LogoutFromTarget](logoutfromtarget.md)メソッド。

**RemoveConnectionFromSession** 、パブリッシュされていないに属している[MSiSCSI\_操作 WMI クラス](msiscsi-operations-wmi-class.md)します。 パラメーターの説明については、 **RemoveConnectionFromSession**メソッドのメンバーの説明を参照してください、 [ **RemoveConnectionFromSession\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_removeconnectionfromsession_in)と[ **RemoveConnectionFromSession\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_removeconnectionfromsession_out)構造体。

ミニポート ドライバー、MSiSCSI を実装する\_操作 WMI クラスは、このメソッドをサポートする必要があります。

 

 





