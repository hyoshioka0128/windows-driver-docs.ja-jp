---
title: DispatchPnP ルーチン
description: DispatchPnP ルーチン
ms.assetid: 909d99ac-5bd3-4b12-bfb4-79713cf2a156
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchPnP ルーチン
- DispatchPnP ルーチン
- PnP ディスパッチ ルーチン WDK カーネル
- Irp WDK カーネルでは、プラグ アンド プレイ ディスパッチ ルーチン
- プラグ アンド プレイ ディスパッチ ルーチン WDK カーネル
- IRP_MJ_PNP I/O 関数のコード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8edb3ced028b893484c95d4b2f90f74f5aa7e46e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376462"
---
# <a name="dispatchpnp-routines"></a>DispatchPnP ルーチン





ドライバーの[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)日常的なサポート[プラグ アンド プレイ](implementing-plug-and-play.md)の Irp を処理することによって、 [ **IRP\_MJ\_PNP** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp) I/O 関数のコード。 関連付けられている、 **IRP\_MJ\_PNP**関数コードがいくつかの小さな I/O 機能コード (を参照してください[プラグ アンド プレイ マイナー Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)) によって、処理する必要のあるすべてのドライバーといくつかのこのオプションで処理できます。 PnP マネージャーでは、これらのマイナー関数コードについては、自分のデバイス ドライバーをクエリに直接ドライバーを開始、停止、およびデバイスを削除するには使用します。

デバイスのすべてのドライバーには、いくつかの場合、関数またはフィルター ドライバーの IRP の失敗が許可される場所を除く、デバイスの PnP Irp を処理する必要があります。

各ドライバーの*DispatchPnP*ルーチンがこれらの規則に従う必要があります。

-   関数またはフィルター ドライバーは、関数またはフィルター ドライバーは IRP を処理し、(たとえばが不足しているリソース) が原因のエラーが発生しない限り、デバイス スタックでは、次のドライバーに PnP Irp を渡す必要があります。

    デバイスのすべてのドライバーには、ドライバーのいずれかのエラーが発生した場合を除き、デバイスの PnP Irp を処理する必要があります。 PnP マネージャーでは、デバイス スタックの最上位のドライバーを Irp を送信します。 関数とフィルター ドライバーは、次のドライバーに IRP を渡すし、親のバス ドライバーが IRP を完了するとします。 参照してください[、デバイス スタックの PnP Irp の渡す](passing-pnp-irps-down-the-device-stack.md)詳細についてはします。

    IRP の処理を試行し、(リソースの不足) など、エラーが発生した場合は、ドライバーは IRP をフェールバックできます。 ドライバーは、ハンドルされないコード IRP を受信する場合、ドライバーにする必要があります、IRP 失敗しません。 IRP の状態を変更することがなく、次のドライバーに、このような IRP を渡す必要があります。

-   ドライバーは、特定 PnP Irp を処理する必要があり、必要に応じて、他のユーザー処理場合があります。

    各 PnP ドライバーが特定の Irp の処理に必要な[ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)で、必要に応じて他のユーザーを処理できます。 参照してください[プラグ アンド プレイ マイナー Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)について Irp は必須およびオプション (関数ドライバー、フィルター ドライバー、バス ドライバー) ドライバーの種類ごとにします。

    ドライバーは、該当するエラー状態と必要な PnP IRP をフェールオーバーできますが、ドライバーでは状態を返す必要がありますいない\_いない\_このような IRP のサポートされています。

-   ドライバーでは、PnP IRP が正常に処理する場合、ドライバーは IRP の状態を成功に設定します。 状態を設定するスタック内の別のドライバーでは依存しません。

    ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_PnP マネージャー、ドライバーが IRP を正常に処理することを通知するために成功します。 一部の Irp の非バス ドライバーは、状態を成功に設定をその親バス ドライバーに依存することにあります。 ただし、これは、リスクの高い方法です。 整合性と堅牢性は、ドライバーする必要があります IRP の状態を成功に設定の各 PnP IRP が正常に処理します。

-   IRP がドライバーに失敗した場合、ドライバーは IRP がエラー状態を完了し、[次へ] のドライバーに IRP を渡しません。

    ような IRP が失敗する[ **IRP\_MN\_クエリ\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)、ドライバーの設定**Irp-&gt;IoStatus.Status**ステータス\_失敗しました。 その他の Irp の追加のエラー状態の値は、状態を含める\_不十分\_リソースと状態\_無効な\_デバイス\_状態。

    ドライバーは、状態を設定しないでください\_いない\_Irp の処理をサポートします。 これは、初期状態の PnP マネージャーで設定します。 IRP は、この状態で完了しましたが、場合、スタック内のドライバーでは IRP; は処理されません。すべてのドライバーには、次のドライバーに IRP が渡されるだけです。

-   ドライバーで (IRP の途中でデバイス スタック)、そのディスパッチ ルーチンでの PnP IRP を処理する必要があります、 [ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン (上、IRP のデバイス stack のバックアップ方法)、またはその両方の参照で指定されています。IRP のページです。

    Irp をなど、いくつか PnP [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)、まずデバイス スタックの上部にあるドライバーをそれぞれ次の下位ドライバーによってし処理する必要があります。 他のユーザーなど[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)、親バス ドライバーによって最初に処理する必要があります。 まだ他など[ **IRP\_MN\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)、バックアップや、デバイス スタックする方法の両方を処理できます。 参照してください[プラグ アンド プレイ マイナー Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)の各 PnP IRP に適用される規則です。 参照してください[を延期する PnP IRP の処理まで低いドライバー完了](postponing-pnp-irp-processing-until-lower-drivers-finish.md)親バス ドライバーによって最初に処理する必要がありますが、PnP Irp の処理についてはします。

-   ドライバーでは、デバイス スタック IRP の方法で IRP に情報を追加、変更しまたはバックアップ IRP の方法で情報を削除する必要があります。

    IRP の PnP クエリに対する応答の情報を返すときに、ドライバーは計画的な情報をデバイスの階層化ドライバーによって渡すを有効にするには、この規則に従う必要があります。

-   ドライバーに依存できませんが、明確に文書化、点を除いては、特定の順序で送信 PnP Irp されています。

-   ドライバーは、PnP IRP を送信するときは、IRP をデバイス スタックの最上位のドライバーに送信する必要があります。

    PnP Irp のほとんどは、PnP マネージャーによって送信されますが、ドライバーによっていくつか送信することができます (たとえば、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface))。 ドライバーは、デバイス スタックの上部にあるドライバーに PnP IRP を送信する必要があります。 呼び出す[ **IoGetAttachedDeviceReference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetattacheddevicereference)デバイス スタックの上部にある、ドライバーのデバイス オブジェクトにポインターを取得します。

オペレーティング システムのチェック ビルドと、ドライバーをテストする必要があります。 システムのチェック ビルドは、上に示した PnP ルールがたくさんドライバーに依存するかどうかを確認します。

 

 




