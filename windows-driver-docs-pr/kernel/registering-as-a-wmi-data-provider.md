---
title: WMI データ プロバイダーとしての登録
description: WMI データ プロバイダーとしての登録
ms.assetid: a08fed24-20b6-46aa-9a52-7a22f0e89ce4
keywords:
- WMI の WDK カーネルでは、WMI に登録します。
- WMI データ プロバイダーを登録します。
- WDK の WMI のデータ プロバイダー
- ドライバー WDK WMI の登録
- イベントは、WDK の WMI をブロックします。
- WDK の WMI をブロックします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e8f5a25e1df4d68e3d94907111e327dbafeeb7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373472"
---
# <a name="registering-as-a-wmi-data-provider"></a>WMI データ プロバイダーとしての登録





WMI をサポートしているドライバーは、データとイベント ブロックを使用できるように WMI クライアント WMI データ プロバイダーとして登録する必要があります。 ドライバーは、デバイス ドライバーが Irp の WMI を処理できるポイントに初期化された後、そのデバイスを開始するときに通常、WMI で登録します。 登録プロセス中にドライバー WMI にポインターを渡しますサポート データとイベントのブロックについては、デバイス オブジェクト。

ドライバーは、2 つのフェーズでは、WMI で登録します。

1.  ドライバー呼び出し[ **IoWMIRegistrationControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)アクション WMIREG\_アクション\_ドライバーに登録して、デバイス オブジェクトへのポインターが渡される[*AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。

2.  ドライバーのハンドル、 [ **IRP\_MN\_REGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[ **IRP\_MN\_REGINFO\_例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex) WMI は、ドライバーへの応答で送信する要求の**IoWMIRegistrationControl**呼び出します。 **Parameters.WMI.DataPath** WMIREGISTER に IRP のメンバーが設定されていると**Parameters.WMI.ProviderId**ドライバーのデバイス オブジェクトのポインターに設定されます。 ドライバーで、」の説明に従って、WMI のライブラリを使用して、いずれかのデータおよびイベント ブロックに関する登録情報を WMI を提供する[ブロックの登録に WMI ライブラリを使用して](using-the-wmi-library-to-register-blocks.md)、または処理することによって、 **IRP\_MN\_REGINFO**または**IRP\_MN\_REGINFO\_EX** 」の説明に従って要求[IRP の処理\_MN\_REGINFO と IRP\_MN\_REGINFO\_ブロックを登録する例:](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)します。

 

 




