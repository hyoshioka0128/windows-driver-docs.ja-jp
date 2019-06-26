---
title: IRP_MJ_CLOSE
description: IRP\_MJ\_CLOSE
ms.assetid: 62bb28de-7f89-4009-9ea9-0aa3d6bca0ed
keywords:
- 未完了のインストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_CLOSE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98b2ef82f7db4856c01700764c432f861cda84f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376104"
---
# <a name="irpmjclose"></a>IRP\_MJ\_CLOSE


## <a name="when-sent"></a>送信時


IRP の受領書\_MJ\_終了要求は、ファイル オブジェクトの参照カウントが 0 になっていることを示します、ファイル システム ドライバーまたはその他のカーネル モード コンポーネントが呼び出されるために通常[ **ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)ファイル オブジェクト。 この要求には、クリーンアップ要求が正常に従います。 ただし、これは必ずしもクリーンアップ要求後すぐに終了要求を受信します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ターゲット デバイス オブジェクトが、ファイル システムの制御デバイス オブジェクトの場合は、ファイル システム ドライバーは、必要な処理を実行した後は IRP を完了する必要があります。

それ以外の場合、ファイル システム ドライバーは、閉じる要求を処理する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


ターゲット デバイス オブジェクトが、フィルター ドライバーの制御デバイス オブジェクトの場合は、何がコントロールのデバイス オブジェクトとの通信を終了して、IRP の完了に必要なフィルター ドライバーが行う必要があります。

それ以外の場合、フィルター ドライバーは、ファイルごとと、フィルター ドライバーによって保持されているファイルごとのオブジェクトのコンテキスト情報を削除するなど、必要な処理を実行した後は、スタック上に次の下位ドライバー IRP を渡す必要があります。

ファイル システム フィルター ドライバー開発者が注意を[ **IoCreateStreamFileObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobject)により、 [ **IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)ボリュームのファイル システム ドライバー スタックに送信される要求。 ファイル システム多くの場合、オブジェクトを作成ストリーム ファイルの操作の副作用として以外のため、 [ **IRP\_MJ\_作成**](irp-mj-create.md)、フィルター ドライバーを確実に検出することは困難ですストリームのファイル オブジェクトの作成。 フィルター ドライバーを受信することはそのため**IRP\_MJ\_クリーンアップ**と[**IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)未知のファイル オブジェクトを要求します。

フィルター ドライバー開発者も注意してくださいとは異なり[ **IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobject)、 [ **IoCreateStreamFileObjectLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobjectlite)しません[ **IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)要求をファイル システム ドライバー スタックに送信します。 このため、のでファイル システム多くの場合、ストリームのファイル オブジェクトの操作の副作用として以外の[ **IRP\_MJ\_作成**](irp-mj-create.md)、フィルター ドライバーのことは困難ですストリームのファイル オブジェクトの作成を確実に検出します。 フィルター ドライバーを受信することはつまり**IRP\_MJ\_閉じる**見えないファイル オブジェクトを以前に要求します。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の終了要求の処理に IRP スタックの場所は、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--flags"></a>*Irp-&gt;フラグ*  
この要求に対して、次のフラグが設定されます。

IRP\_閉じる\_操作

IRP\_同期\_API

<a href="" id="irp--iostatus"></a>*Irp -&gt;IoStatus*へのポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)に関する最終的な完了の状態および情報を受け取る、要求された操作。

<a href="" id="irpsp--fileobject"></a>*IrpSp -&gt;FileObject*に関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_閉じる使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp -&gt;MajorFunction* IRP を指定します\_MJ\_閉じる。

## <a name="see-also"></a>関連項目


[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_閉じる (WDK カーネル リファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)

[**IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)

 

 






