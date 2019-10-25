---
title: IRP ベースまたは高速 I/O とすることが可能な操作
description: IRP ベースまたは高速 I/O とすることが可能な操作
ms.assetid: 768f5744-1aea-4fa8-b81b-d2670d6c878e
keywords:
- 高速 i/o バッファー WDK ファイルシステム
- Flags メンバー WDK ファイルシステム
- デバイスオブジェクトフラグ WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0cdb2070bb47306e271fe66ba396d93d0ad696a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841050"
---
# <a name="operations-that-can-be-irp-based-or-fast-io"></a>IRP ベースまたは高速 I/O とすることが可能な操作


## <span id="ddk_operations_that_can_be_irp_based_or_fast_io_if"></span><span id="DDK_OPERATIONS_THAT_CAN_BE_IRP_BASED_OR_FAST_IO_IF"></span>


次の種類の操作では、IRP ベースまたは高速の i/o 操作を実行できます。

-   IRP\_MJ\_デバイス\_コントロールです。 (IRP\_MJ\_内部\_デバイス\_コントロールは常に IRP ベースであることに注意してください)。

-   IRP\_MJ\_クエリ\_情報。 **Fileinformationclass**パラメーターが**fileinformationclass**、 **Fileinformationclass**、または**FileNetworkOpenInformation**の場合、この操作は高速 i/o になることがあります。

-   IRP\_MJ\_読み取ります。 ミニフィルタードライバーは、MJ i/o IRP\_が受信されないようにするために、 [**FLT\_操作\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_operation_registration)構造で、キャッシュされた\_IO フラグの\_を\_スキップするように FLTFL\_\_操作を設定でき\_読み取り操作とキャッシュされた IRP ベースの読み取り。

-   IRP\_MJ\_書き込みです。 ミニフィルタードライバーでは、FLTFL\_操作\_登録\_スキップ\_キャッシュされた\_IO フラグを FLT\_操作\_登録構造に設定することにより、高速 i/o IRP\_MJ\_書き込みが受信されないようにすることができます。操作とキャッシュされた IRP ベースの書き込み。

これらの操作のいずれかが高速 i/o 操作である場合、対応する IRP ベースの操作で別のバッファリング方法が使用されていても、バッファーも直接 i/o も使用されません。

IRP\_MJ\_デバイス\_制御が高速 i/o 操作である場合、IOCTL の転送の種類に関係なく、常にバッファーと直接の両方の i/o が使用されます。

IRP\_MJ\_LOCK\_CONTROL は、IRP ベースまたは高速の i/o 操作にすることができますが、バッファーはありません。

 

 




