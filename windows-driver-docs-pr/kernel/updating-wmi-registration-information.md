---
title: WMI 登録情報の更新
description: WMI 登録情報の更新
ms.assetid: d24688e5-bb50-4bce-a4d4-4a3bf886f86d
keywords:
- WMI の WDK カーネルでは、WMI に登録します。
- WMI データ プロバイダーを登録します。
- WDK の WMI のデータ プロバイダー
- ドライバー WDK WMI の登録
- イベントは、WDK の WMI をブロックします。
- WDK の WMI をブロックします。
- ブロックを登録します。
- WMI の登録情報を更新しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67ab688a5299ac20a91de68e450c80bf62322dde
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355278"
---
# <a name="updating-wmi-registration-information"></a>WMI 登録情報の更新





WMI での初期登録後、ドライバーは呼び出すことによってその登録情報を変更[ **IoWMIRegistrationControl** ](https://msdn.microsoft.com/library/windows/hardware/ff550480)次の操作のいずれかの。

-   WMIREG\_アクション\_置換した新しい情報で、ドライバーによって提供されるすべての登録情報を登録します。

    応答、WMI を送信するか、 [ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)要求または[ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734) 、ドライバーへの要求**Parameters.WMI.DataPath** WMIREGISTER に設定します。 (システムは Windows 98 および Windows 2000 で、送信、 **IRP\_MN\_REGINFO**要求。 Windows XP のシステムは、後で、送信と、 **IRP\_MN\_REGINFO\_EX**要求します)。

    ドライバーを提供 WMI 新しい登録情報でサポートされており、ブロックをすべての」の説明に従って[ブロックの登録に WMI ライブラリを使用して](using-the-wmi-library-to-register-blocks.md)と[IRP の処理\_MN\_REGINFO と IRP\_MN\_REGINFO\_ブロックを登録する例:](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)します。

-   WMIREG\_アクション\_UPDATE\_ブロックのサポートを追加または削除または登録済みのブロックの静的インスタンスの名前を変更する GUID。

    WMI では、応答、送信、 [ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)または[ **IRP\_MN\_REGINFO\_例** ](https://msdn.microsoft.com/library/windows/hardware/ff551734) 、ドライバーへの要求**Parameters.Wmi.DataPath** WMIUPDATE に設定します。

    ドライバー、更新された登録情報を WMI を指定します。

    -   ドライバー設定 WMIREG\_フラグ\_削除\_そのブロックのサポートを削除する GUID。

    -   WMIREG はクリアされます\_フラグ\_削除\_新しいブロックを追加または既存のブロックを更新する GUID。

    -   ドライバーを設定またはクリア WMIREG\_フラグ\_インスタンス\_*XXX*し、ブロックの静的インスタンスの名前を変更するか動的インスタンスを使用するように変更するために必要なインスタンス名情報を提供名前。

-   WMIREG\_アクション\_ドライバーでは、WMI 情報は提供されなくを WMI に指示する登録解除します。

    WMI は送信しません、 **IRP\_MN\_REGINFO**または**IRP\_MN\_REGINFO\_EX**のため、この呼び出しに応答を要求、ドライバーから詳細情報は必要ありません。 ドライバーの通常のブロックへの応答で登録を解除する[ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)要求。 デバイスへのすべての WMI Irp が完了するまで、登録解除呼び出しがブロックされるように注意してください。 ドライバーは、WMI の Irp をキューでの場合は、呼び出す前にキャンセルにする必要があります[ **IoWMIRegistrationControl** ](https://msdn.microsoft.com/library/windows/hardware/ff550480)の登録を解除します。

 

 




