---
title: バス ドライバーでのシステム電源クエリ IRP の処理
description: バス ドライバーでのシステム電源クエリ IRP の処理
ms.assetid: d42c268e-d57d-41a6-8e61-67c651082106
keywords:
- クエリ power Irp WDK の電源管理
- バス ドライバー WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f9b15b0364ad163d767aac3510dbc4faf3fb375
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359829"
---
# <a name="handling-a-system-query-power-irp-in-a-bus-driver"></a>バス ドライバーでのシステム電源クエリ IRP の処理





システム クエリ性能の要求では、バス ドライバー (これは、デバイスの電源ポリシー所有者ではない) に達すると、ドライバーはクエリ対象のシステム電源の状態に対応するデバイスの電源状態をサポートしていることによりと、ウェイク アップを有効にするクエリ対象のシステム電源の状態では、システムをスリープ解除からそのデバイスはできなくなります。

バス ドライバーの設定では、Windows 7 および Windows Vista では、 **Irp -&gt;IoStatus.Status**ステータス\_成功ドライバーで指定された電源の状態を変更できますまたはドライバーができない場合は、エラー状態を設定します。

バス ドライバーの最初の呼び出しでは、Windows Server 2003、Windows XP、および Windows 2000、 [ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)し、設定**Irp -&gt;IoStatus.Status**にステータス\_成功ドライバーで指定された電源の状態を変更できますまたはドライバーができない場合は、エラー状態を設定します。

電源マネージャーを呼び出す、バス ドライバーには、IRP が完了すると、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP が渡されるときに、その他のドライバーによって設定ルーチンがスタックをダウンします。

 

 




