---
title: デュアルビューの有効化
description: デュアルビューの有効化
ms.assetid: 7779c74d-2076-419d-94e4-07c36501524e
keywords:
- デュアルビュー WDK ビデオミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7192a93d4a366a69ad350cf14eee0d3b81ea1652
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838957"
---
# <a name="enabling-dualview"></a>デュアルビューの有効化


## <span id="ddk_enabling_dualview_gg"></span><span id="DDK_ENABLING_DUALVIEW_GG"></span>


最小限のデュアルビュー実装の場合は、次の操作を実行します。

-   ミニポートドライバーの[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)が返される直前に、新しいビデオポートドライバーのエントリポイントである[**VideoPortCreateSecondaryDisplay**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcreatesecondarydisplay)を呼び出して、セカンダリビューのデバイス拡張機能を生成します。 セカンダリデバイス拡張機能で、2つの新しいプライベートメンバーを追加します。

    1.  デバイスの拡張機能がセカンダリディスプレイ用であることを示すフラグ
    2.  プライマリディスプレイのデバイス拡張機能のアドレスを格納しているポインター。
-   ミニポートドライバーの[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)コールバックルーチンで4つの変更を行う必要があります。この場合、表示される4つの IOCTL 要求に対する応答方法を変更します。 次の4番目の項目は、同じ結果を実現する2つの方法を示しています。

    1.  [**IOCTL\_video\_MAP\_video\_MEMORY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_map_video_memory)要求に応答して、各ビューのフレームバッファーポインターと長さが適切に設定されている必要があります。
    2.  現在の\_モード要求\_設定されている[**IOCTL\_VIDEO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_set_current_mode)に対する応答は、セカンダリビューに固有のものにする必要があります。
    3.  デバイスがプライマリとセカンダリのどちらであるかは、 [**IOCTL\_ビデオ\_リセット\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_reset_device)要求に対する応答によって異なります。 デバイスがプライマリディスプレイの場合は、必要な操作を実行します。 ただし、デバイスがセカンダリディスプレイの場合は、アクションを実行しないことをお勧めします。
    4.  両方のビューの正しいマップを取得するには、 [**IOCTL\_video\_SHARE\_video\_MEMORY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_share_video_memory)要求に対する応答を変更します。 DirectDraw の実装では、DirectDraw 関数[*Ddmapmemory*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory)を変更して両方のビューの正しいマップを取得できることに注意してください。
-   ディスプレイドライバーは、論理フレームバッファーアドレスと物理ビデオメモリオフセットとの調整を処理する必要があります。 これは DirectDraw 実装では特に重要です。これは、デュアルビューでは、プライマリサーフェイスがメモリ位置0以外の場所で開始される可能性があるためです。 ディスプレイドライバーは、PHalInfo を入力して DirectDraw に通知する必要があり**ます。 pvprimary**と **&gt;pHalInfo**には、 [**DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)を処理するときの適切なビデオメモリオフセットを使用して、&gt;を入力します。

### <a name="span-idadditional_implementation_notesspanspan-idadditional_implementation_notesspanspan-idadditional_implementation_notesspanadditional-implementation-notes"></a><span id="Additional_Implementation_Notes"></span><span id="additional_implementation_notes"></span><span id="ADDITIONAL_IMPLEMENTATION_NOTES"></span>その他の実装に関する注意事項

-   [*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)は、プライマリデバイスオブジェクトに対して1回だけ呼び出されます。 この呼び出しでは、任意のセカンダリデバイスオブジェクトを初期化する必要があります。

-   *Benable*が**FALSE**に設定されている[**DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)呼び出しの場合、ミニポートドライバーは他のビューの状態を確認する必要があります。 他のビューがアクティブな状態でも、ビデオチップをオフにすることは避けてください。

-   描画操作の描画コンテキストが同じであるとは限りません (色深度や stride など)。 これは、タイルフレームバッファーを使用するチップに特に重要です。

-   GDI は、組み込みデバイスでのみプライマリビューを設定できます。 ラップトップコンピューターなどの一部のシステムには、モニターデバイス (Lcd) が組み込まれていますが、外部モニターに接続することもできます。 ミニポートドライバーは、 [**VideoPortCreateSecondaryDisplay**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcreatesecondarydisplay)を呼び出すときに、ビデオ\_デュアルドライブ\_リムーバブルフラグを渡すことにより、ビューをリムーバブルとしてマークする必要があります。

-   デュアルビューモードのラップトップコンピューターでは、ホットキースイッチを無効にする必要があります。 ビデオ ACPI 対応システムでは、ミニポートドライバーは IOCTL\_ビデオを拒否し、 [ **\_子\_状態\_構成要求を検証\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_validate_child_state_configuration)ます。

-   Multichild デバイスをサポートするラップトップコンピューターの場合、ミニポートドライバーは、子\_状態の要求\_取得し、論理子の関係を返す (次のセクションで説明します) [ **\_IOCTL\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_get_child_state)を処理する必要があります。

 

 





