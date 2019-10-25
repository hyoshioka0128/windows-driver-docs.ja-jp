---
title: WMI データ プロバイダーとしての登録
description: WMI データ プロバイダーとしての登録
ms.assetid: a08fed24-20b6-46aa-9a52-7a22f0e89ce4
keywords:
- WMI WDK カーネル、WMI への登録
- WMI データプロバイダーの登録
- データプロバイダー WDK WMI
- ドライバー登録 WDK WMI
- イベントブロック WDK WMI
- WDK WMI をブロックする
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f128523fc91a06c62d7f7159a8a66e879eeda642
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838467"
---
# <a name="registering-as-a-wmi-data-provider"></a>WMI データ プロバイダーとしての登録





Wmi をサポートするドライバーは、データおよびイベントブロックを wmi クライアントで使用できるようにするために、WMI データプロバイダーとして登録する必要があります。 ドライバーは通常、デバイスの起動時に WMI に登録されます。その後、ドライバーが WMI Irp を処理できるポイントにデバイスが初期化されます。 登録プロセス中に、ドライバーは、デバイスオブジェクトへのポインターと、サポートされているデータおよびイベントブロックに関する情報を WMI に渡します。

ドライバーは、次の2つのフェーズで WMI に登録します。

1.  ドライバーは[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出します。アクション\_\_アクションと、ドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンに渡されたデバイスオブジェクトへのポインターを呼び出します。

2.  ドライバーは、ドライバーの**Iowmiregistrationcontrol**呼び出しへの応答として WMI が送信する[ **\_reginfo**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[**irp\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)によって出力される irp\_を処理します。 IRP の**データパス**メンバーは、"wmi register" および "parameters" に設定されて**います。 wmi. ProviderId**は、ドライバーのデバイスオブジェクトポインターに設定されます。 このドライバーは、wmi ライブラリを使用して[ブロックを登録する](using-the-wmi-library-to-register-blocks.md)方法に関するページで説明されているように wmi ライブラリを使用するか、または**irp\_の\_Reginfo**または irp @no__ を処理することによって、データとイベントブロックに関する登録情報を wmi に提供します。「 [irp\_\_\_の処理](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)」で説明されているように\_の reginfo\_ex 要求を t_5_ しています。

 

 




