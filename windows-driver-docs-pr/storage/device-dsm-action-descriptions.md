---
title: DEVICE_DSM_ACTION の説明
description: このページでは、デバイスのデータセット属性に対してデータセット管理 (DSM) アクションを実行するために使用できる DEVICE_DSM_ACTION 定数について説明します。
ms.assetid: cc64c7ad-7d1c-45c7-b236-a43e57086f8d
keywords: ストレージデータセット管理アクション、データセット管理アクション、DSM アクション
ms.localizationpriority: medium
ms.date: 08/23/2019
ms.openlocfilehash: 6512edac830ec92a702e5b962be6c73abc0c7c6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845179"
---
# <a name="device_dsm_action-descriptions"></a>DEVICE_DSM_ACTION の説明

このページでは、デバイスのデータセットに対してデータセット管理 (DSM) アクションを実行するために使用できる DEVICE_DSM_ACTION 定数について説明します。 これらの定数は、 *ntddstor*で定義されています。 非破壊として識別されたアクションは、データを変更しません。 DSM アクションの処理方法の詳細については、「[データセット管理の概要](data-set-management-overview.md)」を参照してください。

| DEVICE_DSM_ACTION 定数 | 説明 |
| -------------------------- | ----------- |
| **DeviceDsmAction_None** | 構造体の初期化のみを目的としています。 |
| **DeviceDsmAction_Trim** | ドライバーは、トリミング操作を実行します。 |
| **DeviceDsmAction_Notification** | 損なわ. ドライバーは、通知操作を実行します。 このアクションでは、 [DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)構造体の直後にあるパラメーターブロックが[DEVICE_DSM_NOTIFICATION_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_dsm_notification_parameters)構造体として書式設定されます。 Windows 7 以降のバージョンでサポートされています。 |
| **DeviceDsmAction_OffloadRead** | 損なわ. ドライバーは、オフロード読み取り操作を実行します。 このアクションでは、 [DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)構造体の直後にあるパラメーターブロックが[DEVICE_DSM_OFFLOAD_READ_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_dsm_offload_read_parameters)構造体として書式設定されます。 出力は、 [DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)構造体の後に[STORAGE_OFFLOAD_READ_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_offload_read_output)構造体で構成されます。 Windows 8 以降のバージョンでサポートされています。 |
| **DeviceDsmAction_OffloadWrite** | ドライバーは、オフロード書き込み操作を実行します。 このアクションでは、 [DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)構造体の直後にあるパラメーターブロックが[DEVICE_DSM_OFFLOAD_WRITE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_dsm_offload_write_parameters)構造体として書式設定されます。 出力は、 [DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)構造体の後に[STORAGE_OFFLOAD_WRITE_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_offload_write_output)構造体で構成されます。 Windows 8 以降のバージョンでサポートされています。 |
| **DeviceDsmAction_Allocation** | 損なわ. ドライバーは、論理ブロックのプロビジョニング操作を実行します。 論理ブロック範囲は、1つの[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_data_set_range)構造体で指定されます。 Windows 8 以降のバージョンでサポートされています。 |
| **DeviceDsmAction_Repair** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_Scrub** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_DrtQuery** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_DrtClear** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_DrtDisable** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_TieringQuery** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_Map** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_RegenerateParity** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_NvCache_Change_Priority** | 損なわ. ドライバーは、指定された論理ブロックの範囲のキャッシュ優先度を変更します。 新しいターゲットの優先順位は、 [DEVICE_DSM_NVCACHE_CHANGE_PRIORITY_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_dsm_nvcache_change_priority_parameters)構造体で設定されます。これは、 [DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)構造体の直後にあるパラメーターブロックに配置されます。 優先順位を変更する論理ブロック範囲は、1つまたは複数の[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_data_set_range)構造体で指定されます。 Windows 8.1 以降のバージョンでサポートされています。 |
| **DeviceDsmAction_NvCache_Evict** | 損なわ. ドライバーは、キャッシュメディアからデータを削除します。 すべてのデータを削除するには、 [DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)の**FLAGS**メンバーに DEVICE_DSM_FLAG_ENTIRE_DATA_SET_RANGE フラグを設定し、 [DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_data_set_range)構造体を含めないようにします。 削除する特定の論理ブロック範囲は、1つまたは複数の[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_data_set_range)構造体で指定されます。 **DeviceDsmAction_NvCache_Evict**アクションは同期的に実行されます。 削除アクションが成功するか失敗するまで、他のアクションは処理されません。 デバイスを使用するアプリケーションへの影響を制限するために、発行される各**DeviceDsmAction_NvCache_Evict** action には比較的小さなデータ範囲が含まれている必要があります。 10 MB を超えないようにし、理想的には 2 MB よりも小さくする必要があります。 これにより、デバイス上のデータにアクセスするときに、ユーザーレベルのアプリケーションで顕著な遅延が発生する可能性が最小限に抑えられます。 Windows 8.1 以降のバージョンでサポートされています。 |
| **DeviceDsmAction_TopologyIdQuery** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_GetPhysicalAddresses** | 損なわ. ドライバーは、1つまたは複数の論理ブロックの範囲に対応する物理アドレスの範囲を返します。 この操作は、永続メモリディスクでのみサポートされています。 論理ブロック範囲は、DEVICE_DSM_INPUT 構造体の直後に一連の[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_data_set_range)構造体として指定されます。 出力は[DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)構造体で構成され、その後にパディングが続き、出力ブロックで要求された物理アドレス範囲を持つ[DEVICE_DSM_PHYSICAL_ADDRESSES_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_dsm_physical_addresses_output)構造体になります。 各物理アドレス範囲は、 [DEVICE_STORAGE_ADDRESS_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_storag_address_range)構造体で返されます。 出力バッファーの大きさが不十分ですべてのデータを保持できない場合、DSM は STATUS_BUFFER_OVERFLOW を返し、DEVICE_DSM_PHYSICAL_ADDRESSES_OUTPUT 構造体の**TotalNumberOfRanges**フィールドには DEVICE_STORAGE_ADDRESS_RANGE の数が含まれます。要求を満たすために必要な要素。 メモリエラーが含まれている物理アドレスの範囲には、そのアドレスとして DEVICE_DSM_PHYSICAL_ADDRESS_HAS_MEMORY_ERROR があります。 返された物理アドレス範囲は、返された各物理アドレス範囲の長さを追跡することによって、入力論理ブロック範囲にマップできます。 1つの論理ブロック範囲は、多数の物理アドレス範囲に対応できることに注意してください。 DEVICE_DSM_FLAG_PHYSICAL_ADDRESSES_OMIT_TOTAL_RANGES が[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)構造体の**Flags**フィールドで設定されている場合、ドライバーは**TotalNumberOfRanges**を計算しません。 これは、範囲の合計数を知る必要がない呼び出し元のパフォーマンスの最適化です。 |
| **DeviceDsmAction_ScopeRegen** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_ReportZones** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_OpenZone** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_FinishZone** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_CloseZone** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_ResetWritePointer** | 内部使用専用。 |
| **DeviceDsmAction_GetRangeErrorInfo** | 損なわ. ドライバーは、1つまたは複数の論理ブロック範囲にメディアエラーが含まれているかどうかに関する情報を返します。 これは、永続メモリディスクでのみサポートされています。 論理ブロック範囲は、 [DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)構造体の直後に一連の[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_data_set_range)構造体として指定されます。 出力は、 [DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)構造体と、 [DEVICE_STORAGE_RANGE_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_storage_range_attributes)の配列を保持するパディングと[DEVICE_DSM_RANGE_ERROR_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_dsm_range_error_output)) 構造で構成されます。 出力バッファーの大きさが不十分ですべてのデータを保持できない場合、DSM は STATUS_BUFFER_OVERFLOW を返し、DEVICE_DSM_RANGE_ERROR_OUTPUT 構造体の**TotalNumberOfRanges**フィールドには DEVICE_STORAGE_RANGE_ATTRIBUTES 要素の数が含まれます。要求を満たすために必要です。 各 DEVICE_STORAGE_RANGE_ATTRIBUTES 構造体には、 **Israngebad**フィールドが含まれています。 論理ブロック範囲にメディアエラーが含まれている場合、ドライバーはそのフィールドを1に設定します。 要求されたいずれかの範囲にメディアエラーがない場合、ドライバーは DEVICE_DSM_RANGE_ERROR_OUTPUT の Flags フィールドに DEVICE_STORAGE_NO_ERRORS を設定します。 DEVICE_STORAGE_RANGE_ATTRIBUTES 配列の要素は、順序が入力範囲の順序に対応するように並べ替えられます。 たとえば、最初の入力範囲が3つの出力範囲に分割された場合、配列内の最初の3つの範囲になります。 呼び出し元は、出力範囲の長さを追跡することによって、入力範囲に対応する出力範囲を知ることができます。 |
| **DeviceDsmAction_WriteZeroes** | 内部使用専用。 |
| **DeviceDsmAction_LostQuery** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_GetFreeSpace** | 損なわ. 内部使用専用。 |
| **DeviceDsmAction_ConversionQuery** | 損なわ. 内部使用専用。 |
