---
title: SCSI ミニポートドライバールーチンの DriverEntry
description: 各ミニポートドライバーは、読み込むために DriverEntry という名前のルーチンが明示的に指定されている必要があります。注 SCSI ポートドライバーおよび SCSI ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。
ms.assetid: dda79363-06a9-4902-8e04-186293b6c9d4
keywords:
- DriverEntry のルーチンストレージデバイス
topic_type:
- apiref
api_name:
- DriverEntry
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2e3bd556f6cfd74c3ce63afb4ab3b54764bef214
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845171"
---
# <a name="driverentry-of-scsi-miniport-driver-routine"></a>SCSI ミニポートドライバールーチンの DriverEntry


各ミニポートドライバーは、読み込むために**Driverentry**という名前のルーチンが明示的に指定されている必要があります。

&gt; \[!&gt;\] SCSI ポートドライバーと SCSI ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。

 

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
ULONG DriverEntry(
  _In_ PVOID Argument1,
  _In_ PVOID Argument2
);
```

<a name="parameters"></a>パラメーター
----------

\] の*引数 1* \[  
ミニポートドライバーが**ScsiPortInitialize**を呼び出す必要があるポインターです。

\] の*引数 2* \[  
ミニポートドライバーが**ScsiPortInitialize**を呼び出す必要があるポインターです。

<a name="return-value"></a>戻り値
------------

**Driverentry**は、 **ScsiPortInitialize**によって返された値を返します。 **ScsiPortInitialize**を複数回呼び出す場合、 **Driverentry**は**ScsiPortInitialize**によって返される最小値を返します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーの**Driverentry**ルーチンは、スタックにメモリを割り当て、ハードウェア\_初期化\_データ構造体をゼロで初期化します。 **Driverentry**は、ハードウェア\_初期化\_データ構造内のすべてのメンバーを0に設定してから、ミニポートドライバーがサポートする HBA に適した値に設定する必要があります。

**Driverentry**では、 **Hwinitializationdatasize**メンバーを**sizeof**(HW\_初期化\_データ) に設定して、使用しているこの構造体のバージョンを示すと共に、HBA。

次に、 **Driverentry**は**ScsiPortInitialize**を呼び出します。 **MicroChannel**と**Isa**の種類のバスの両方など、複数の種類の i/o バスで接続できる HBA をミニポートドライバーがサポートしている場合は、i/o バスの種類ごとに**ScsiPortInitialize**を1回呼び出す必要があります。 このようなミニポートドライバーは、 **Driverentry**ルーチンから**ScsiPortInitialize**への呼び出しによって返される最小値を返す必要があります。 ミニポートドライバーのライターは、 **ScsiPortInitialize**によって返される値についての仮定を行うことはできません。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**ハードウェア\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)

[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))

[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)

 

 






