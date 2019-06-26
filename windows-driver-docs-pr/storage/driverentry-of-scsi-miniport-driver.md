---
title: SCSI ミニポート ドライバーの DriverEntry ルーチン
description: 各ミニポート ドライバーには、明示的に読み込むために DriverEntry という名前のルーチンが必要です。注意してください、SCSI ポートはドライバーと SCSI ミニポート ドライバー モデルが変更されるか利用今後です。
ms.assetid: dda79363-06a9-4902-8e04-186293b6c9d4
keywords:
- DriverEntry ルーチン ストレージ デバイス
topic_type:
- apiref
api_name:
- DriverEntry
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 629778fc5987971e7d8bf8b056f55f7aee38596b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368262"
---
# <a name="driverentry-of-scsi-miniport-driver-routine"></a>SCSI ミニポート ドライバーの DriverEntry ルーチン


各ミニポート ドライバーが明示的に指定のルーチンをいる必要があります**DriverEntry**読み込まれるためです。

&gt; \[!注\] &gt; SCSI ポートはドライバーと SCSI ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。

 

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

*[引数 1]* \[で\]  
ミニポート ドライバーを呼び出す必要がありますが、ポインターは、 **ScsiPortInitialize**します。

*[引数 2]* \[で\]  
ミニポート ドライバーを呼び出す必要がありますが、ポインターは、 **ScsiPortInitialize**します。

<a name="return-value"></a>戻り値
------------

**DriverEntry**によって返される値を返します**ScsiPortInitialize**します。 呼び出す場合**ScsiPortInitialize**複数回**DriverEntry**によって返される最小値を返します**ScsiPortInitialize**します。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーの**DriverEntry**ルーチンがスタックにメモリを割り当て、ハードウェアを初期化します\_初期化\_ゼロのデータ構造体。 **DriverEntry**ハードウェア ベースのすべてのメンバーをゼロする必要があります\_初期化\_HBA(s) ミニポート ドライバーに適切な値で初期化する前にデータ構造をサポートしています。

**DriverEntry**設定する必要があります、 **HwInitializationDataSize**メンバー **sizeof**(HW\_初期化\_データ) をこの構造体のバージョンを示すためにこれを使用して、だけでなく hba に関連づけての適切なすべてのメンバーを初期化します。

次に、 **DriverEntry**呼び出し**ScsiPortInitialize**します。 ミニポート ドライバーが両方などの I/O バスの 2 つ以上の型に接続できる HBA(s) をサポートしているか**マイクロ チャネル**と**Isa**バスを入力する必要がありますを呼び出すことが**ScsiPortInitialize**I/O バスの種類ごとに 1 回です。 このようなミニポート ドライバーへの呼び出しによって返される最小値を返す必要があります**ScsiPortInitialize**から、 **DriverEntry**ルーチン。 ミニポート ドライバーのライターがによって返される値に関する仮定ことないが**ScsiPortInitialize**します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)

[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))

[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)

 

 






