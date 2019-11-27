---
title: IRP_MN_STOP_DEVICE 要求の処理 (Windows 2000 以降)
description: IRP_MN_STOP_DEVICE 要求の処理 (Windows 2000 以降)
ms.assetid: 5e91748c-d03a-48f7-a9cc-df2801d8a555
keywords:
- IRP_MN_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6f992c337719cefb3229e43f8224f83e06b0a82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836591"
---
# <a name="handling-an-irp_mn_stop_device-request-windows-2000-and-later"></a>IRP\_の処理\_\_デバイスの要求の停止 (Windows 2000 以降)





[ **\_デバイス要求\_停止する IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)は、デバイススタックの上位のドライバーによって最初に処理され、次に下位のドライバーごとに処理されます。 ドライバーは、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで停止 irp を処理します。

ドライバーは、次のような手順を使用して、 **\_デバイスの要求\_停止する IRP\_** を処理します。

1.  デバイスが一時停止されていることを確認します。

    IRP\_に応答してデバイスを完全に一時停止しなかった場合は[ **\_クエリ\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)の要求を停止します。 デバイス拡張機能で HOLD\_NEW\_REQUESTS フラグを設定し、デバイスを一時停止するために必要なその他の操作を実行します。

    デバイスのリソース再調整操作中に電力が失われる可能性があるため、デバイスの状態が失われる可能性があります。 デバイスのドライバーは、デバイスの状態に関する情報を保存し、後続の IRP\_を受信したときにその情報を復元して[ **\_デバイスの要求\_開始**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)する必要があります。

2.  デバイスのハードウェアリソースを解放します。

    関数ドライバーでは、正確な操作はデバイスとドライバーによって異なりますが、割り込みの切断、 [**io切った割り込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)の切断、 [**Mmunmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)を使用した物理アドレス範囲の解放、i/o ポートの解放などを行うことができます。

    フィルターまたはバスドライバーによってデバイスのハードウェアリソースが取得された場合、そのドライバーは IRP\_に応答してリソースを解放し、 **\_デバイスの要求\_停止**する必要があります。

3.  **Irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

4.  IRP を次の下位のドライバーに渡すか、または IRP を完了します。

    -   関数またはフィルタードライバーで、次のスタックの場所を[**IoskipIoCallDriver Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で設定します。次に、IRP を[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して次の下位のドライバーに渡し、 **IoCallDriver**から状態を*DispatchPnP*ルーチンからのリターンステータスとして返します。 IRP を完了しないでください。

    -   バスドライバーでは、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を使用して IRP を完了します。 IO\_は\_インクリメントを行わず、 *DispatchPnP*ルーチンからを返します。

デバイスがリソースの再調整を停止している間、デバイスにアクセスする Irp を開始することはできません。 ドライバーは、[デバイスが一時停止したときの受信 irp の保持](holding-incoming-irps-when-a-device-is-paused.md)に関するページで説明されているように、このような irp をキューに格納する必要があります。また、ドライバーが IRP を保持するキューを実装しておらず、i/o 要求を削除してはいけない場合は失敗します。

 

 




