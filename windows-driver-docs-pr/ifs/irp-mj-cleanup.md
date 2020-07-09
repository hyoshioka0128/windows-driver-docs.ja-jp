---
title: IRP_MJ_CLEANUP (IFS)
description: IRP\_MJ\_CLEANUP
ms.assetid: e4593d99-a721-4ab1-82a5-b32b9c312b25
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_CLEANUP
topic_type:
- apiref
api_name:
- IRP_MJ_CLEANUP
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c40dd8c42f6066e79683f1413b5933496299b47d
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141314"
---
# <a name="irp_mj_cleanup-ifs"></a>IRP \_ MJ \_ CLEANUP (IFS)


## <a name="when-sent"></a>送信時


IRP \_ MJ \_ CLEANUP 要求の受信は、ファイルオブジェクトのハンドル参照カウントが0に達したことを示します。 (つまり、ファイルオブジェクトへのすべてのハンドルが閉じられています)。多くの場合、ユーザーモードアプリケーションが、ファイルオブジェクトへの最後の未処理ハンドルで Microsoft Win32 **CloseHandle**関数 (またはカーネルモードドライバーが[**zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出したとき) を呼び出したときに送信されます。

ファイルオブジェクトへのすべてのハンドルが閉じられている場合は、必ずしもファイルオブジェクトが使用されなくなったことを意味するわけではないことに注意してください。 キャッシュマネージャーやメモリマネージャーなどのシステムコンポーネントでは、ファイルオブジェクトへの未解決の参照が保持される場合があります。 これらのコンポーネントは、IRP \_ MJ \_ CLEANUP 要求が受信された後でも、ファイルに対して読み取りまたは書き込みを行うことができます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ターゲットデバイスオブジェクトがファイルシステムのコントロールデバイスオブジェクトである場合は、ファイルシステムドライバーが IRP を完了する必要があります。

それ以外の場合、ファイルシステムドライバーはクリーンアップ要求を処理する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


ターゲットデバイスオブジェクトがフィルタードライバーのコントロールデバイスオブジェクトである場合、フィルタードライバーは IRP を完了する必要があります。

それ以外の場合は、必要な処理を実行した後、フィルタードライバーが IRP をスタック上の次の下位のドライバーに渡す必要があります。

ファイルシステムフィルタードライバーの作成者は、 [**Iocreatestreamfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)によって IRP \_ MJ \_ CLEANUP 要求がボリュームのファイルシステムドライバースタックに送信されることに注意してください。 ファイルシステムは、IRP MJ create 以外の操作の副作用としてストリームファイルオブジェクトを作成することが多いため \_ \_ 、フィルタードライバーがストリームファイルオブジェクトの作成を確実に検出することは困難です。 したがって、フィルタードライバーは、以前に表示さ \_ \_ れて \_ いないファイルオブジェクトに対して、irp MJ CLEANUP 要求と irp MJ CLOSE 要求を受け取ることを想定して \_ います。

フィルタードライバーの作成者は、 [**Iocreatestreamfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)とは異なり、 [**iocreatestreamfileMJ tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)では、IRP \_ \_ のクリーンアップ要求がファイルシステムのドライバースタックに送信されないことにも注意してください。 このため、ファイルシステムでは、IRP MJ create 以外の操作の副作用としてストリームファイルオブジェクトを作成することが多いため、 \_ \_ フィルタードライバーがストリームファイルオブジェクトの作成を確実に検出することは困難です。 そのため、フィルタードライバーは、以前に表示さ \_ \_ れていないファイルオブジェクトに対して IRP MJ CLOSE 要求を受け取ることを想定しています。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーでは、クリーンアップ要求の処理中に、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--flags"></a>*Irp- &gt; フラグ*  
この要求には、次のフラグが設定されています。

IRP \_ CLOSE \_ 操作

IRP \_ 同期 \_ API

<a href="" id="irp--iostatus"></a>*Irp- &gt;* 最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造への iostatus ポインター。

<a href="" id="irpsp--fileobject"></a>*Irpsp- &gt;* *DeviceObject*に関連付けられているファイルオブジェクトへの FileObject ポインター。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 ファイルオブジェクト構造の "関連性のある**fileobject** " フィールド \_ は、IRP MJ CLEANUP の処理中は無効であり、 \_ \_ 使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*Irpsp- &gt;MajorFunction*は、IRP MJ クリーンアップを指定し \_ \_ ます。

## <a name="see-also"></a>関連項目


[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**Iocreatestreamfileite Tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ CLEANUP (WDK カーネルリファレンス)**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)

[**IRP \_ MJ \_ CLOSE**](irp-mj-close.md)

[**IRP \_ MJ の \_ 作成**](irp-mj-create.md)

[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)

 

 






