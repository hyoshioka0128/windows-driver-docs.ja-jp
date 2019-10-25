---
title: 電源管理に関するデバイス オブジェクト フラグの設定
description: 電源管理に関するデバイス オブジェクト フラグの設定
ms.assetid: 58d1a3a2-c8ea-446c-b1d6-ed00411d1d75
keywords:
- DO_POWER_PAGABLE
- DO_POWER_INRUSH
- デバイスオブジェクトフラグ WDK 電源管理
- オブジェクトフラグ WDK 電源管理
- WDK 電源管理にフラグをかける
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8424b17f14cb3cf878ebd47b958d9fa445f72c23
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836359"
---
# <a name="setting-device-object-flags-for-power-management"></a>電源管理に関するデバイス オブジェクト フラグの設定





[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンでは、各ドライバーがデバイスオブジェクト (フィルターデバイスオブジェクト (DO)、機能デバイスオブジェクト (FDO)、または物理デバイスオブジェクト (PDO)) を作成し、デバイスの属性を記述するためにデバイスオブジェクトの DO\_*XXX*フラグを設定します。およびドライバーの構成。 次のデバイスオブジェクトフラグは、電源管理に関連しています。

| Flag               | 説明                                                                                                                                                                                                                                                                                                |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \_POWER\_突入電流  | デバイスが初めてオンになったときに、デバイスによって描画された現在のが増加していることを示します。 このようなサージや "突入電流" は、しばらくの間、デバイスによって描画される現在のが低い動作レベルになるまで継続します。                                                                                   |
| 電源\_PAGABLE を\_ | ドライバーがページング可能であることを示します。 Windows 2000 以降では、ページングできるドライバーは、DO\_POWER\_PAGABLE フラグを設定する必要があります。 電源マネージャーは、IRQL = パッシブ\_レベルでこのようなドライバーを呼び出します。 ページング可能なドライバーの詳細については、「[ドライバーのページングの作成](making-drivers-pageable.md)」を参照してください。 |

 

デバイスオブジェクトフラグは、通常、デバイスの PDO を作成するときにバスドライバーによって設定されます。 ただし、一部の関数ドライバーでは、 *AddDevice*ルーチンの一部としてこれらのフラグの値を変更する必要がある場合があります。 Windows Vista 以降のオペレーティングシステムでは、デバイススタック内のすべてのデバイスオブジェクトに同じ電源関連フラグが設定されている必要はありません。 ただし、Windows Server 2003、Windows XP、および Windows 2000 では、デバイススタック内のすべてのデバイスオブジェクトに同じ電源関連フラグが設定されている必要があります。

Windows 2000 以降では、ページングパスにあるデバイスのドライバーは、DO\_POWER\_PAGABLE フラグを設定することはできません。 ページングファイルに i/o 操作が含まれている場合、ドライバーは "ページングパス" にあります。 このフラグが設定されていないドライバーは、IRQL = ディスパッチ\_レベルで呼び出す必要があります。 詳細については、「[ディスパッチルーチンの制約](https://docs.microsoft.com/windows-hardware/drivers/ifs/constraints-on-dispatch-routines)」を参照してください。

一般に、ドライバーは、DO\_POWER\_PAGABLE フラグのバスドライバーの値を変更しないようにする必要があります。下位レベルのドライバーによって消去された場合、ドライバーはこのフラグを設定しないようにする必要があります。 [Pnp ページング要求](https://docs.microsoft.com/windows-hardware/drivers/storage/handling-pnp-paging-requests)に関係する遷移を処理するとき (通常は、 [**irp\_MJ\_pnp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)に応答し[ **\_\_て、デバイス\_\_の使用状況通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)要求) が発生した場合は、ストレージドライバーを使用する必要があります。フラグの設定とクリアを注意深くシーケンス処理します。

起動時に突入電流電源が必要なデバイスのドライバーでは、デバイスオブジェクトの DO\_POWER\_突入電流フラグを設定してから、デバイスの\_を実行する\_初期化フラグをオフにする必要があります。 デバイススタック内の1つのドライバー (通常はバスドライバー (PDO)) では、デバイスの DO\_POWER\_突入電流フラグを設定する必要があります。 フラグは、電源装置の過負荷を避けるために、このようなデバイスの電源を一度に1つずつ電源オンにする必要があることを電源マネージャーに通知します。 電源マネージャーを使うと、特定の時点で、システム内の任意の場所で1つの電源突入電流 IRP だけがアクティブになります。

Windows Vista 以降のドライバーでは、DO\_POWER\_PAGABLE フラグと DO\_POWER\_突入電流フラグの両方を設定できます。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーは DO\_POWER\_PAGABLE フラグと DO\_電源\_突入電流フラグの両方を設定することはできません。

 

 




