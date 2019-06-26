---
title: DualView の有効化
description: DualView の有効化
ms.assetid: 7779c74d-2076-419d-94e4-07c36501524e
keywords:
- デュアル WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d769652d019c24f303e5e349933c7dacb091bdc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385675"
---
# <a name="enabling-dualview"></a>DualView の有効化


## <span id="ddk_enabling_dualview_gg"></span><span id="DDK_ENABLING_DUALVIEW_GG"></span>


最小限のデュアル実装には、以下を実行してください。

-   ミニポート ドライバーの直前に[ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)戻り値は、新しいビデオ ポート ドライバー エントリ ポイントを呼び出す[ **VideoPortCreateSecondaryDisplay**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportcreatesecondarydisplay)、セカンダリの表示のデバイスの拡張機能を生成します。 セカンダリ デバイス拡張機能では、2 つの新しいプライベート メンバーを追加します。

    1.  デバイスの拡張機能を示すフラグはセカンダリの表示
    2.  プライマリ ディスプレイのデバイスの拡張機能のアドレスを含むポインター
-   ミニポート ドライバーのでは、次の 4 つの変更を行う必要があります[ *HwVidStartIO* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)コールバック ルーチンを示す 4 つの IOCTL 要求に応答する方法を変更します。 次の一覧の 4 番目の項目は、同じ結果を行うための 2 つの方法を表示します。

    1.  応答、 [ **IOCTL\_ビデオ\_マップ\_ビデオ\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_map_video_memory) 、各ビューのフレーム バッファー ポインターと長さである要求の内容が正しく設定します。
    2.  応答、 [ **IOCTL\_ビデオ\_設定\_現在\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_set_current_mode)要求をできるように特定のセカンダリ ビュー。
    3.  応答、 [ **IOCTL\_ビデオ\_リセット\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)要求は、デバイスがプライマリまたはセカンダリの表示がかどうかによって異なります。 デバイスがプライマリ ディスプレイの場合は、任意の必要な操作を実行します。 デバイスがセカンダリの表示の場合は、ただし、お勧めするアクションを実行しません。
    4.  応答の変更、 [ **IOCTL\_ビデオ\_共有\_ビデオ\_メモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_share_video_memory)要求は、両方のビューの正しいマップを取得します。 注 DirectDraw 実装では、DirectDraw 関数を変更できます[ *DdMapMemory* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory)両方のビューの正しいマップを取得します。
-   ディスプレイ ドライバーは、論理フレーム バッファーのアドレスと物理のビデオ メモリのオフセットの間の調整の考慮する必要があります。 これは、デュアル ビューでプライマリ サーフェスが開始任意の場所メモリ位置の 0 以外のために、DirectDraw 実装にとって特に重要です。 ディスプレイ ドライバーは、情報を入力して DirectDraw を通知する必要があります**pHalInfo -&gt;vmiData.pvPrimary**と**pHalInfo -&gt;vmiData.fpPrimary**適切なビデオ メモリで次のようにオフセットします。処理の[ **DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)します。

### <a name="span-idadditionalimplementationnotesspanspan-idadditionalimplementationnotesspanspan-idadditionalimplementationnotesspanadditional-implementation-notes"></a><span id="Additional_Implementation_Notes"></span><span id="additional_implementation_notes"></span><span id="ADDITIONAL_IMPLEMENTATION_NOTES"></span>その他の実装に関する注意事項

-   [*HwVidInitialize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_initialize)プライマリ デバイス オブジェクトを一度だけ呼び出されます。 この呼び出しでは、すべてのセカンダリ デバイス オブジェクトを初期化する必要があります。

-   [ **DrvAssertMode** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)を呼び出す*bEnable*に設定されている**FALSE**、ミニポート ドライバーは、他のビューの状態を確認する必要があります。 他のビューがアクティブなまま中に、ビデオのチップをオフにすることを避ける必要があります。

-   描画操作に同じ描画コンテキスト (たとえば、色深度と stride) があることを想定しないでください。 これは、タイル フレーム バッファーを使用するチップの特に重要です。

-   GDI は、組み込みデバイスのプライマリ ビューにのみ設定できます。 ラップトップ コンピューターなど、一部のシステムでは、組み込み監視デバイス (Lcd) があるが外部モニターにも接続されていることができます。 ミニポート ドライバーは、ビデオを渡すことによってリムーバブルとビューをマークする必要があります\_デュアル\_REMOVABLE フラグを呼び出すときに[ **VideoPortCreateSecondaryDisplay**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportcreatesecondarydisplay)します。

-   デュアル モードのラップトップ コンピューターには、ホットキー スイッチを無効にする必要があります。 ビデオの ACPI 対応システムで、ミニポート ドライバーを拒否すべき[ **IOCTL\_ビデオ\_検証\_子\_状態\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_validate_child_state_configuration)要求。

-   Multichild デバイスをサポートしているラップトップ コンピューターのミニポート ドライバーを処理する必要があります[ **IOCTL\_ビデオ\_取得\_子\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)要求と戻り値の論理上の子のリレーションシップ (次のセクションで説明します)。

 

 





