---
title: Storport ドライバーの関数役割型を使用した関数の宣言
description: Storport ドライバーを分析する SDV を有効にするには、Storport に対して定義されている関数の役割の型宣言を使用して関数を宣言する必要があります。 関数のロールの種類は、Storport.h で定義されます。
ms.assetid: 40BD11CD-A559-4F90-BF39-4ED2FB800392
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ad901f3f8148b928ac3e37eb12af7e07d7019c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371422"
---
# <a name="declaring-functions-by-using-function-role-types-for-storport-drivers"></a>Storport ドライバーの関数役割型を使用した関数の宣言


Storport ドライバーを分析する SDV を有効にするには、Storport に対して定義されている関数の役割の型宣言を使用して関数を宣言する必要があります。 関数のロールの種類は、Storport.h で定義されます。

対応するロールの種類を指定することによって、Storport ドライバー内の各コールバック関数を宣言する必要があります。

次のコード例では、DriverIntialize コールバック関数の関数の役割の型宣言を示します。 関数のロールの種類は sp\_ドライバー\_を初期化します。

```
sp_DRIVER_INITIALIZE DriverEntry;
```

コールバック関数に関数のプロトタイプ宣言がある場合とロールの種類の関数の宣言、関数プロトタイプを置き換える必要があります。

| ロールの種類の関数                        | Storport ルーチン                                                                                                               |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| sp\_ドライバー\_初期化                    | DriverEntry                                                                                                                    |
| HW\_初期化                            | [**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_initialize)                                                                               |
| HW\_BUILDIO                               | [**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)                                                                                     |
| HW\_STARTIO                               | [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)                                                                                     |
| HW\_を中断                             | [**HwStorInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_interrupt)                                                                                 |
| HW\_タイマー                                 | [**HwStorTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_timer)                                                                                         |
| HW\_検索\_アダプター                         | [**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)                                                                             |
| HW\_リセット\_バス                            | [**HwStorResetBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_reset_bus)                                                                                   |
| HW\_アダプター\_コントロール                      | [**HwStorAdapterControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_adapter_control)                                                                       |
| HW\_パッシブ\_初期化\_ルーチン          | [**HwStorPassiveInitializeRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_passive_initialize_routine)                                                   |
| HW\_DPC\_ルーチン                          | [**HwStorDpcRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_dpc_routine)                                                                               |
| HW\_FREE\_アダプター\_リソース              | 一部を HwFreeAdapterResources、 [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)構造体。  |
| HW\_プロセス\_サービス\_要求             | 一部を HwProcessServiceRequest、 [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)構造体。 |
| HW\_完了\_サービス\_IRP                | 一部を HwCompleteServiceIrp、 [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)構造体。    |
| HW\_初期化\_トレース                   | 一部を HwInitializeTracing、 [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)構造体。     |
| HW\_クリーンアップ\_トレース                      | 一部を HwCleanupTracing、 [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)構造体。        |
| 仮想\_HW\_検索\_アダプター                | 一部を HwFindAdapter、 [**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)構造体。           |
| HW\_メッセージ\_シグナルされた\_INTERRUPT\_ルーチン | [**HwMSInterruptRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_message_signaled_interrupt_routine)                                                                       |

 

 

 





