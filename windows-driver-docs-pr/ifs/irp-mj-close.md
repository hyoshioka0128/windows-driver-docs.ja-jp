---
title: IRP_MJ_CLOSE
description: IRP\_MJ\_CLOSE
ms.assetid: 62bb28de-7f89-4009-9ea9-0aa3d6bca0ed
keywords:
- IRP_MJ_CLOSE インストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_CLOSE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29994f5da65d3624e202b4667268c4a43a8c4a20
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841194"
---
# <a name="irp_mj_close"></a>IRP\_MJ\_CLOSE


## <a name="when-sent"></a>送信時


IRP\_MJ\_CLOSE 要求の受信は、ファイルオブジェクトの参照カウントが0に達したことを示します。通常、ファイルシステムドライバーまたはその他のカーネルモードコンポーネントがファイルオブジェクトで[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出したためです。 通常、この要求はクリーンアップ要求の後に続きます。 ただし、これは必ずしも、終了要求がクリーンアップ要求の直後に受信されることを意味するわけではありません。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ターゲットデバイスオブジェクトがファイルシステムのコントロールデバイスオブジェクトである場合は、必要な処理を実行した後で、ファイルシステムドライバーが IRP を完了する必要があります。

それ以外の場合は、ファイルシステムドライバーが close 要求を処理する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


ターゲットデバイスオブジェクトがフィルタードライバーのコントロールデバイスオブジェクトである場合、フィルタードライバーは、コントロールデバイスオブジェクトとの通信を終了し、IRP を完了するために必要な処理を実行する必要があります。

それ以外の場合、フィルタードライバーは、フィルタードライバーによって保持されているファイルごとのオブジェクトおよびファイルごとのオブジェクトのコンテキスト情報を削除するなど、必要な処理を実行した後、スタック上の次の下位のドライバーに IRP を渡す必要があります。

ファイルシステムフィルタードライバーの作成者は、 [**Iocreatestreamfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)によって[**IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)要求がボリュームのファイルシステムドライバースタックに送信されることに注意してください。 ファイルシステムは、 [**IRP\_MJ\_create**](irp-mj-create.md)以外の操作の副作用としてストリームファイルオブジェクトを作成することが多いため、フィルタードライバーがストリームファイルオブジェクトの作成を確実に検出することは困難です。 したがって、フィルタードライバーは、以前に表示されていないファイルオブジェクトに対して、 **irp\_MJ\_CLEANUP**および[**IRP\_\_MJ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)を受け取ることを予期しています。

フィルタードライバーの作成者は、 [**Iocreatestreamfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)とは異なり、 [**iocreatestreamfileMJ tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)では、 [**IRP\_\_クリーンアップ**](irp-mj-cleanup.md)要求がファイルシステムのドライバースタックに送信されないことにも注意してください。 このため、およびでは、ファイルシステムは、 [**IRP\_MJ\_create**](irp-mj-create.md)以外の操作の副作用としてストリームファイルオブジェクトを作成することが多いため、フィルタードライバーがストリームファイルオブジェクトの作成を確実に検出することは困難です。 したがって、フィルタードライバーは、以前に表示されていないファイルオブジェクトに対して、 **IRP\_MJ\_閉じる**要求を受け取ることを期待します。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、終了要求を処理するときに、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--flags"></a>*Irp&gt;フラグ*  
この要求には、次のフラグが設定されています。

IRP\_\_操作を閉じる

IRP\_同期\_API

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

<a href="" id="irpsp--fileobject"></a>*Irpsp-&gt;FileObject* *DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_obect 構造体でもあります。 IRP\_MJ\_CLOSE の処理中は、ファイル\_オブジェクト構造の関連性のあるフィールドが無効である**ため、使用**できません。

<a href="" id="irpsp--majorfunction"></a>*Irpsp-&gt;MajorFunction*IRP\_MJ\_閉じることを指定します。

## <a name="see-also"></a>関連項目


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**Iocreatestreamfileite Tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_CLOSE (WDK カーネルリファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)

[**IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)

[**IRP\_MJ\_作成**](irp-mj-create.md)

[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)

 

 






