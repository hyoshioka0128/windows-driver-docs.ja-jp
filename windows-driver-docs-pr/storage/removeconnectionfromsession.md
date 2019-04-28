---
title: RemoveConnectionFromSession
description: RemoveConnectionFromSession
ms.assetid: ae23713a-c75d-4669-a643-44e95dbb713c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 90ffa0371ee38faa104854609c99ec2cf2592166
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374183"
---
# <a name="removeconnectionfromsession"></a>RemoveConnectionFromSession


**RemoveConnectionFromSession**メソッド iSCSI イニシエーター ログオン セッションからの接続を削除する HBA を管理するミニポート ドライバーに指示します。

ISCSI イニシエーター (つまり、仮想ミニポート ドライバー) は、複数の接続セッションをサポートしていません。 使用しない**RemoveConnectionFromSession**の iSCSI イニシエーター。

**RemoveConnectionFromSession**メソッドでは、最後の接続、セッションから削除されません。 1 つの接続とセッションを閉じる必要があります、 [LogoutFromTarget](logoutfromtarget.md)メソッド。

**RemoveConnectionFromSession** 、パブリッシュされていないに属している[MSiSCSI\_操作 WMI クラス](msiscsi-operations-wmi-class.md)します。 パラメーターの説明については、 **RemoveConnectionFromSession**メソッドのメンバーの説明を参照してください、 [ **RemoveConnectionFromSession\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff563974)と[ **RemoveConnectionFromSession\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff563976)構造体。

ミニポート ドライバー、MSiSCSI を実装する\_操作 WMI クラスは、このメソッドをサポートする必要があります。

 

 





