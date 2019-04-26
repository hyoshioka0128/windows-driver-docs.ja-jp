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
ms.openlocfilehash: bdf46453087e4173551db7f0d8a4ffc76fff27de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352794"
---
# <a name="operations-that-can-be-irp-based-or-fast-io"></a>IRP ベースまたは高速 I/O とすることが可能な操作


## <span id="ddk_operations_that_can_be_irp_based_or_fast_io_if"></span><span id="DDK_OPERATIONS_THAT_CAN_BE_IRP_BASED_OR_FAST_IO_IF"></span>


次の種類の操作は IRP ベースまたは高速の I/O 操作になります。

-   IRP\_MJ\_デバイス\_コントロール。 (注その IRP\_MJ\_内部\_デバイス\_コントロールは IRP ベースでは常にします)。

-   IRP\_MJ\_クエリ\_情報。 場合、この操作は高速の I/O にできる、 **FileInformationClass**パラメーターが**FileBasicInformation**、 **FileStandardInformation**、または**FileNetworkOpenInformation**します。

-   IRP\_MJ\_を読み取る。 ミニフィルター ドライバーは、FLTFL を設定できる\_操作\_登録\_スキップ\_CACHED\_IO フラグ、 [ **FLT\_操作\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544668)高速の I/O IRP を受信しないために構造\_MJ\_読み取り操作および IRP ベースのキャッシュの読み取り。

-   IRP\_MJ\_を記述します。 ミニフィルター ドライバーは、FLTFL を設定できます\_操作\_登録\_スキップ\_CACHED\_IO フラグ、FLT\_操作\_を避けるために、登録の構造体高速の I/O IRP を受信\_MJ\_書き込み操作と IRP ベースのキャッシュの書き込み。

これらの操作のいずれかが高速な I/O 操作の場合は、常に使用バッファーも直接 I/O、IRP ベースの同等の操作は、バッファリングの別の方法を使用する場合でもです。

ときに IRP\_MJ\_デバイス\_コントロールが高速な I/O 操作であるバッファーも直接 I/O、IOCTL の転送の種類に関係なく常に使用します。

IRP\_MJ\_ロック\_コントロールは IRP ベースまたは高速の I/O 操作であることができます、バッファーがありません。

 

 




