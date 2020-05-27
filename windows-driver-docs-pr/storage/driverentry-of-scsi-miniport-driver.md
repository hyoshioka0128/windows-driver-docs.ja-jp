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
ms.openlocfilehash: 7fd62290aeb95a9376de974603357040822dcc14
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851482"
---
# <a name="driverentry-of-scsi-miniport-driver-routine"></a>SCSI ミニポートドライバールーチンの DriverEntry


各ミニポートドライバーは、読み込むために**Driverentry**という名前のルーチンが明示的に指定されている必要があります。

> [!NOTE]
> SCSI ポートドライバーおよび SCSI ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。

 

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

*引数 1* \[から\]  
ミニポートドライバーが**ScsiPortInitialize**を呼び出す必要があるポインターです。

*引数 2* \[から\]  
ミニポートドライバーが**ScsiPortInitialize**を呼び出す必要があるポインターです。

<a name="return-value"></a>戻り値
------------

**Driverentry**は、 **ScsiPortInitialize**によって返された値を返します。 **ScsiPortInitialize**を複数回呼び出す場合、 **Driverentry**は**ScsiPortInitialize**によって返される最小値を返します。

<a name="remarks"></a>コメント
-------

ミニポートドライバーの**Driverentry**ルーチンは、スタックにメモリを割り当て、 \_ \_ ゼロを使用して HW 初期化データ構造体を初期化します。 **Driverentry**は、ハードウェア初期化データ構造内のすべてのメンバーを0に設定してから、 \_ \_ ミニポートドライバーがサポートする HBA に適した値で初期化する必要があります。

**Driverentry**では、 **Hwinitializationdatasize**メンバーを**sizeof**(HW 初期化データ) に設定して、 \_ 使用している \_ この構造のバージョンを示し、HBA に対してすべてのメンバーを適切に初期化する必要があります。

次に、 **Driverentry**は**ScsiPortInitialize**を呼び出します。 **MicroChannel**と**Isa**の種類のバスの両方など、複数の種類の i/o バスで接続できる HBA をミニポートドライバーがサポートしている場合は、i/o バスの種類ごとに**ScsiPortInitialize**を1回呼び出す必要があります。 このようなミニポートドライバーは、 **Driverentry**ルーチンから**ScsiPortInitialize**への呼び出しによって返される最小値を返す必要があります。 ミニポートドライバーのライターは、 **ScsiPortInitialize**によって返される値についての仮定を行うことはできません。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**HW \_ 初期化 \_ データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)

[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))

[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)

 

 






