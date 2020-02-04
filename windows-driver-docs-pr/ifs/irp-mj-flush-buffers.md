---
title: IRP_MJ_FLUSH_BUFFERS
description: IRP\_MJ\_フラッシュ\_バッファー
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
ms.openlocfilehash: c0d27d227cd3567c553d78cc552bf547b7dcc8ef
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977679"
---
# <a name="irp_mj_flush_buffers"></a>IRP\_MJ\_フラッシュ\_バッファー


## <a name="when-sent"></a>送信時


バッファー内のデータをディスクにフラッシュする必要がある場合、IRP\_MJ\_FLUSH\_BUFFERS 要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって送信されます。 たとえば、ユーザーモードアプリケーションが**Flushfilebuffers**などの Microsoft Win32 関数を呼び出した場合に、これを送信できます。 (ファイルシステムドライバーおよびファイルシステムフィルタードライバーの場合、通常は、(IRP の送信よりも) [**Ccflushcache**](https://msdn.microsoft.com/library/windows/hardware/ff539082)を呼び出すことをお勧めします)。

データの内部バッファーを保持するすべてのファイルシステムおよびフィルタードライバーは、この IRP を処理する必要があります。これにより、ファイルデータまたはメタデータへの変更をシステムのシャットダウン間で保持できるようになります。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ファイルオブジェクトに関連付けられている重要なデータまたはメタデータをディスクにフラッシュし、IRP を完了する必要があります。 この IRP を処理する方法の詳細については、FASTFAT サンプルを調べてください。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、ファイルオブジェクトに関連付けられている重要なデータまたはメタデータをディスクにフラッシュし、この IRP をスタック上の次の下位のドライバーに渡します。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、次の IRP のメンバーで設定されている情報を使用できます。また、バッファーのフラッシュの要求を処理するときに、IRP スタックの場所です。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  
最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_MJ\_フラッシュ\_バッファーの処理中は、ファイル\_オブジェクト構造の関連性の**あるフィールドは**無効であるため、使用できません。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP\_MJ\_フラッシュ\_バッファーを指定します。

## <a name="see-also"></a>「


[**CcFlushCache**](https://msdn.microsoft.com/library/windows/hardware/ff539082)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_フラッシュ\_バッファー (WDK カーネルリファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)

 

 






