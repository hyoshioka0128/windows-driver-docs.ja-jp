---
title: Storport ドライバーの関数役割型を使用した関数の宣言
description: SDV で Storport ドライバーを分析できるようにするには、Storport に対して定義されている関数ロール型の宣言を使用して関数を宣言する必要があります。 関数ロールの種類は、Storport で定義されています。
ms.assetid: 40BD11CD-A559-4F90-BF39-4ED2FB800392
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de028e62d53936f924cf7a55366cfc7f4e925291
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840287"
---
# <a name="declaring-functions-by-using-function-role-types-for-storport-drivers"></a>Storport ドライバーの関数役割型を使用した関数の宣言


SDV で Storport ドライバーを分析できるようにするには、Storport に対して定義されている関数ロール型の宣言を使用して関数を宣言する必要があります。 関数ロールの種類は、Storport で定義されています。

対応するロールの種類を指定して、Storport ドライバーで各コールバック関数を宣言する必要があります。

DriverIntialize コールバック関数の関数ロール型宣言を次のコード例に示します。 関数ロールの種類は sp\_DRIVER\_INITIALIZE です。

```
sp_DRIVER_INITIALIZE DriverEntry;
```

コールバック関数に関数プロトタイプ宣言がある場合は、関数プロトタイプを関数ロール型宣言に置き換える必要があります。

| 関数ロールの種類                        | Storport ルーチン                                                                                                               |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| sp\_ドライバー\_初期化                    | DriverEntry                                                                                                                    |
| ハードウェア\_初期化                            | [**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)                                                                               |
| ハードウェア\_BUILDIO                               | [**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)                                                                                     |
| ハードウェア\_STARTIO                               | [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)                                                                                     |
| ハードウェア\_割り込み                             | [**HwStorInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_interrupt)                                                                                 |
| HW\_タイマー                                 | [**HwStorTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_timer)                                                                                         |
| ハードウェア\_\_アダプターの検索                         | [**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)                                                                             |
| ハードウェア\_リセット\_バス                            | [**HwStorResetBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_reset_bus)                                                                                   |
| ハードウェア\_アダプター\_制御                      | [**HwStorAdapterControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control)                                                                       |
| ハードウェア\_パッシブ\_\_ルーチンを初期化します          | [**HwStorPassiveInitializeRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_passive_initialize_routine)                                                   |
| ハードウェア\_DPC\_ルーチン                          | [**HwStorDpcRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_dpc_routine)                                                                               |
| ハードウェア\_空き\_アダプター\_リソース              | [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)構造の一部を HwFreeAdapterResources します。  |
| ハードウェア\_プロセス\_サービス\_要求             | [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)構造の一部を HwProcessServiceRequest します。 |
| ハードウェア\_\_サービス\_IRP の完了                | [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)構造の一部を HwCompleteServiceIrp します。    |
| ハードウェア\_\_トレースの初期化                   | [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)構造の一部を HwInitializeTracing します。     |
| ハードウェア\_クリーンアップ\_トレース                      | [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)構造の一部を HwCleanupTracing します。        |
| VIRTUAL\_HW\_\_アダプターの検索                | [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)構造の一部を HwFindAdapter します。           |
| HW\_メッセージ\_シグナル\_割り込み\_ルーチン | [**HwMSInterruptRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_message_signaled_interrupt_routine)                                                                       |

 

 

 





