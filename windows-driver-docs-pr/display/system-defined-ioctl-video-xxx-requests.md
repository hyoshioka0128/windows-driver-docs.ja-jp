---
title: システム定義の IOCTL_VIDEO_XXX 要求
description: システム定義の IOCTL_VIDEO_XXX 要求
ms.assetid: 30309de1-c991-402d-a701-7e88c3367d24
keywords:
- ビデオミニポートドライバー WDK Windows 2000、要求の処理
- 要求処理 WDK ビデオミニポート
- I/o WDK ビデオミニポート
- システム定義の IOCTL_VIDEO_XXX requests WDK ビデオミニポート
- IOCTL_VIDEO_XXX が WDK ビデオミニポートを要求する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33bb4fe9a28878c97099c2a6bcf123f569c6097f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825510"
---
# <a name="system-defined-ioctl_video_xxx-requests"></a>システム定義の IOCTL\_ビデオ\_XXX 要求


## <span id="ddk_system_defined_ioctl_video_xxx_requests_gg"></span><span id="DDK_SYSTEM_DEFINED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


通常、ほとんどのビデオミニポートドライバーは、次の要求をサポートしています。

[**IOCTL\_ビデオ\_クエリ\_NUM\_利用可能\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_num_avail_modes)

[**IOCTL\_ビデオ\_クエリ\_利用可能\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_avail_modes)

[**IOCTL\_ビデオ\_クエリ\_現在の\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_current_mode)

[**現在の\_モード\_設定した IOCTL\_ビデオ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_current_mode)

[**IOCTL\_ビデオ\_リセット\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)

[**ビデオ\_マップ\_ビデオ\_メモリを\_IOCTL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_map_video_memory)

[**IOCTL\_ビデオ\_\_ビデオ\_メモリのマップ解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_unmap_video_memory)

[**ビデオ\_共有\_ビデオ\_メモリ\_IOCTL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_share_video_memory)

[**IOCTL\_ビデオ\_\_ビデオ\_メモリの共有を解除する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_unshare_video_memory)

[**IOCTL\_ビデオ\_クエリ\_パブリック\_アクセス\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_public_access_ranges)

[**IOCTL\_VIDEO\_無料\_パブリック\_アクセス\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_free_public_access_ranges)

[**IOCTL\_ビデオ\_\_電源\_管理を取得する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_power_management)

[**IOCTL\_ビデオ\_設定\_電源\_管理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_power_management)

[ **\_子\_状態を取得\_ための IOCTL\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)

[**IOCTL\_ビデオ\_設定\_子\_状態\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_child_state_configuration)

[ **\_子\_状態\_構成を検証するための IOCTL\_ビデオ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_validate_child_state_configuration)

アダプターの機能に応じて、ビデオミニポートドライバーは次の追加の要求をサポートできます。

[**IOCTL\_ビデオ\_クエリ\_カラー\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_color_capabilities)

[**IOCTL\_ビデオ\_設定\_色\_レジスタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_color_registers)(デバイスにパレットがある場合は必須)

[**IOCTL\_ビデオ\_\_ポインターを無効にする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_pointer)

[ **\_ポインターを有効にするための IOCTL\_ビデオ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_pointer)

[**IOCTL\_ビデオ\_クエリ\_ポインター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_capabilities)

[**IOCTL\_VIDEO\_クエリ\_ポインター\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_attr)

[**IOCTL\_VIDEO\_SET\_ポインター\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_attr)

[**IOCTL\_ビデオ\_クエリ\_ポインター\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_pointer_position)

[**ポインター\_位置\_設定する IOCTL\_ビデオ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_pointer_position)

[**VIDEOPARAMETERS\_の IOCTL\_ビデオ\_ハンドル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)

[**IOCTL\_ビデオ\_スイッチ\_デュアルビュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_switch_dualview)

次の追加の要求をサポートするには、VGA と互換性のある SVGA ミニポートドライバーが必要です。

[**IOCTL\_ビデオ\_\_ハードウェア\_状態の保存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_save_hardware_state)

[**IOCTL\_VIDEO\_RESTORE\_ハードウェア\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_restore_hardware_state)

[**IOCTL\_ビデオ\_\_カーソルを無効にする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_disable_cursor)

[ **\_カーソルを有効にするための IOCTL\_ビデオ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_enable_cursor)

[**IOCTL\_VIDEO\_QUERY\_CURSOR\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_attr)

[**IOCTL\_VIDEO\_SET\_CURSOR\_ATTR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_attr)

[**IOCTL\_ビデオ\_クエリ\_カーソル\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_cursor_position)

[**カーソル\_位置\_設定する IOCTL\_ビデオ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_cursor_position)

[**IOCTL\_ビデオ\_\_銀行を取得\_\_コードを選択する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_bank_select_code)

[ **\_パレット\_レジスタに設定した IOCTL\_ビデオ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_palette_registers)

[**IOCTL\_ビデオ\_読み込み\_および\_設定\_フォント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_load_and_set_font)

各 IOCTL の詳細については、「[ビデオミニポートドライバーの I/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。 ミニポートドライバーのライターは、ドキュメントに記載されていないシステム定義の Ioctl を使用しないでください。

 

 





