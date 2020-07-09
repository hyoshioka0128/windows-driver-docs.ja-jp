---
title: IRP_MJ_SHUTDOWN (IFS)
description: IRP \_ MJ の \_ シャットダウン
ms.assetid: 4f7ba339-87f5-4011-8981-de6c31a9239a
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_SHUTDOWN
topic_type:
- apiref
api_name:
- IRP_MJ_SHUTDOWN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eff3c2715c08763e86c554e46fda4b46b667f80b
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141319"
---
# <a name="irp_mj_shutdown-ifs"></a>IRP \_ MJ \_ SHUTDOWN (IFS)


## <a name="when-sent"></a>送信時


IRP \_ MJ \_ SHUTDOWN 要求は、システムがシャットダウンされるときに、i/o マネージャーまたはファイルシステムドライバーによって送信されます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムは、必要なクリーンアップを実行し、状態が SUCCESS の IRP を完了する必要があり \_ ます。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、シャットダウン要求の処理中に、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp- &gt; iostatus*  
最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
IRP \_ MJ SET SHUTDOWN を指定し \_ \_ ます。

## <a name="see-also"></a>関連項目


[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ SHUTDOWN (WDK カーネルリファレンス)**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)

 

 






