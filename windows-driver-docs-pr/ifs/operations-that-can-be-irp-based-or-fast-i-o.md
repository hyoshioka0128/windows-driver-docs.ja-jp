---
title: IRP ベースまたは高速 I/O とすることが可能な操作
description: IRP ベースまたは高速 I/O とすることが可能な操作
ms.assetid: 768f5744-1aea-4fa8-b81b-d2670d6c878e
keywords:
- 高速の I/O バッファー WDK ファイル システム
- メンバーの WDK ファイル システムをフラグします。
- デバイス オブジェクトのフラグの WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80f70acd3b5008b45b62efd5821504fa5dda5c6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384801"
---
# <a name="operations-that-can-be-irp-based-or-fast-io"></a>IRP ベースまたは高速 I/O とすることが可能な操作


## <span id="ddk_operations_that_can_be_irp_based_or_fast_io_if"></span><span id="DDK_OPERATIONS_THAT_CAN_BE_IRP_BASED_OR_FAST_IO_IF"></span>


次の種類の操作は IRP ベースまたは高速の I/O 操作になります。

-   IRP\_MJ\_デバイス\_コントロール。 (注その IRP\_MJ\_内部\_デバイス\_コントロールは IRP ベースでは常にします)。

-   IRP\_MJ\_クエリ\_情報。 場合、この操作は高速の I/O にできる、 **FileInformationClass**パラメーターが**FileBasicInformation**、 **FileStandardInformation**、または**FileNetworkOpenInformation**します。

-   IRP\_MJ\_を読み取る。 ミニフィルター ドライバーは、FLTFL を設定できる\_操作\_登録\_スキップ\_CACHED\_IO フラグ、 [ **FLT\_操作\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_operation_registration)高速の I/O IRP を受信しないために構造\_MJ\_読み取り操作および IRP ベースのキャッシュの読み取り。

-   IRP\_MJ\_を記述します。 ミニフィルター ドライバーは、FLTFL を設定できます\_操作\_登録\_スキップ\_CACHED\_IO フラグ、FLT\_操作\_を避けるために、登録の構造体高速の I/O IRP を受信\_MJ\_書き込み操作と IRP ベースのキャッシュの書き込み。

これらの操作のいずれかが高速な I/O 操作の場合は、常に使用バッファーも直接 I/O、IRP ベースの同等の操作は、バッファリングの別の方法を使用する場合でもです。

ときに IRP\_MJ\_デバイス\_コントロールが高速な I/O 操作であるバッファーも直接 I/O、IOCTL の転送の種類に関係なく常に使用します。

IRP\_MJ\_ロック\_コントロールは IRP ベースまたは高速の I/O 操作であることができます、バッファーがありません。

 

 




