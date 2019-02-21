---
title: デバイスを削除します。
description: デバイスを削除します。
ms.assetid: 8184987f-5c46-4dd6-aad2-3c32b14205fd
keywords:
- PnP WDK カーネルでは、デバイスの削除
- プラグ アンド プレイの WDK カーネル、デバイスの削除
- デバイスの削除
- WDK の PnP、デバイスの削除の通知
- WDK PnP Irp
- I/O 要求パケット PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2033825edfa1e8b00f056f58fe6bd45c5227cfbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550542"
---
# <a name="removing-a-device"></a>デバイスを削除します。





PnP マネージャーでは、デバイス、またはコンピューターから物理的に削除されるときに、デバイスの場合は、そのデバイス オブジェクトを削除するドライバーを指示します。 PnP マネージャーも送信、*削除*IRP デバイスは無効か、または起動に失敗したときに、デバイス、Windows 2000 以降で、ドライバーを更新するユーザーを要求するとします。

次のセクションでは、説明、PnP マネージャーが発行したとき*削除*Irp とそれらの Irp に応答するドライバーが行う必要があります。 このセクションでは、次のトピックについて説明します。

[Irp を削除する場合は、発行](understanding-when-remove-irps-are-issued.md)

[IRP の処理\_MN\_クエリ\_削除\_デバイス要求](handling-an-irp-mn-query-remove-device-request.md)

[IRP の処理\_MN\_削除\_デバイス要求](handling-an-irp-mn-remove-device-request.md)

[IRP の処理\_MN\_キャンセル\_削除\_デバイス要求](handling-an-irp-mn-cancel-remove-device-request.md)

[IRP の処理\_MN\_突然\_削除要求](handling-an-irp-mn-surprise-removal-request.md)

[削除ロックを使用します。](using-remove-locks.md)

 

 




