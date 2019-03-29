---
title: Storport ドライバーの関数役割型を使用した関数の宣言
description: Storport ドライバーを分析する SDV を有効にするには、Storport に対して定義されている関数の役割の型宣言を使用して関数を宣言する必要があります。 関数のロールの種類は、Storport.h で定義されます。
ms.assetid: 40BD11CD-A559-4F90-BF39-4ED2FB800392
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64ecfc2e698591f8e373ed2e76d88cf034561acb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570162"
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
| HW\_初期化                            | [**HwStorInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff557396)                                                                               |
| HW\_BUILDIO                               | [**HwStorBuildIo**](https://msdn.microsoft.com/library/windows/hardware/ff557369)                                                                                     |
| HW\_STARTIO                               | [**HwStorStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff557423)                                                                                     |
| HW\_を中断                             | [**HwStorInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff557403)                                                                                 |
| HW\_タイマー                                 | [**HwStorTimer**](https://msdn.microsoft.com/library/windows/hardware/ff557426)                                                                                         |
| HW\_検索\_アダプター                         | [**HwStorFindAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff557390)                                                                             |
| HW\_リセット\_バス                            | [**HwStorResetBus**](https://msdn.microsoft.com/library/windows/hardware/ff557415)                                                                                   |
| HW\_アダプター\_コントロール                      | [**HwStorAdapterControl**](https://msdn.microsoft.com/library/windows/hardware/ff557365)                                                                       |
| HW\_パッシブ\_初期化\_ルーチン          | [**HwStorPassiveInitializeRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff557407)                                                   |
| HW\_DPC\_ルーチン                          | [**HwStorDpcRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff557383)                                                                               |
| HW\_FREE\_アダプター\_リソース              | 一部を HwFreeAdapterResources、 [**仮想\_HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff568010)構造体。  |
| HW\_プロセス\_サービス\_要求             | 一部を HwProcessServiceRequest、 [**仮想\_HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff568010)構造体。 |
| HW\_完了\_サービス\_IRP                | 一部を HwCompleteServiceIrp、 [**仮想\_HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff568010)構造体。    |
| HW\_初期化\_トレース                   | 一部を HwInitializeTracing、 [**仮想\_HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff568010)構造体。     |
| HW\_クリーンアップ\_トレース                      | 一部を HwCleanupTracing、 [**仮想\_HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff568010)構造体。        |
| 仮想\_HW\_検索\_アダプター                | 一部を HwFindAdapter、 [**仮想\_HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff568010)構造体。           |
| HW\_メッセージ\_シグナルされた\_INTERRUPT\_ルーチン | [**HwMSInterruptRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff557268)                                                                       |

 

 

 





