---
title: デバイス ノードの状態フラグ
description: デバイス ノードの状態フラグ
ms.assetid: 64f4548f-ace3-440c-8a36-97bd46cfa986
keywords:
- プラグ アンド プレイ (PnP)、デバイス ノードの状態フラグします。
- デバイス ノードの状態フラグ
- DNF_XXX
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 256ad7a90f2bab282b98f16bb4f5e152e84aae98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560648"
---
# <a name="device-node-status-flags"></a>デバイス ノードの状態フラグ


## <span id="ddk_device_node_status_flags_dbg"></span><span id="DDK_DEVICE_NODE_STATUS_FLAGS_DBG"></span>


デバイス ノードの状態フラグには、デバイスの状態について説明します。

最も重要なフラグは次のとおりです。

<span id="DNF_MADEUP__0x00000001_"></span><span id="dnf_madeup__0x00000001_"></span><span id="DNF_MADEUP__0X00000001_"></span>**DNF\_MADEUP (0x00000001)**  
デバイスが作成されており、PnP マネージャーが所有します。 これは、バス ドライバーでは作成されませんでした。

<span id="DNF_DUPLICATE__0x00000002_"></span><span id="dnf_duplicate__0x00000002_"></span><span id="DNF_DUPLICATE__0X00000002_"></span>**DNF\_DUPLICATE (0x00000002)**  
[デバイス] ノードでは、列挙されたデバイスの別のノードと重複しています。

<span id="DNF_HAL_NODE__0x00000004_"></span><span id="dnf_hal_node__0x00000004_"></span><span id="DNF_HAL_NODE__0X00000004_"></span>**DNF\_HAL\_NODE (0x00000004)**  
[デバイス] ノードでは、ハードウェア アブストラクション レイヤー (HAL) によって作成されたルート ノードです。

<span id="DNF_REENUMERATE__0x00000008_"></span><span id="dnf_reenumerate__0x00000008_"></span><span id="DNF_REENUMERATE__0X00000008_"></span>**DNF\_REENUMERATE (0x00000008)**  
デバイスは再列挙する必要があります。

<span id="DNF_ENUMERATED__0x00000010_"></span><span id="dnf_enumerated__0x00000010_"></span><span id="DNF_ENUMERATED__0X00000010_"></span>**DNF\_ENUMERATED (0x00000010)**  
デバイスの PDO は、その親によって公開されています。

<span id="DNF_IDS_QUERIED__0x00000020_"></span><span id="dnf_ids_queried__0x00000020_"></span><span id="DNF_IDS_QUERIED__0X00000020_"></span>**DNF\_IDS\_QUERIED (0x00000020)**  
オペレーティング システムは IRP を送信する必要があります\_MN\_クエリ\_デバイス ドライバーへの要求の ID。

<span id="DNF_HAS_BOOT_CONFIG__0x00000040_"></span><span id="dnf_has_boot_config__0x00000040_"></span><span id="DNF_HAS_BOOT_CONFIG__0X00000040_"></span>**DNF\_HAS\_BOOT\_CONFIG (0x00000040)**  
デバイスでは、BIOS で割り当てられたリソースがあります。 デバイスと見なされます擬似開始し、再均衡化に参加する必要があります。

<span id="DNF_BOOT_CONFIG_RESERVED__0x00000080_"></span><span id="dnf_boot_config_reserved__0x00000080_"></span><span id="DNF_BOOT_CONFIG_RESERVED__0X00000080_"></span>**DNF\_BOOT\_CONFIG\_RESERVED (0x00000080)**  
デバイスのブート リソースが予約されています。

<span id="DNF_NO_RESOURCE_REQUIRED__0x00000100_"></span><span id="dnf_no_resource_required__0x00000100_"></span><span id="DNF_NO_RESOURCE_REQUIRED__0X00000100_"></span>**DNF\_いいえ\_リソース\_REQUIRED (0x00000100)**  
デバイスでは、リソースは必要ありません。

<span id="DNF_RESOURCE_REQUIREMENTS_NEED_FILTERED__0x00000200_"></span><span id="dnf_resource_requirements_need_filtered__0x00000200_"></span><span id="DNF_RESOURCE_REQUIREMENTS_NEED_FILTERED__0X00000200_"></span>**DNF\_リソース\_要件\_必要\_フィルター (0x00000200)**  
デバイスのリソース要件の一覧は、フィルター処理された一覧を示します。

<span id="DNF_RESOURCE_REQUIREMENTS_CHANGED__0x00000400_"></span><span id="dnf_resource_requirements_changed__0x00000400_"></span><span id="DNF_RESOURCE_REQUIREMENTS_CHANGED__0X00000400_"></span>**DNF\_リソース\_要件\_CHANGED (0x00000400)**  
デバイスのリソース要件の一覧が変更されました。

<span id="DNF_NON_STOPPED_REBALANCE__0x00000800_"></span><span id="dnf_non_stopped_rebalance__0x00000800_"></span><span id="DNF_NON_STOPPED_REBALANCE__0X00000800_"></span>**DNF\_NON\_STOPPED\_REBALANCE (0x00000800)**  
デバイスは、新しいリソースに停車しなくても再開できます。

<span id="DNF_LEGACY_DRIVER__0x00001000_"></span><span id="dnf_legacy_driver__0x00001000_"></span><span id="DNF_LEGACY_DRIVER__0X00001000_"></span>**DNF\_LEGACY\_DRIVER (0x00001000)**  
デバイスの制御のドライバーは、非 PnP ドライバーです。

<span id="DNF_HAS_PROBLEM__0x00002000_"></span><span id="dnf_has_problem__0x00002000_"></span><span id="DNF_HAS_PROBLEM__0X00002000_"></span>**DNF\_HAS\_PROBLEM (0x00002000)**  
デバイスは、問題が発生し、削除されます。

<span id="DNF_HAS_PRIVATE_PROBLEM__0x00004000_"></span><span id="dnf_has_private_problem__0x00004000_"></span><span id="DNF_HAS_PRIVATE_PROBLEM__0X00004000_"></span>**DNF\_HAS\_PRIVATE\_PROBLEM (0x00004000)**  
デバイスの報告 PNP\_デバイス\_も PNP を報告せずに失敗しました\_デバイス\_リソース\_要件\_変更されました。

<span id="DNF_HARDWARE_VERIFICATION__0x00008000_"></span><span id="dnf_hardware_verification__0x00008000_"></span><span id="DNF_HARDWARE_VERIFICATION__0X00008000_"></span>**DNF\_ハードウェア\_(0x00008000) の検証**  
[デバイス] ノードでは、ハードウェアの検証があります。

<span id="DNF_DEVICE_GONE__0x00010000_"></span><span id="dnf_device_gone__0x00010000_"></span><span id="DNF_DEVICE_GONE__0X00010000_"></span>**DNF\_DEVICE\_GONE (0x00010000)**  
IRP では、デバイスの PDO は返されなく\_クエリ\_関係要求。

<span id="DNF_LEGACY_RESOURCE_DEVICENODE__0x00020000_"></span><span id="dnf_legacy_resource_devicenode__0x00020000_"></span><span id="DNF_LEGACY_RESOURCE_DEVICENODE__0X00020000_"></span>**DNF\_LEGACY\_RESOURCE\_DEVICENODE (0x00020000)**  
[デバイス] ノードは、従来のリソースの割り当てに作成されました。

<span id="DNF_NEEDS_REBALANCE__0x00040000_"></span><span id="dnf_needs_rebalance__0x00040000_"></span><span id="DNF_NEEDS_REBALANCE__0X00040000_"></span>**DNF\_NEEDS\_REBALANCE (0x00040000)**  
[デバイス] ノードの再調整がトリガーされます。

<span id="DNF_LOCKED_FOR_EJECT__0x00080000_"></span><span id="dnf_locked_for_eject__0x00080000_"></span><span id="DNF_LOCKED_FOR_EJECT__0X00080000_"></span>**DNF\_LOCKED\_FOR\_EJECT (0x00080000)**  
デバイスが排出されるか、排出されるデバイスに関連します。

<span id="DNF_DRIVER_BLOCKED__0x00100000_"></span><span id="dnf_driver_blocked__0x00100000_"></span><span id="DNF_DRIVER_BLOCKED__0X00100000_"></span>**DNF\_DRIVER\_BLOCKED (0x00100000)**  
読み込みを 1 つまたは複数のデバイス ノードのドライバーがブロックされています。

<span id="DNF_CHILD_WITH_INVALID_ID__0x00200000_"></span><span id="dnf_child_with_invalid_id__0x00200000_"></span><span id="DNF_CHILD_WITH_INVALID_ID__0X00200000_"></span>**DNF\_CHILD\_WITH\_INVALID\_ID (0x00200000)**  
[デバイス] ノードの 1 つまたは複数の子が無効な Id を持ちます。

<span id="DNF_ASYNC_START_NOT_SUPPORTED__0x00400000_"></span><span id="dnf_async_start_not_supported__0x00400000_"></span><span id="DNF_ASYNC_START_NOT_SUPPORTED__0X00400000_"></span>**DNF\_ASYNC\_START\_NOT\_SUPPORTED (0x00400000)**  
デバイスは、非同期の開始をサポートしていません。

<span id="DNF_ASYNC_ENUMERATION_NOT_SUPPORTED__0x00800000_"></span><span id="dnf_async_enumeration_not_supported__0x00800000_"></span><span id="DNF_ASYNC_ENUMERATION_NOT_SUPPORTED__0X00800000_"></span>**DNF\_ASYNC\_ENUMERATION\_NOT\_SUPPORTED (0x00800000)**  
デバイスは、非同期列挙をサポートしていません。

<span id="DNF_LOCKED_FOR_REBALANCE__0x01000000_"></span><span id="dnf_locked_for_rebalance__0x01000000_"></span><span id="DNF_LOCKED_FOR_REBALANCE__0X01000000_"></span>**DNF\_LOCKED\_FOR\_REBALANCE (0x01000000)**  
負荷を分散、デバイスがロックされています。

<span id="DNF_UNINSTALLED__0x02000000_"></span><span id="dnf_uninstalled__0x02000000_"></span><span id="DNF_UNINSTALLED__0X02000000_"></span>**DNF\_UNINSTALLED (0x02000000)**  
IRP\_MN\_クエリ\_削除\_デバイス要求がデバイスの進行中です。

<span id="DNF_NO_LOWER_DEVICE_FILTERS__0x04000000_"></span><span id="dnf_no_lower_device_filters__0x04000000_"></span><span id="DNF_NO_LOWER_DEVICE_FILTERS__0X04000000_"></span>**DNF\_NO\_LOWER\_DEVICE\_FILTERS (0x04000000)**  
デバイスの低いデバイス フィルターの種類のレジストリ エントリはありません。

<span id="DNF_NO_LOWER_CLASS_FILTERS__0x08000000_"></span><span id="dnf_no_lower_class_filters__0x08000000_"></span><span id="DNF_NO_LOWER_CLASS_FILTERS__0X08000000_"></span>**DNF\_いいえ\_低い\_クラス\_フィルター (0x08000000)**  
デバイスの下位のフィルター クラス型のレジストリ エントリはありません。

<span id="DNF_NO_SERVICE__0x10000000_"></span><span id="dnf_no_service__0x10000000_"></span><span id="DNF_NO_SERVICE__0X10000000_"></span>**DNF\_いいえ\_サービス (0x10000000)**  
サービスのレジストリ エントリがない、デバイスにします。

<span id="DNF_NO_UPPER_DEVICE_FILTERS__0x20000000_"></span><span id="dnf_no_upper_device_filters__0x20000000_"></span><span id="DNF_NO_UPPER_DEVICE_FILTERS__0X20000000_"></span>**DNF\_いいえ\_上限\_デバイス\_フィルター (0x20000000)**  
デバイスの上限デバイス フィルターの種類のレジストリ エントリはありません。

<span id="DNF_NO_UPPER_CLASS_FILTERS__0x40000000_"></span><span id="dnf_no_upper_class_filters__0x40000000_"></span><span id="DNF_NO_UPPER_CLASS_FILTERS__0X40000000_"></span>**DNF\_いいえ\_上限\_クラス\_フィルター (0x40000000)**  
デバイスのフィルター処理クラス上の型のレジストリ エントリはありません。

<span id="DNF_WAITING_FOR_FDO__0x80000000_"></span><span id="dnf_waiting_for_fdo__0x80000000_"></span><span id="DNF_WAITING_FOR_FDO__0X80000000_"></span>**DNF\_WAITING\_FOR\_FDO (0x80000000)**  
デバイスの列挙体は、ドライバーがその FDO がアタッチされるまでに待機しています。

 

 





