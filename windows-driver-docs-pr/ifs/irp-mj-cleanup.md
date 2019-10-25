---
title: IRP_MJ_CLEANUP
description: IRP\_MJ\_CLEANUP
ms.assetid: e4593d99-a721-4ab1-82a5-b32b9c312b25
keywords:
- IRP_MJ_CLEANUP インストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_CLEANUP
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a67023be7034846d67cbe78055e5910f281f2b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841183"
---
# <a name="irp_mj_cleanup"></a>IRP\_MJ\_CLEANUP


## <a name="when-sent"></a>送信時


IRP\_MJ\_クリーンアップ要求を受信すると、ファイルオブジェクトのハンドル参照カウントが0に達したことを示します。 (つまり、ファイルオブジェクトへのすべてのハンドルが閉じられています)。多くの場合、ユーザーモードアプリケーションが、ファイルオブジェクトへの最後の未処理ハンドルで Microsoft Win32 **CloseHandle**関数 (またはカーネルモードドライバーが[**zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出したとき) を呼び出したときに送信されます。

ファイルオブジェクトへのすべてのハンドルが閉じられている場合は、必ずしもファイルオブジェクトが使用されなくなったことを意味するわけではないことに注意してください。 キャッシュマネージャーやメモリマネージャーなどのシステムコンポーネントでは、ファイルオブジェクトへの未解決の参照が保持される場合があります。 これらのコンポーネントは、IRP\_MJ\_クリーンアップ要求を受信した後でも、ファイルに対して読み取りまたは書き込みを行うことができます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ターゲットデバイスオブジェクトがファイルシステムのコントロールデバイスオブジェクトである場合は、ファイルシステムドライバーが IRP を完了する必要があります。

それ以外の場合、ファイルシステムドライバーはクリーンアップ要求を処理する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


ターゲットデバイスオブジェクトがフィルタードライバーのコントロールデバイスオブジェクトである場合、フィルタードライバーは IRP を完了する必要があります。

それ以外の場合は、必要な処理を実行した後、フィルタードライバーが IRP をスタック上の次の下位のドライバーに渡す必要があります。

ファイルシステムフィルタードライバーの作成者は、 [**Iocreatestreamfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)によって IRP\_MJ\_クリーンアップ要求がボリュームのファイルシステムドライバースタックに送信されることに注意してください。 ファイルシステムは、IRP\_MJ\_CREATE 以外の操作の副作用としてストリームファイルオブジェクトを作成することが多いため、フィルタードライバーがストリームファイルオブジェクトの作成を確実に検出することは困難です。 したがって、フィルタードライバーは、以前に表示されていないファイルオブジェクトに対して、IRP\_MJ\_CLEANUP および IRP\_\_MJ を受け取ることを予期しています。

フィルタードライバーの作成者は、 [**Iocreatestreamfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)とは異なり、 [**iocreatestreamfileMJ tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)では、IRP\_\_クリーンアップ要求がファイルシステムのドライバースタックに送信されないことにも注意してください。 このため、およびでは、ファイルシステムは、IRP\_MJ\_CREATE 以外の操作の副作用としてストリームファイルオブジェクトを作成することが多いため、フィルタードライバーがストリームファイルオブジェクトの作成を確実に検出することは困難です。 したがって、フィルタードライバーは、以前に表示されていないファイルオブジェクトに対して、IRP\_MJ\_閉じる要求を受け取ることを期待します。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーでは、クリーンアップ要求の処理中に、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--flags"></a>*Irp&gt;フラグ*  
この要求には、次のフラグが設定されています。

IRP\_\_操作を閉じる

IRP\_同期\_API

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

<a href="" id="irpsp--fileobject"></a>*Irpsp-&gt;FileObject* *DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_obect 構造体でもあります。 IRP\_MJ\_CLEANUP の処理中は、ファイル\_オブジェクト構造の関連性の**あるフィールドは**無効であるため、使用できません。

<a href="" id="irpsp--majorfunction"></a>*Irpsp-&gt;MajorFunction*IRP\_MJ\_クリーンアップを指定します。

## <a name="see-also"></a>関連項目


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**Iocreatestreamfileite Tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_CLEANUP (WDK カーネルリファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)

[**IRP\_MJ\_閉じる**](irp-mj-close.md)

[**IRP\_MJ\_作成**](irp-mj-create.md)

[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)

 

 






