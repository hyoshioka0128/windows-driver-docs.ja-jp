---
title: システム定義の IOCTL_VIDEO_XXX 要求
description: システム定義の IOCTL_VIDEO_XXX 要求
ms.assetid: 30309de1-c991-402d-a701-7e88c3367d24
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、要求の処理
- 要求処理の WDK ビデオのミニポート
- I/O WDK ビデオのミニポート
- システム定義の IOCTL_VIDEO_XXX 要求 WDK ビデオのミニポート
- IOCTL_VIDEO_XXX 要求 WDK のビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6079c34645379d4a052b24faad76a28b6c7904b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372051"
---
# <a name="system-defined-ioctlvideoxxx-requests"></a>システム定義の IOCTL\_ビデオ\_XXX 要求


## <span id="ddk_system_defined_ioctl_video_xxx_requests_gg"></span><span id="DDK_SYSTEM_DEFINED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


通常、ほとんどのビデオのミニポート ドライバーでは、次の要求をサポートします。

[**IOCTL\_ビデオ\_クエリ\_NUM\_利用\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_num_avail_modes)

[**IOCTL\_ビデオ\_クエリ\_利用\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_avail_modes)

[**IOCTL\_ビデオ\_クエリ\_現在\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_current_mode)

[**IOCTL\_VIDEO\_SET\_CURRENT\_MODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_current_mode)

[**IOCTL\_VIDEO\_RESET\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)

[**IOCTL\_ビデオ\_マップ\_ビデオ\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_map_video_memory)

[**IOCTL\_ビデオ\_UNMAP\_ビデオ\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_unmap_video_memory)

[**IOCTL\_ビデオ\_共有\_ビデオ\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_share_video_memory)

[**IOCTL\_ビデオ\_共有解除\_ビデオ\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_unshare_video_memory)

[**IOCTL\_ビデオ\_クエリ\_パブリック\_アクセス\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_public_access_ranges)

[**IOCTL\_ビデオ\_FREE\_パブリック\_アクセス\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_free_public_access_ranges)

[**IOCTL\_ビデオ\_取得\_POWER\_管理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_get_power_management)

[**IOCTL\_ビデオ\_設定\_POWER\_管理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_power_management)

[**IOCTL\_ビデオ\_取得\_子\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)

[**IOCTL\_ビデオ\_設定\_子\_状態\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_child_state_configuration)

[**IOCTL\_ビデオ\_検証\_子\_状態\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_validate_child_state_configuration)

ビデオのミニポート ドライバーは、アダプターの機能に応じて、次の追加の要求をサポートできます。

[**IOCTL\_ビデオ\_クエリ\_色\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_color_capabilities)

[**IOCTL\_ビデオ\_設定\_色\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_color_registers) (デバイスがパレットがかどうかに必要)

[**IOCTL\_ビデオ\_を無効にする\_ポインター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_pointer)

[**IOCTL\_ビデオ\_を有効にする\_ポインター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_pointer)

[**IOCTL\_ビデオ\_クエリ\_ポインター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_capabilities)

[**IOCTL\_ビデオ\_クエリ\_ポインター\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_attr)

[**IOCTL\_ビデオ\_設定\_ポインター\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_attr)

[**IOCTL\_ビデオ\_クエリ\_ポインター\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_position)

[**IOCTL\_ビデオ\_設定\_ポインター\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_position)

[**IOCTL\_VIDEO\_HANDLE\_VIDEOPARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)

[**IOCTL\_ビデオ\_スイッチ\_デュアル ビュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_switch_dualview)

次の追加の要求をサポートするためには、VGA と互換性のある SVGA ミニポート ドライバーが必要です。

[**IOCTL\_ビデオ\_保存\_ハードウェア\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_save_hardware_state)

[**IOCTL\_ビデオ\_復元\_ハードウェア\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_restore_hardware_state)

[**IOCTL\_ビデオ\_を無効にする\_カーソル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_cursor)

[**IOCTL\_ビデオ\_を有効にする\_カーソル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_cursor)

[**IOCTL\_ビデオ\_クエリ\_カーソル\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_attr)

[**IOCTL\_VIDEO\_SET\_CURSOR\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_attr)

[**IOCTL\_ビデオ\_クエリ\_カーソル\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_position)

[**IOCTL\_ビデオ\_設定\_カーソル\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_position)

[**IOCTL\_VIDEO\_GET\_BANK\_SELECT\_CODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_get_bank_select_code)

[**IOCTL\_ビデオ\_設定\_パレット\_を登録します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_palette_registers)

[**IOCTL\_ビデオ\_ロード\_AND\_設定\_フォント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_load_and_set_font)

見つかる各 IOCTL の詳細に[ビデオのミニポート ドライバー I/O 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 ミニポート ドライバー開発者は、ドキュメントに未記載のシステム定義の Ioctl には使用しないでください。

 

 





