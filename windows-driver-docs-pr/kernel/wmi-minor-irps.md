---
title: WMI のマイナー IRP
description: WMI のマイナー IRP
ms.date: 08/12/2017
ms.assetid: 5788294f-2145-4381-9b06-3b138b2d26df
ms.localizationpriority: medium
ms.openlocfilehash: abe1f2e0dd4c93a96e204c81b44662afb9876539
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838303"
---
# <a name="wmi-minor-irps"></a>WMI のマイナー IRP





このセクションでは、WDM の WMI 拡張機能の一部である[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)の irp について説明します。 すべての WMI Irp は、主要なコード[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)、および特定の wmi 要求を示すマイナーコードを使用します。 Wmi カーネルモードコンポーネントは、wmi データの供給元としてドライバーが正常に登録された後、いつでも WMI Irp を送信できます。 通常、WMI Irp は、ユーザーモードデータコンシューマーが WMI データを要求したときに送信されます。

すべてのドライバーで、 [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが WMI 要求を処理するためのディスパッチテーブルのエントリポイントを設定する必要があります。

ドライバーが[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出して wmi データプロバイダーとして登録する場合は、「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」で説明されているいずれかの方法を使用して wmi irp を処理する必要があります。

WMI データプロバイダーとして登録されていないドライバーは、すべての WMI 要求を次の下位のドライバーに転送する必要があります。

このセクションでは、次のシステム定義の WMI マイナー関数コードについて説明します。

[**IRP\_\_1 つの\_インスタンス\_変更**](irp-mn-change-single-instance.md)

[**IRP\_\_1 つの\_項目\_変更**](irp-mn-change-single-item.md)

[**IRP\_\_\_コレクションを無効にする**](irp-mn-disable-collection.md)

[**IRP\_\_\_イベントを無効にする**](irp-mn-disable-events.md)

[**IRP\_\_\_コレクションを有効にする**](irp-mn-enable-collection.md)

[**IRP\_\_\_イベントを有効にする**](irp-mn-enable-events.md)

[**IRP\_\_メソッドを実行\_** ](irp-mn-execute-method.md)

[**IRP\_\_クエリ\_すべての\_データ**](irp-mn-query-all-data.md)

[**IRP\_\_クエリ\_単一\_インスタンス**](irp-mn-query-single-instance.md)

[**IRP\_\_REGINFO**](irp-mn-reginfo.md)

[**IRP\_\_REGINFO\_EX**](irp-mn-reginfo-ex.md)

ドライバーが、他の IRP マイナー関数コードを含む IRP を受信した場合、irp を次の下位のドライバーに転送する必要があります。

 

 




