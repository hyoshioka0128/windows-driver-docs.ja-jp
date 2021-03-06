---
title: バス相対アドレスの仮想アドレスへのマッピング
description: バス相対アドレスの仮想アドレスへのマッピング
ms.assetid: 16496465-8a30-4250-9d64-afd36a788ae2
keywords:
- 仮想アドレス空間のマッピングの WDK カーネル
- 物理アドレス空間のマッピングの WDK カーネル
- マッピングのメモリ
- アドレス空間のマッピングの WDK カーネル
- アドレス空間の WDK カーネルを翻訳します。
- メモリ管理 WDK カーネルは、アドレスのマッピング
- バスの相対メモリ領域の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: be828c854982041d81a8334fa0502b6bc4a2f3d9
ms.sourcegitcommit: 289b5f97aff1b9ea1fefc9a8731e0fc16533073b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492535"
---
# <a name="mapping-bus-relative-addresses-to-virtual-addresses"></a>バス相対アドレスの仮想アドレスへのマッピング





一部のプロセッサでは、他のプロセッサがない別のメモリと I/O のアドレス空間を実装します。 ハードウェア プラットフォームでのこれらの違いによりメカニズム ドライバーは、I/O、またはメモリ常駐型と異なるため、プラットフォームのデバイス リソースへのアクセスに使用します。

マネージャーのデバイスの I/O、メモリ リソース、PnP への応答を要求するドライバー [ **IRP\_MN\_クエリ\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements) IRP します。 ハードウェアのアーキテクチャに応じて、HAL は I/O 領域またはメモリの領域での I/O リソースを割り当てることができ、I/O 領域またはメモリ領域でのメモリ リソースを割り当てることができます。

HAL がリソースにアクセスするデバイス (デバイスの登録) などのバスの相対メモリ領域を使用する場合、ドライバーは、これらのリソースにアクセスできるようにする仮想メモリに I/O の領域をマップする必要があります。 ドライバーでは、リソースがデバイスの起動時に PnP マネージャーで、ドライバーに渡される翻訳済みのリソースを調べることによって I/O またはメモリ常駐がかどうかを判断できます。 HAL が I/O の領域を使用する場合のマッピングは必要ありません。

具体的には、ドライバーを受け取ると、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)に構造を調べる必要があります、要求**IrpSp&gt;Parameters.StartDevice.AllocatedResources**と**IrpSp -&gt;Parameters.StartDevice.AllocatedResourcesTranslated**、生 (バス-相対) について説明するリソースの変換、それぞれ、PnP マネージャーがデバイスに割り当てられています。 ドライバーは、デバッグを支援するため、デバイスの拡張機能の各リソースの一覧のコピーを保存する必要があります。

リソースの一覧はペアになっている[ **CM\_リソース\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_resource_list) 、生のリストの各要素が変換されたリストの同じ要素に対応する構造体。 たとえば場合、 **AllocatedResources.List**\[0\]生 I/O ポートの範囲について説明します**AllocatedResourcesTranslated.List**\[0\]変換後の同じ範囲をについて説明します。 変換された各リソースには、物理アドレスとリソースの種類が含まれています。

ドライバーでの翻訳済みのメモリ リソースが割り当てられている場合 (**CmResourceTypeMemory**) を呼び出す必要があります[ **MmMapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapiospace)を通じて仮想アドレスを物理アドレスにマップするにはそのは、デバイスの登録にアクセスできます。 プラットフォームに依存しない方法で動作するドライバーの場合、すべての返される、変換されたリソースを確認して、必要に応じてマップします。

**カーネル モード ドライバーは IRP への応答で、次の手順を実行する必要があります\_MN\_開始\_デバイスのすべてのリソースにアクセスするために、デバイスの要求**

1.  コピー **IrpSp -&gt;Parameters.StartDevice.AllocatedResources**デバイス拡張機能にします。

2.  コピー **IrpSp -&gt;Parameters.StartDevice.AllocatedResourcesTranslated**デバイス拡張機能にします。

3.  ループ内の各記述子要素を検査**AllocatedResourcesTranslated**します。 記述子リソースの種類が場合**CmResourceTypeMemory**、呼び出す**MmMapIoSpace**、物理アドレスと翻訳されたリソースの長さを渡します。

ドライバーが受信すると、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)または[ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)を呼び出して、マッピングをリリースにする必要があります、PnP マネージャーから要求[ **MmUnmapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapiospace)のようなループ内で。 ドライバーは呼び出す必要がありますも**MmUnmapIoSpace**にする必要がありますが失敗した場合、 **IRP\_MN\_開始\_デバイス**要求。

生のリソースの種類が、ドライバーを呼び出す必要がある HAL アクセス ルーチンを示します (**読み取り\_登録\__XXX_** 、**書き込み\_レジスタ\__XXX_** 、**読み取り\_ポート\__XXX_** 、**書き込み\_ポート\_ _XXX_** )。 ほとんどのドライバーは、ドライバー自体がリソースを要求またはドライバー開発者は、デバイスのハードウェアの性質、必要な型を知っているため、使用するこれらのルーチンの判断するために生のリソースの一覧を確認する必要はありません。

 I/O 領域内のリソースの (**CmResourceTypePort**、 **CmResourceTypeInterrupt**、 **CmResourceTypeDma**)、ドライバーは、返されたの下位 32 ビットを使用する必要がありますリソースへのアクセス、デバイスなどを通じて、HAL の読み取りと書き込みの物理アドレス**読み取り\_登録\__XXX_** 、**書き込み\_登録\__XXX_** 、**読み取り\_ポート\__XXX_** 、**書き込み\_ポート\__XXX_** ルーチン。
 
 

 




