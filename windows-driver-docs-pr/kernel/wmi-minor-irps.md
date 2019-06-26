---
title: WMI のマイナー IRP
description: WMI のマイナー IRP
ms.date: 08/12/2017
ms.assetid: 5788294f-2145-4381-9b06-3b138b2d26df
ms.localizationpriority: medium
ms.openlocfilehash: d48d8b56fb1bd07a33eadb22b3847c7a9ff51936
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353787"
---
# <a name="wmi-minor-irps"></a>WMI のマイナー IRP





このセクションについて説明します、 [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) Irp WDM に WMI の拡張機能の一部であります。 メジャーは、コードのすべての WMI Irp 使用[ **IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)と軽微なコードが特定の WMI 要求を示します。 WMI のカーネル モード コンポーネント Irp を送信する WMI いずれかの WMI データの供給業者として次のドライバーの登録に成功した時刻。 WMI の Irp 通常送信ユーザー モードのデータ コンシューマーが WMI データを要求されたときにします。

すべてのドライバーのディスパッチ テーブル エントリ ポイントを設定する必要があります、 [ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) WMI 要求を処理するルーチン。

呼び出すことによって、そのドライバーが WMI データ プロバイダーとして登録するかどうか[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)で説明する手法のいずれかを使用して WMI Irp を処理する必要があります[WMI の要求を処理する](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests).

WMI データ プロバイダーとして登録されていないドライバーは、次の下位ドライバーへのすべての WMI 要求を転送する必要があります。

このセクションでは、次のシステム定義 WMI マイナー機能コードについて説明します。

[**IRP\_MN\_変更\_単一\_インスタンス**](irp-mn-change-single-instance.md)

[**IRP\_MN\_変更\_単一\_項目**](irp-mn-change-single-item.md)

[**IRP\_MN\_DISABLE\_COLLECTION**](irp-mn-disable-collection.md)

[**IRP\_MN\_を無効にする\_イベント**](irp-mn-disable-events.md)

[**IRP\_MN\_ENABLE\_COLLECTION**](irp-mn-enable-collection.md)

[**IRP\_MN\_を有効にする\_イベント**](irp-mn-enable-events.md)

[**IRP\_MN\_EXECUTE\_メソッド**](irp-mn-execute-method.md)

[**IRP\_MN\_クエリ\_すべて\_データ**](irp-mn-query-all-data.md)

[**IRP\_MN\_クエリ\_単一\_インスタンス**](irp-mn-query-single-instance.md)

[**IRP\_MN\_REGINFO**](irp-mn-reginfo.md)

[**IRP\_MN\_REGINFO\_EX**](irp-mn-reginfo-ex.md)

ドライバーは IRP を他の IRP マイナー関数コードを格納している場合、次の下位のドライバーに IRP を転送します。

 

 




