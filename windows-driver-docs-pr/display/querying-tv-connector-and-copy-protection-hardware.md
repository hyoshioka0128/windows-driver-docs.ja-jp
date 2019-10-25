---
title: テレビ コネクタおよびコピー防止ハードウェアのクエリ
description: テレビ コネクタおよびコピー防止ハードウェアのクエリ
ms.assetid: 7812a3ba-42f1-4872-bfe8-08933802f0c1
keywords:
- TV コネクタ WDK ビデオミニポート
- コピー防止 WDK ビデオミニポート、クエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b475722e3bb701783d400cb1631334714fb4d8e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829653"
---
# <a name="querying-tv-connector-and-copy-protection-hardware"></a>テレビ コネクタおよびコピー防止ハードウェアのクエリ


## <span id="ddk_querying_tv_connector_and_copy_protection_hardware_gg"></span><span id="DDK_QUERYING_TV_CONNECTOR_AND_COPY_PROTECTION_HARDWARE_GG"></span>


TV コネクタがあるアダプターのビデオミニポートドライバーは、 [*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)関数の VIDEOPARAMETERS 要求\_処理するために、 [**IOCTL\_\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)を処理する必要があります。 IOCTL 要求が\_ビデオ\_ハンドル\_VIDEOPARAMETERS を処理する場合、 [**video\_要求\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)構造の**InputBuffer**メンバーは[**VIDEOPARAMETERS**](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)構造体を指します。 VIDEOPARAMETERS 構造体の**Dwcommand**メンバーは、ミニポートドライバーが tv コネクタ (VP\_コマンド\_GET) に関する情報を提供する必要があるかどうか、または指定された設定をテレビコネクタ (VP\_コマンドに適用するかどうかを指定し @no__ の設定)。

VIDEOPARAMETERS 構造体の**Dwcommand**メンバーが VP\_COMMAND\_GET の場合、ミニポートドライバーは次の操作を行う必要があります。

-   VIDEOPARAMETERS 構造体の**Guid**メンバーを確認します。

-   TV コネクタがサポートする機能ごとに、VIDEOPARAMETERS 構造体の**dwFlags**メンバーに対応するフラグを設定します。

-   **DwFlags**メンバーで設定されている各フラグについて、VIDEOPARAMETERS 構造体の対応するメンバーに値を割り当てて、そのフラグに関連付けられている機能と現在の設定を示します。 特定のフラグに対応する構造体メンバーの一覧については、 [**VIDEOPARAMETERS**](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)のリファレンスページを参照してください。

VIDEOPARAMETERS 構造体の**Dwmode**メンバーは、テレビ出力をビデオ再生用に最適化するか、Windows デスクトップを表示するかを指定します。 ビデオ\_モードの値\_テレビ\_再生では、テレビ出力がビデオ再生用に最適化されていることを指定します (つまり、ちらつきフィルターが無効になっており、オーバースキャンが有効になっています)。 [ビデオ\_モード] の値\_WIN\_グラフィックスは、テレビ出力が Windows グラフィックス用に最適化されていることを指定します (つまり、最大のちらつきフィルターが有効で、オーバースキャンが無効になっています)。

VP\_コマンド\_GET の応答として、ミニポートドライバーで VP\_フラグ\_TV\_MODE フラグを設定する必要があります **。また、** **dwAvailableModes**で VP\_モード\_WIN\_GRAPHICS ビットに設定する必要があります。 **DwAvailableModes**で\_\_モードを TV\_再生ビットに設定することは任意です。 さらに、ミニポートドライバーでは、\_\_フラグを設定する必要があります。このフラグは、 **dwFlags**では最大\_スケーリングされていません。また、VIDEOPARAMETERS 構造体の対応するメンバーに値を割り当てる必要があります。

VP\_コマンド\_GET の応答として、TV 出力が現在無効になっている場合は、ミニポートドライバーで**Dwmode**を0に設定し、 **dwTVStandard**を VP\_STANDARD\_WIN\_VGA に設定して、 **Dwmode ab vstandard を設定する必要があります。** VP\_STANDARD\_WIN\_VGA に勝利します。

例 1: アダプターが TV 出力をサポートしています。これは現在無効になっています。 ミニポートドライバーは、VP\_コマンド\_GET に応答して、次の操作を行う必要があります。

-   **DwFlags**で、VP\_フラグ\_テレビ\_モード、VP\_フラグ\_テレビ\_標準、および tv コネクタでサポートされている機能を表すその他すべてのフラグを設定します。

-   **Dwmode**を0に設定します。

-   **DwAvailableModes**で、VP\_モード\_WIN\_グラフィックスに設定します。 ハードウェアで VP\_モード\_テレビ\_再生がサポートされている場合は、そのビットも設定します。

-   **DwTVStandard**を VP\_TV\_STANDARD\_WIN\_VGA に設定します。

-   **Dwavailability Ab・ Vstandard**では、テレビコネクタでサポートされているテレビ標準を表すすべてのビットを設定します。

-   \_**dwFlags**で設定されているすべてのフラグについては、\_テレビの\_モードおよび VP\_フラグ\_既に説明されているフラグ\_VIDEOPARAMETERS) に対して、対応するメンバーに値を割り当てます。データ.

例 2: テレビ出力を有効にするには、(ミニポートドライバーではなく) 呼び出し元が次の操作を行う必要があります。

-   **DwFlags**では、\_テレビ\_モードおよび VP\_フラグ\_TV\_STANDARD に\_フラグを設定します。 他のすべてのフラグをクリアします。

-   **Dwmode**を VP\_モードに設定し\_WIN\_GRAPHICS または VP\_モード\_テレビ\_の再生します。 両方のビットを設定しないでください。

-   **DwTvStandard**を目的の標準 (たとえば、VP\_TV\_STANDARD\_NTSC\_M) に設定します。 **DwTvStandard**の他のビットは設定しないでください。

例 3: テレビ出力を無効にするには、(ミニポートドライバーではなく) 呼び出し元が次の操作を行う必要があります。

-   **DwFlags**では、\_テレビ\_モードおよび VP\_フラグ\_TV\_STANDARD に\_フラグを設定します。 他のすべてのフラグをクリアします。

-   **Dwmode**を0に設定します。

-   **DwTvStandard**で、VP\_TV\_STANDARD\_WIN\_VGA に設定します。 **DwTvStandard**の他のすべてのビットをクリアします。

 

 





