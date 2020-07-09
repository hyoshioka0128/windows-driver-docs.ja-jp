---
title: IRP_MJ_FLUSH_BUFFERS (IFS)
description: IRP \_ MJ の \_ フラッシュ \_ バッファー
ms.assetid: 13df0d84-0320-4d7e-9acc-8f913ba6afaa
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_FLUSH_BUFFERS
topic_type:
- apiref
api_name:
- IRP_MJ_FLUSH_BUFFERS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ac3e7a90753051f997b91c3c24594a27aa87120
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141211"
---
# <a name="irp_mj_flush_buffers-ifs"></a>IRP \_ MJ の \_ フラッシュ \_ バッファー (IFS)


## <a name="when-sent"></a>送信時


IRP \_ MJ \_ FLUSH \_ BUFFERS 要求は、バッファーデータをディスクにフラッシュする必要がある場合に、i/o マネージャーと他のオペレーティングシステムコンポーネント、およびその他のカーネルモードドライバーによって送信されます。 たとえば、ユーザーモードアプリケーションが**Flushfilebuffers**などの Microsoft Win32 関数を呼び出した場合に、これを送信できます。 (ファイルシステムドライバーおよびファイルシステムフィルタードライバーの場合、通常は、(IRP の送信よりも) [**Ccflushcache**](https://msdn.microsoft.com/library/windows/hardware/ff539082)を呼び出すことをお勧めします)。

データの内部バッファーを保持するすべてのファイルシステムおよびフィルタードライバーは、この IRP を処理する必要があります。これにより、ファイルデータまたはメタデータへの変更をシステムのシャットダウン間で保持できるようになります。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ファイルオブジェクトに関連付けられている重要なデータまたはメタデータをディスクにフラッシュし、IRP を完了する必要があります。 この IRP を処理する方法の詳細については、FASTFAT サンプルを調べてください。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、ファイルオブジェクトに関連付けられている重要なデータまたはメタデータをディスクにフラッシュし、この IRP をスタック上の次の下位のドライバーに渡します。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、次の IRP のメンバーで設定されている情報を使用できます。また、バッファーのフラッシュの要求を処理するときに、IRP スタックの場所です。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp- &gt; iostatus*  
最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 ファイルオブジェクト構造の "関連性のある**fileobject** " フィールド \_ は、IRP MJ FLUSH バッファーの処理中は無効であり、 \_ \_ \_ 使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
IRP \_ MJ フラッシュバッファーを指定し \_ \_ ます。

## <a name="see-also"></a>関連項目


[**CcFlushCache**](https://msdn.microsoft.com/library/windows/hardware/ff539082)

[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ の \_ フラッシュ \_ バッファー (WDK カーネルリファレンス)**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)

 

 






