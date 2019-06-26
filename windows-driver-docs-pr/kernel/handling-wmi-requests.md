---
title: WMI 要求の処理
description: WMI 要求の処理
ms.assetid: d95b736c-045d-4888-8bab-b0a6201f8830
keywords:
- WMI の WDK カーネルでは、要求
- WDK の WMI の要求
- Irp WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 753875dc7ea41999a30c83daeccb8e2122f258b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371891"
---
# <a name="handling-wmi-requests"></a>WMI 要求の処理





すべてのドライバーのディスパッチ テーブル エントリ ポイントを設定する必要があります、 [ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) WMI 要求を処理するルーチン。 場合、ドライバー [WMI データ プロバイダーとして登録](registering-as-a-wmi-data-provider.md)WMI のすべての要求を処理する必要があります。 それ以外の場合、ドライバーでは、[次へ] の下位のドライバーをすべての WMI 要求を転送する必要があります。

主要なコードであるすべての WMI Irp [ **IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)と次の小さなコードの 1 つ。

-   [**IRP\_MN\_REGINFO**](irp-mn-reginfo.md)、 [ **IRP\_MN\_REGINFO\_EX**](irp-mn-reginfo-ex.md): クエリまたはドライバーの更新ドライバーが呼び出された後に、登録情報[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)します。

-   [**IRP\_MN\_クエリ\_すべて\_データ**](irp-mn-query-all-data.md)、 [ **IRP\_MN\_クエリ\_単一\_インスタンス**](irp-mn-query-single-instance.md)-すべてのインスタンスまたは指定されたデータ ブロックの 1 つのインスタンスに対してクエリします。

-   [**IRP\_MN\_変更\_単一\_項目**](irp-mn-change-single-item.md)、 [ **IRP\_MN\_変更\_単一\_インスタンス**](irp-mn-change-single-instance.md)— 1 つの項目またはデータ ブロックのインスタンスの複数の項目を変更するドライバーを要求します。

-   [**IRP\_MN\_を有効にする\_コレクション**](irp-mn-enable-collection.md)、 [ **IRP\_MN\_を無効にする\_コレクション**](irp-mn-disable-collection.md)— データを収集するか、このようなブロックのデータの蓄積を停止する高価なとしてドライバーが登録されているブロック用の累積を開始するドライバーを要求します。

-   [**IRP\_MN\_を有効にする\_イベント**](irp-mn-enable-events.md)、 [ **IRP\_MN\_を無効にする\_イベント**](irp-mn-disable-events.md)有効な場合、イベントが発生した場合、指定されたイベントの通知の送信を開始するか、このようなイベントの通知の送信を停止、ドライバーを要求します。

-   [**IRP\_MN\_EXECUTE\_メソッド**](irp-mn-execute-method.md)— データ ブロックに関連付けられているメソッドの実行にドライバーを要求します。

WMI のカーネル モード コンポーネント送信 WMI Irp いつを以下に、ドライバーの登録に成功した WMI データ プロバイダーは、通常ユーザー モードのデータ コンシューマーには、ドライバーのデバイスの WMI 情報が要求されました。 かどうか、ドライバーが呼び出すことによって WMI データ プロバイダーとして登録します[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)、次の方法のいずれかで後続の WMI 要求を処理にする必要があります。

-   カーネル モードの WMI ライブラリ ルーチンを呼び出す**WmiSystemControl** PDO の。 詳細については、次を参照してください。 [WMI Irp の処理を呼び出す WmiSystemControl](calling-wmisystemcontrol-to-handle-wmi-irps.md)します。

-   その[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンが処理し、そのドライバーが呼び出しで渡されるデバイス オブジェクトへのポインターでタグ付けされた該当する要求を完了**IoWMIRegistrationControl**、およびその他の転送[ **IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control) [次へ] の下のドライバーに要求します。 詳細については、次を参照してください。 [DispatchSystemControl ルーチンで WMI Irp の処理](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)します。

WMI のマイナー Irp の一覧は、次を参照してください。 [WMI マイナー Irp](wmi-minor-irps.md)します。 

 




