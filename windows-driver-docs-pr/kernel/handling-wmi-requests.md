---
title: WMI 要求の処理
description: WMI 要求の処理
ms.assetid: d95b736c-045d-4888-8bab-b0a6201f8830
keywords:
- WMI WDK カーネル、要求
- WDK WMI を要求する
- Irp WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fd1080ce6c5df2a2abb6ba99e4290b0bf192f29
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838652"
---
# <a name="handling-wmi-requests"></a>WMI 要求の処理





すべてのドライバーで、 [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが WMI 要求を処理するためのディスパッチテーブルのエントリポイントを設定する必要があります。 ドライバーが[wmi データプロバイダーとして登録](registering-as-a-wmi-data-provider.md)されている場合は、すべての wmi 要求を処理する必要があります。 それ以外の場合、ドライバーは、すべての WMI 要求を次の下位ドライバーに転送する必要があります。

すべての WMI Irp には、 [**MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)の主要なコード irp\_、次のいずれかのマイナーコードがあります。

-   [**Irp\_** ](irp-mn-reginfo.md)は、ドライバーが[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出した後に、ドライバーの登録情報を照会または更新します。 reginfo、 [**irp\_\_\_** ](irp-mn-reginfo-ex.md)は、\_になります。

-   [**Irp\_\_クエリ\_すべての\_データ**](irp-mn-query-all-data.md)、IRP\_すべての\_の[**クエリ\_単一の\_インスタンス**](irp-mn-query-single-instance.md)(特定のデータブロックのすべてのインスタンスまたは1つのインスタンスに対するクエリ)。

-   [**Irp\_\_変更\_1 つの\_項目**](irp-mn-change-single-item.md)、 [**irp\_\_1 つの単一\_インスタンス**](irp-mn-change-single-instance.md)の変更\_、1つの項目またはデータブロックのインスタンス内の複数の項目を変更するようにドライバーに要求します。

-   [**Irp\_\_有効にすると、\_collection**](irp-mn-enable-collection.md)、 [**IRP\_\_コレクションの無効化\_収集**](irp-mn-disable-collection.md)を有効にします。ドライバーが収集にかかるコストとして登録されたブロックのデータの累積を開始するようにドライバーに要求するか、または停止します。このようなブロックのデータを累積しています。

-   [**Irp\_\_有効にすると、\_イベントを有効に**](irp-mn-enable-events.md)し、 [**irp\_、\_イベントの無効化**](irp-mn-disable-events.md)を有効にします。イベントが有効になっている場合、または通知の送信を停止する場合は、特定のイベントの通知の送信を開始するようドライバーに要求します。このようなイベントの。

-   [**IRP\_\_実行\_メソッド**](irp-mn-execute-method.md): データブロックに関連付けられているメソッドを実行するようにドライバーに要求します。

Wmi カーネルモードコンポーネントは、ドライバーが正常に登録されたことを示す wmi データプロバイダーとして、通常、ユーザーモードデータコンシューマーがドライバーのデバイスの WMI 情報を要求したときに、WMI Irp を送信します。 ドライバーが[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出して wmi データプロバイダーとして登録する場合は、次のいずれかの方法で、後続の各 wmi 要求を処理する必要があります。

-   PDO のカーネルモード WMI ライブラリルーチンの呼び出し**システムコントロール**を呼び出します。 詳細については、「 [WMI irp を処理するための呼び出しの呼び出し](calling-wmisystemcontrol-to-handle-wmi-irps.md)」を参照してください。

-   [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで、デバイスオブジェクトへのポインターでタグ付けされた要求を処理して完了します。これにより、ドライバーは**Iowmiregistrationcontrol**への呼び出しで渡され、他の[**IRP\_MJ\_システムに転送されます。** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)次に低いドライバーに要求を制御\_ます。 詳細については、「 [DispatchSystemControl ルーチンでの WMI irp の処理](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)」を参照してください。

WMI の軽微な Irp の一覧については、「 [Wmi Minor irp](wmi-minor-irps.md)」を参照してください。 

 




