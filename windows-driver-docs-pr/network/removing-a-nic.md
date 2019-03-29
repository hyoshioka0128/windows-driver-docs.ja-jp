---
title: NIC の取り外し
description: NIC の取り外し
ms.assetid: eaa4b784-4375-465d-9ef5-99b38b7fd15a
keywords:
- WDK の Nic を削除するネットワークを
- ネットワーク インターフェイス カードの WDK ネットワーク, 削除
- プラグ アンド プレイ WDK NDIS ミニポート、NIC を削除します。
- Nic の WDK ネットワークを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3aaa2d3380026f1b1d21f258edc314eea9267f14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574706"
---
# <a name="removing-a-nic"></a>NIC の取り外し





次の手順では、NDIS が NIC の削除に参加する方法について説明します。

1.  PnP マネージャーの問題、 [ **IRP\_MN\_クエリ\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551705)中断することがなく、NIC を削除できるかどうかをクエリする要求、コンピューター。

2.  NDIS は、この IRP を受信、呼び出し、 [ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)ドライバー スタック内の NIC に関連付けられている最も低いフィルター ドライバーの機能です。 この呼び出しで NDIS 指定のイベント コード**NetEventQueryRemoveDevice**します。

    **注**  NDIS は、エントリをアドバタイズするフィルター ドライバーのためだけにこの手順を実行、 [ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)関数。 呼び出すときに、フィルター ドライバーはこのエントリ ポイントをアドバタイズし、 [ **NdisFRegisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562608)関数。

     

3.  呼び出しのコンテキスト内でその[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)関数、フィルター ドライバーを呼び出す必要があります[ **NdisFNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561828)を転送するには**NetEventQueryRemoveDevice**ドライバー スタックでは、次のフィルター ドライバーまでイベント。 これにより、NDIS フィルター ドライバーの呼び出しに*FilterNetPnPEvent*のイベント コードを使用して関数**NetEventQueryRemoveDevice**します。

    **注**  NDIS ドライバー スタックのエントリ ポイントを通知するには、次のフィルター ドライバーに対してのみこの手順を実行する、 [ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)関数。

     

4.  スタックの最上位フィルター ドライバーが転送されるまでドライバー スタック内の各フィルター ドライバーが、前の手順を繰り返し、 **NetEventQueryRemoveDevice**イベント。

    この場合、NDIS 呼び出し、 [ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263) NIC にバインドされているすべてのプロトコル ドライバーの機能 この呼び出しで NDIS 指定のイベント コード**NetEventQueryRemoveDevice**します。

5.  プロトコル ドライバーに失敗した場合、 **NetEventQueryRemoveDevice** NDIS エラー コードを返すことによってイベント\_状態\_からエラー *ProtocolNetPnPEvent*、NDIS または PnP マネージャーエラーを無視し、後から成功可能性があります、 [ **IRP\_MN\_クエリ\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551705)要求。 プロトコル ドライバーが失敗した場合でも、NIC の削除を処理するためにプロトコル ドライバーを準備する必要があります、そのため、 **NetEventQueryRemoveDevice**イベント。

6.  PnP マネージャーの問題、 [ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738) NIC または、ソフトウェア表現(デバイスオブジェクト、およびなど)を削除する要求[**IRP\_MN\_キャンセル\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff550823)削除保留中のキャンセルを要求します。 なお IRP\_MN\_削除\_デバイス要求は常に付いていない IRP\_MN\_クエリ\_削除\_デバイス要求。

7.  PnP マネージャー IRP が発行された場合\_MN\_キャンセル\_削除\_デバイス要求、NDIS 呼び出し、 [ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)最下位の関数ドライバー スタック内の NIC に関連付けられているフィルター ドライバー。 この呼び出しで NDIS 指定のイベント コード**NetEventCancelRemoveDevice**します。

    **注**  NDIS は、エントリをアドバタイズするフィルター ドライバーのためだけにこの手順を実行、 [ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)関数。

     

8.  呼び出しのコンテキスト内でその[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)関数、フィルター ドライバーを呼び出す必要があります[ **NdisFNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561828)を転送するには**NetEventCancelRemoveDevice**ドライバー スタックでは、次のフィルター ドライバーまでイベント。 これにより、NDIS フィルター ドライバーの呼び出しに*FilterNetPnPEvent*のイベント コードを使用して関数**NetEventCancelRemoveDevice**します。

    **注**  NDIS ドライバー スタックのエントリ ポイントを通知するには、次のフィルター ドライバーに対してのみこの手順を実行する、 [ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)関数。

     

9.  スタックの最上位フィルター ドライバーが転送されるまでドライバー スタック内の各フィルター ドライバーが、前の手順を繰り返し、 **NetEventCancelRemoveDevice**イベント。

    この場合、NDIS 呼び出し、 [ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263) NIC にバインドされているすべてのプロトコル ドライバーの機能 この呼び出しで NDIS 指定のイベント コード**NetEventCancelRemoveDevice**します。 このイベントのコードでは、削除のシーケンスを終了します。

10. PnP マネージャーが IRP を発行する場合\_MN\_削除\_デバイス要求と、NDIS は、次の手順を実行します。

    1.  NIC にバインドされているすべてのプロトコル ドライバーが一時停止します

    2.  NIC に関連付けられているすべてのフィルター ドライバーが一時停止します

    3.  NIC のミニポート ドライバーが一時停止します

    4.  呼び出す、 [ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278) NIC にバインドされているすべてのプロトコル ドライバーの機能

    5.  呼び出す、 [ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918) NIC に関連付けられているすべてのフィルター モジュールの関数

11. NDIS ミニポート ドライバーが正常に初期化すると、呼び出しますミニポート ドライバーの[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)関数。 NDIS セット、 *HaltAction*パラメーターの*MiniportHaltEx*に**NdisHaltDeviceDisabled**します。

12. NDIS 送信 IRP\_MN\_削除\_スタックの次のような低いデバイス オブジェクトへのデバイス要求。

13. NDIS が完了した IRP を受信すると\_MN\_削除\_NDIS 破棄 NIC 用に作成する機能のデバイス オブジェクト (FDO) スタックでは、[次へ] の下のデバイスからのデバイス要求オブジェクト

 

 





