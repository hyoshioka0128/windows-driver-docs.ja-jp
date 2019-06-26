---
title: IRP_MJ_CLEANUP
description: IRP\_MJ\_CLEANUP
ms.assetid: e4593d99-a721-4ab1-82a5-b32b9c312b25
keywords:
- IRP_MJ_CLEANUP インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_CLEANUP
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 685d4dfa6823b1a4b586442e8d4efd50e62a4d27
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376106"
---
# <a name="irpmjcleanup"></a>IRP\_MJ\_CLEANUP


## <a name="when-sent"></a>送信時


IRP の受領書\_MJ\_クリーンアップ要求では、ファイル オブジェクトのハンドルの参照カウントがゼロに達したことを示します。 (つまり、ファイル オブジェクトへのすべてのハンドルが閉じられました。)多くの場合、ユーザー モード アプリケーションには、Microsoft Win32 が呼び出されたときに送信される**CloseHandle**関数 (カーネル モード ドライバーが呼び出されたときまたは[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)) 最後のファイル オブジェクトへの未処理のハンドル。

あるファイル オブジェクトへのすべてのハンドルが閉じられたときにこれは必ずしもファイル オブジェクトが不要になった使用されていることに注意してください。 重要です。 キャッシュ マネージャーや、メモリ マネージャーなどのシステム コンポーネントには、ファイル オブジェクトへの未解決の参照を保持可能性があります。 これらのコンポーネントの読み取りや IRP 後も、ファイルから作成できますも\_MJ\_クリーンアップ要求を受信します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ターゲット デバイス オブジェクトが、ファイル システムの制御デバイス オブジェクトの場合、ファイル システム ドライバーは IRP を完了する必要があります。

それ以外の場合、ファイル システム ドライバーは、クリーンアップ要求を処理する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


ターゲット デバイス オブジェクトが、フィルター ドライバーの制御デバイス オブジェクトの場合は、フィルター ドライバーは IRP を完了する必要があります。

それ以外の場合、フィルター ドライバーは、必要な処理を実行した後は、スタック上に次の下位ドライバー IRP を渡す必要があります。

ファイル システム フィルター ドライバー開発者が注意を[ **IoCreateStreamFileObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobject) IRP が\_MJ\_クリーンアップ要求のファイル システム ドライバー スタックへの送信、ボリューム。 ファイル システム多くの場合、オブジェクトを作成ストリーム ファイル IRP 以外の操作の副作用としてため\_MJ\_作成、ストリームのファイル オブジェクトの作成を確実に検出するために、フィルター ドライバーに対することは困難です。 フィルター ドライバーは IRP を受信することしたがって\_MJ\_クリーンアップと IRP\_MJ\_閉じるが以前の見えないファイル オブジェクトを要求します。

フィルター ドライバー開発者も注意してくださいとは異なり[ **IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobject)、 [ **IoCreateStreamFileObjectLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobjectlite)しませんIRP が発生する\_MJ\_クリーンアップ要求をファイル システム ドライバー スタックに送信します。 このため、のでファイル システム多くの場合、ストリームのファイル オブジェクトの IRP 以外の操作の副作用として\_MJ\_作成、ストリームのファイル オブジェクトの作成を確実に検出するために、フィルター ドライバーに対することは困難です。 フィルター ドライバーは IRP を受信することしたがって\_MJ\_閉じるが以前の見えないファイル オブジェクトを要求します。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP のクリーンアップ要求の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--flags"></a>*Irp-&gt;フラグ*  
この要求に対して、次のフラグが設定されます。

IRP\_閉じる\_操作

IRP\_同期\_API

<a href="" id="irp--iostatus"></a>*Irp -&gt;IoStatus*へのポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)に関する最終的な完了の状態および情報を受け取る、要求された操作。

<a href="" id="irpsp--fileobject"></a>*IrpSp -&gt;FileObject*に関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_クリーンアップ使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp -&gt;MajorFunction* IRP を指定します\_MJ\_クリーンアップします。

## <a name="see-also"></a>関連項目


[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_クリーンアップ (WDK カーネル リファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)

[**IRP\_MJ\_CLOSE**](irp-mj-close.md)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)

 

 






