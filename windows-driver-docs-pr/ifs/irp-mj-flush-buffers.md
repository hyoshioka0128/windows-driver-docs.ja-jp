---
title: IRP_MJ_FLUSH_BUFFERS
description: IRP\_MJ\_フラッシュ\_バッファー
ms.assetid: 13df0d84-0320-4d7e-9acc-8f913ba6afaa
keywords:
- IRP_MJ_FLUSH_BUFFERS インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_FLUSH_BUFFERS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd3d4271feb6129dd828ed496ece9245d1709e8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384829"
---
# <a name="irpmjflushbuffers"></a>IRP\_MJ\_フラッシュ\_バッファー


## <a name="when-sent"></a>送信時


IRP\_MJ\_フラッシュ\_バッファー要求を送信 I/O マネージャーとその他のオペレーティング システムのコンポーネントに加えてその他のカーネル モード ドライバーでは、バッファー内のデータをフラッシュする必要がある場合をディスクにします。 送信できる、たとえば、ユーザー モード アプリケーションには、Microsoft Win32 関数が呼び出されるとなど**FlushFileBuffers**します。 (ファイル システム ドライバーとファイル システム フィルター ドライバーは、呼び出す[ **CcFlushCache** ](https://msdn.microsoft.com/library/windows/hardware/ff539082) IRP を送信する方が便利です)。

すべてファイル システムとフィルター ドライバーのデータの内部バッファーを維持するは、システムがシャット ダウンの間でファイル データまたはメタデータへの変更を保持できますようにこの IRP を処理する必要があります。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、任意の重要なデータまたはメタデータ ファイルのオブジェクトに関連付けられたと IRP の完了のディスクにフラッシュする必要があります。 この IRP の処理方法の詳細については、FASTFAT サンプルを調べます。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、ファイル オブジェクトに関連付けられているし、スタックの次の下位ドライバーには、この IRP を渡す、重要なデータやメタデータはディスクにフラッシュする必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のバッファーのフラッシュ要求の処理中の IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_フラッシュ\_バッファー使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_フラッシュ\_バッファー。

## <a name="see-also"></a>関連項目


[**CcFlushCache**](https://msdn.microsoft.com/library/windows/hardware/ff539082)

[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_フラッシュ\_バッファー (WDK カーネル リファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)

 

 






