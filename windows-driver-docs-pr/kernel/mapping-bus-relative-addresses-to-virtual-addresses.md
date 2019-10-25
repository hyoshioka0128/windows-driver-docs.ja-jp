---
title: バスの相対アドレスを仮想アドレスにマップする
description: バスの相対アドレスを仮想アドレスにマップする
ms.assetid: 16496465-8a30-4250-9d64-afd36a788ae2
keywords:
- 仮想アドレス空間のマッピング WDK カーネル
- 物理アドレス空間のマッピング WDK カーネル
- メモリのマッピング
- アドレス空間マッピング WDK カーネル
- アドレス空間 WDK カーネルの変換
- メモリ管理 (WDK カーネル)、アドレスのマッピング
- バス相対メモリ領域 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22b19d04a95614c87e2a4c6f59082e299291d355
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838543"
---
# <a name="mapping-bus-relative-addresses-to-virtual-addresses"></a>バスの相対アドレスを仮想アドレスにマップする





プロセッサによっては、個別のメモリおよび i/o アドレス空間が実装されますが、他のプロセッサでは実装されません。 これらのハードウェアプラットフォームの違いにより、i/o またはメモリ常駐型デバイスリソースへのアクセスに使用されるメカニズムドライバーは、プラットフォームによって異なります。

ドライバーは、PnP マネージャーの Irp\_に応答してデバイス i/o およびメモリリソースを要求します。この[ **\_クエリ\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)の irp を実行します。 ハードウェアアーキテクチャによっては、HAL は i/o 領域またはメモリ領域に i/o リソースを割り当てることができ、i/o 領域またはメモリ領域にメモリリソースを割り当てることができます。

HAL がバス相対メモリ空間を使用してデバイスリソース (デバイスレジスタなど) にアクセスする場合、ドライバーは、これらのリソースにアクセスできるように、i/o 領域を仮想メモリにマップする必要があります。 ドライバーは、デバイスの起動時に PnP マネージャーによってドライバーに渡された変換されたリソースを調べることによって、リソースが i/o またはメモリ常駐であるかどうかを判断できます。 HAL で i/o space を使用する場合、マッピングは必要ありません。

具体的には、\_デバイスの要求を[**開始\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を受信した場合は、その構造を**irpsp-&gt;パラメーター**で調べる必要があります。 AllocatedResources と**irpsp-&gt;AllocatedResourcesTranslated。** PnP マネージャーがデバイスに割り当てた未加工の (バス相対) リソースと変換されたリソースをそれぞれ記述します。 ドライバーは、デバッグに役立つように、デバイス拡張機能に各リソースリストのコピーを保存する必要があります。

リソースリストは[**CM\_リソース\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)の構造体であり、未加工のリストの各要素は翻訳されたリストの同じ要素に対応しています。 たとえば、 **AllocatedResources**\[0\] によって raw i/o ポート範囲が記述されている場合、 **AllocatedResourcesTranslated**\[0\] は変換後の同じ範囲を示します。 変換された各リソースには、物理アドレスとリソースの種類が含まれます。

ドライバーに変換されたメモリリソース (**CmResourceTypeMemory**) が割り当てられている場合は、 [**Mmmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)を呼び出して、物理アドレスをデバイスレジスタにアクセスできる仮想アドレスにマップする必要があります。 ドライバーがプラットフォームに依存しない方法で動作するようにするには、返されたすべてのリソースをチェックし、必要に応じてマップする必要があります。

**カーネルモードドライバーは、すべてのデバイスリソースへのアクセスを確保するために、IRP\_に応答して次の手順を実行する必要があります。これにより、\_デバイスの要求\_開始されます。**

1.  **Irpsp-&gt;AllocatedResources パラメーター**をデバイス拡張機能にコピーします。

2.  **Irpsp-&gt;AllocatedResourcesTranslated パラメーター**をデバイス拡張機能にコピーします。

3.  ループで、 **AllocatedResourcesTranslated**内の各記述子要素を検査します。 記述子のリソースの種類が**CmResourceTypeMemory**の場合は、 **Mmmapiospace**を呼び出して、翻訳されたリソースの物理アドレスと長さを渡します。

ドライバーが Irp\_を受信したときに、\_デバイスまたは[**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) [ **\_停止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)します。 PNP マネージャーからのデバイスの要求\_削除するには、 [**mmunmapiospace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace)を同様に呼び出して、マッピングを解放する必要があります。ループ.\_ また、ドライバーは、**デバイス要求\_開始\_IRP\_** が失敗する必要がある場合に、 **Mmunmapiospace**を呼び出す必要があります。

Raw リソースの種類は、ドライバーが呼び出す必要のある HAL アクセスルーチンを示します (**読み取り\_登録\__xxx_** 、**書き込み\_登録\__xxx_** 、**読み取り\_ポート\__xxx_** 、 **\_ポート\__XXX_** ) を書き込みます。 ドライバー自体がリソースを要求したか、またはドライバーライターがデバイスハードウェアの特性によって必要な種類を認識しているため、ほとんどのドライバーは、未加工のリソースリストを確認して、どのルーチンを使用するかを判断する必要はありません。

 I/o スペースのリソース (**Cmresourcetypeport**、 **cmresourcetypeport**、 **CmResourceTypeDma**) の場合、ドライバーは、返された物理アドレスの下位32ビットを使用してデバイスリソースにアクセスする必要があります。たとえば、HAL の読み取りと書き込みの**読み取り\_、 _xxx_\_の登録**、 **\_の登録\__xxx_** 、**読み取り\_ポート\__xxx_** 、 **\_ポートの書き込み\__xxx_** ルーチン。
 
 

 




