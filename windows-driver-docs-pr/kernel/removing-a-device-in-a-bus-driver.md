---
title: バス ドライバーでのデバイスの削除
description: バス ドライバーでのデバイスの削除
ms.assetid: f3961c29-02e1-41f0-bb7f-784bcdb57eb0
keywords:
- バス ドライバー WDK PnP
- DispatchPnP ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d5de3fb21e9cd6540961fb15926cbbaab626247
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579770"
---
# <a name="removing-a-device-in-a-bus-driver"></a>バス ドライバーでのデバイスの削除





親のバス ドライバーのすべての操作を取り消す必要があります (子 PDO) の子のデバイスを削除するときにその解析が実行を追加して、デバイスを起動します。

バス ドライバーは、次のようなプロシージャを使って子デバイスを削除します。 その[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

1.  ドライバーを処理する前[ **IRP\_MN\_突然\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)この PDO を要求しますか?

    そうである場合、残りのクリーンアップを実行し、手順 4 に進みます。

    通常、ドライバーは、ドライバーが処理されるかどうかを示すデバイス拡張機能のフラグ、 **IRP\_MN\_突然\_削除**デバイスの要求。

2.  ドライバーでキューにすべての要求を完了します。

3.  バス ドライバーでは、これを行う場合、デバイスからの電源を削除し、呼び出すことによって電源マネージャーに通知[ **PoSetPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff559765)します。

    バス ドライバー子デバイス電源可能であれば、およびデバイスの電源状態の変更の電源マネージャーに通知します。 バス ドライバーへの応答では、 [ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)要求は、デバイスの電源ポリシー所有者は送信しません、 [**IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)デバイスが削除されるときに要求します。 詳細については、次を参照してください。[電源管理](implementing-power-management.md)します。

4.  バス ドライバーへの応答に、最新では、このデバイスが報告されたかどうか、 [ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://msdn.microsoft.com/library/windows/hardware/ff551670) の要求**BusRelations**デバイスがコンピューターにまだ物理的に存在します。 この場合は、バス ドライバー。

    -   デバイスが物理的に削除されるまでは、デバイスの PDO を保持します。

    -   セット**Irp -&gt;IoStatus.Status**ステータス\_成功します。

    -   IRP の完了[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)します。

    -   返されます、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

    バス ドライバーは、後続の列挙型では、このデバイスを報告し続ける必要があります (**IRP\_MN\_クエリ\_デバイス\_リレーション**の**BusRelations**) デバイスが物理的に削除されるまでです。 PnP マネージャー、列挙されたデバイスを追加し、開始するかどうかの追跡。

5.  デバイスが、バス ドライバーの最新の応答に含まれていない場合、 **IRP\_MN\_クエリ\_デバイス\_リレーション**要求**BusRelations**、バス ドライバーがコンピューターから物理的に削除するデバイスと見なします。 この場合は、バス ドライバーは、次を行います。

    -   デバイスに固有の割り当て、メモリ、イベント、およびなどをクリーンアップします。

    -   セット**Irp -&gt;IoStatus.Status**ステータス\_成功します。

    -   IRP の完了[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)します。

    -   PDO を解放[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)します。

        バス ドライバーは、ドライバー、最新のデバイスを省略した場合、PDO を削除する必要があります**BusRelations**一覧。 ユーザー接続されている場合、デバイス、マシンにもう一度、バス ドライバーがへの応答で新しい PDO を作成する必要があります**BusRelations**クエリ。 バス ドライバーは、デバイスの新しいインスタンスを同じ PDO を再利用、コンピューターは正しく動作しません。

    -   返されます、 *DispatchPnP*ルーチン。

デバイスがまだ存在する場合、PnP マネージャーが送信する場合、 **IRP\_MN\_削除\_デバイス**要求、バス ドライバーの PDO を保持します。 その後は、バスからデバイスが物理的に削除場合、PnP マネージャーに送信別**IRP\_MN\_削除\_デバイス**します。 IRP の後続の削除の受信、時に、バス ドライバーは、デバイスの PDO を削除します。

バス ドライバーが処理できる必要があります、 **IRP\_MN\_削除\_デバイス**デバイスが既に削除し、持つ PDO は削除対象としてマークします。 このような IRP への応答、バス ドライバーは IRP を成功または、状態を返す\_いいえ\_かかる\_デバイス。 デバイスの PDO がまだ削除されていないこの場合は、バス ドライバーの以前の呼び出しに関係なく**IoDeleteDevice**いくつかのコンポーネントは、オブジェクトへの参照をしているため、します。 そのため、バス ドライバーは IRP の 2 つ目の削除を処理中に、PDO をアクセスできます。 バス ドライバーを呼び出してはならない**IoDeleteDevice**をもう一度 PDO; の I/O システム削除 PDO 参照カウントがゼロになったときにします。

受信するまでに、バス ドライバーが子デバイスの場合は、そのデータ構造を削除できません、 **IRP\_MN\_削除\_デバイス**デバイスの要求。 バス ドライバーは、デバイスが削除され、呼び出すことを検出可能性も[ **IoInvalidateDeviceRelations**](https://msdn.microsoft.com/library/windows/hardware/ff549353)、PnP マネージャーに送信するまで、デバイスの PDO は削除する必要がありますが、 **IRP\_MN\_削除\_デバイス**要求。

 

 




