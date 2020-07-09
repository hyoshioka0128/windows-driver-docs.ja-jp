---
title: IRP_MJ_CLOSE (IFS)
description: IRP\_MJ\_CLOSE
ms.assetid: 62bb28de-7f89-4009-9ea9-0aa3d6bca0ed
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_CLOSE
topic_type:
- apiref
api_name:
- IRP_MJ_CLOSE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9612df55783090503f4c31c2af94ef79798dfe3
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141325"
---
# <a name="irp_mj_close-ifs"></a>IRP \_ MJ \_ CLOSE (IFS)


## <a name="when-sent"></a>送信時


IRP MJ CLOSE 要求の受信は、ファイル \_ \_ オブジェクトの参照カウントが0に達したことを示します。通常、ファイルシステムドライバーまたはその他のカーネルモードコンポーネントがファイルオブジェクトで[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出したことが原因です。 通常、この要求はクリーンアップ要求の後に続きます。 ただし、これは必ずしも、終了要求がクリーンアップ要求の直後に受信されることを意味するわけではありません。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ターゲットデバイスオブジェクトがファイルシステムのコントロールデバイスオブジェクトである場合は、必要な処理を実行した後で、ファイルシステムドライバーが IRP を完了する必要があります。

それ以外の場合は、ファイルシステムドライバーが close 要求を処理する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


ターゲットデバイスオブジェクトがフィルタードライバーのコントロールデバイスオブジェクトである場合、フィルタードライバーは、コントロールデバイスオブジェクトとの通信を終了し、IRP を完了するために必要な処理を実行する必要があります。

それ以外の場合、フィルタードライバーは、フィルタードライバーによって保持されているファイルごとのオブジェクトおよびファイルごとのオブジェクトのコンテキスト情報を削除するなど、必要な処理を実行した後、スタック上の次の下位のドライバーに IRP を渡す必要があります。

ファイルシステムフィルタードライバーの作成者は、 [**Iocreatestreamfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)によって[**IRP \_ MJ \_ CLEANUP**](irp-mj-cleanup.md)要求がボリュームのファイルシステムドライバースタックに送信されることに注意してください。 ファイルシステムは、 [**IRP \_ MJ \_ create**](irp-mj-create.md)以外の操作の副作用としてストリームファイルオブジェクトを作成することが多いため、フィルタードライバーがストリームファイルオブジェクトの作成を確実に検出することは困難です。 したがって、フィルタードライバーは、以前に表示されていないファイルオブジェクトに対して、 **irp \_ MJ \_ CLEANUP**要求と[**irp \_ MJ \_ CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)要求を受け取ることを想定しています。

フィルタードライバーの作成者は、 [**Iocreatestreamfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)とは異なり、 [**iocreatestreamfileMJ tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)では、 [**IRP \_ の \_ クリーンアップ**](irp-mj-cleanup.md)要求がファイルシステムのドライバースタックに送信されないことにも注意してください。 このため、ファイルシステムでは、 [**IRP \_ MJ \_ create**](irp-mj-create.md)以外の操作の副作用としてストリームファイルオブジェクトを作成することが多いため、フィルタードライバーがストリームファイルオブジェクトの作成を確実に検出することは困難です。 そのため、フィルタードライバーは、以前に表示されていないファイルオブジェクトに対して**IRP \_ MJ \_ CLOSE**要求を受け取ることを想定しています。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、終了要求を処理するときに、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--flags"></a>*Irp- &gt; フラグ*  
この要求には、次のフラグが設定されています。

IRP \_ CLOSE \_ 操作

IRP \_ 同期 \_ API

<a href="" id="irp--iostatus"></a>*Irp- &gt;* 最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造への iostatus ポインター。

<a href="" id="irpsp--fileobject"></a>*Irpsp- &gt;* *DeviceObject*に関連付けられているファイルオブジェクトへの FileObject ポインター。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 ファイルオブジェクト構造の関連性のある**fileobject**フィールド \_ は、IRP MJ CLOSE の処理中は無効であり、 \_ 使用でき \_ ません。

<a href="" id="irpsp--majorfunction"></a>*Irpsp- &gt;MajorFunction*は、IRP MJ CLOSE を指定し \_ \_ ます。

## <a name="see-also"></a>関連項目


[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**Iocreatestreamfileite Tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ CLOSE (WDK カーネルリファレンス)**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)

[**IRP \_ MJ の \_ クリーンアップ**](irp-mj-cleanup.md)

[**IRP \_ MJ の \_ 作成**](irp-mj-create.md)

[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)

 

 






