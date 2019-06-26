---
title: IRP_MJ_SHUTDOWN
description: IRP\_MJ\_シャット ダウン
ms.assetid: 4f7ba339-87f5-4011-8981-de6c31a9239a
keywords:
- IRP_MJ_SHUTDOWN インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_SHUTDOWN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8bccfeedc684e610d017d3660d2caa72d8db6a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375676"
---
# <a name="irpmjshutdown"></a>IRP\_MJ\_シャット ダウン


## <a name="when-sent"></a>送信時


IRP\_MJ\_シャット ダウン要求は I/O マネージャーによって、またはファイル システム ドライバーによって、システムがシャット ダウンされるときに、送信されます。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システムが、必要なクリーンアップを実行する必要があり、ステータスの IRP の完了\_成功します。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の IRP スタックの場所をシャット ダウン要求の処理では、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_設定\_シャット ダウンします。

## <a name="see-also"></a>関連項目


[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_シャット ダウン (WDK カーネル リファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)

 

 






