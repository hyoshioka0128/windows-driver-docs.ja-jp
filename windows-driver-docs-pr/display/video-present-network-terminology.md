---
title: ビデオ表現ネットワークの用語
description: ビデオ表現ネットワークの用語
ms.assetid: a7a02522-de13-419f-8dc5-065943fd4645
keywords:
- ビデオの現在のネットワーク WDK 表示、用語
- VidPN WDK の表示、用語
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d12c40803419d2f0e39ac3706bb35ecdac9dcf
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242893"
---
# <a name="video-present-network-terminology"></a>ビデオ表現ネットワークの用語


VidPN マネージャーは、ビデオの現在のネットワーク (VidPN) の概念を使用して、ディスプレイアダプターに接続されているディスプレイデバイスのセットを管理します。 詳細については、「[ビデオの現在のネットワークの概要](introduction-to-video-present-networks.md)」を参照してください。

次の一覧に、VidPNs、ディスプレイアダプター、およびディスプレイアダプターに接続するデバイスの説明に使用される主な用語の定義を示します。

<span id="display_adapter_s_presentational_subsystem"></span><span id="DISPLAY_ADAPTER_S_PRESENTATIONAL_SUBSYSTEM"></span>**ディスプレイアダプターの主要サブシステム**  
ビデオメモリからレンダリングされたコンテンツをスキャンし、ビデオ出力に表示するすべてのハードウェア。

<span id="video_present_network"></span><span id="VIDEO_PRESENT_NETWORK"></span>**ビデオの現在のネットワーク**  
ディスプレイアダプターに存在するビデオソースを、アダプター上のビデオに存在するビデオに関連付けて、それらのソースとターゲットをどのように構成するかを指定するモデル。 これは、ディスプレイアダプターの主要サブシステムを抽象化したものです。 VidPN は、次の要素で構成されます。

<span id="video_present_sources"></span><span id="VIDEO_PRESENT_SOURCES"></span>**ビデオの現在のソース**  
ディスプレイアダプターが同時に提示できる独立したビュー (主サーフェスチェーン)。

<span id="video_present_targets"></span><span id="VIDEO_PRESENT_TARGETS"></span>**ビデオの現在のターゲット**  
ディスプレイアダプターがビューを表示できる独立した物理ビデオ出力。

<span id="topology"></span><span id="TOPOLOGY"></span>**モジュール**  
ビデオの存在するパスのコレクション。各ビデオ*は、ビデオ*の現在のソースとビデオの現在のターゲットの間の関連付けです。 ビデオの存在パスは、特定のソースが特定のターゲットに接続されていることを指定します。 パスでは、表示されるコンテンツに適用されるコンテンツ変換も指定します。 ソースをターゲットに接続すると、表示アダプターはソースのプライマリサーフェイス (チェーン) からスキャンし、スキャンされたコンテンツをターゲットのビデオシグナル形式にエンコードし、コンテンツ変換 (コントラスト、明るさの向上、ちらつきのフィルター、色の変換など) をプロセスで適用します。

<span id="source_mode_sets"></span><span id="SOURCE_MODE_SETS"></span>**ソースモードセット**  
VidPN に表示される各ビデオは、ソースモードセットに関連付けられています。これは、VidPN のトポロジでソースでサポートされている主な表面形式 (ソースモード) のリストです。

<span id="target_mode_sets"></span><span id="TARGET_MODE_SETS"></span>**ターゲットモードセット**  
VidPN 内の各ビデオは、ターゲットモードセットに関連付けられています。これは、VidPN のトポロジのターゲットでサポートされているビデオ信号形式 (ターゲットモード) の一覧です。

<span id="monitor_source_mode_sets"></span><span id="MONITOR_SOURCE_MODE_SETS"></span>**ソースモードセットの監視**  
モニター (または他の外部ディスプレイデバイス) に接続されている、VidPN 内の各ターゲットは、接続されたモニターでサポートされているビデオ信号形式の一覧であるモニターソースモードセットに関連付けられています。

<span id="active_VidPN"></span><span id="active_vidpn"></span><span id="ACTIVE_VIDPN"></span>**アクティブな VidPN**  
ディスプレイアダプターに現在設定されている VidPN。

<span id="pinned_mode"></span><span id="PINNED_MODE"></span>**固定モード**  
特定のビデオのソースまたはターゲットとして必要なモードとして指定されたモード。 ソース (ターゲット) に固定されているモードは、必ずしもソース (ターゲット) によって現在使用されているモードではありません。代わりに、特定の VidPN 内のそのソース (ターゲット) に適したモードです (おそらく、次のアクティブな VidPN として使用される可能性があります)。 ピン留めされたモードは、そのモードで、VidPN に適用される追加の制約を通じて、引き続き使用できる必要があります。 つまり、変更された VidPN ですべてのピン留めモードがサポートされている場合を除き、VidPN に変更を行うことはできません。

<span id="functional_VidPN"></span><span id="functional_vidpn"></span><span id="FUNCTIONAL_VIDPN"></span>**機能的な VidPN**  
次のすべての条件を満たす VidPN。

-   このトポロジには、少なくとも1つのビデオの存在するパスが含まれています。

-   トポロジ内のすべてのビデオは、ピン留めモードで表示されます。

-   トポロジ内のすべてのビデオが存在する場合は、ピン留めされたモードになります。

<span id="modality"></span><span id="MODALITY"></span>**モダリティ**  
VidPN のトポロジにおけるすべてのソースとターゲットのモードセットのコレクション。

<span id="cofunctional_mode_set"></span><span id="COFUNCTIONAL_MODE_SET"></span>**cofunctional モードセット**  
特定のソースまたはターゲットに対して使用できるモードのセット。たとえば、VidPN の制約 (トポロジ、他のソースとターゲットにピン留めされたモードなど) を指定します。

<span id="cofunctional_VidPN_modality"></span><span id="cofunctional_vidpn_modality"></span><span id="COFUNCTIONAL_VIDPN_MODALITY"></span>**cofunctional な VidPN モダリティ**  
VidPN のトポロジ内のすべてのソースとターゲットに対する cofunctional モードセットのコレクション。

<span id="child_device_of_the_display_adapter"></span><span id="CHILD_DEVICE_OF_THE_DISPLAY_ADAPTER"></span>**ディスプレイアダプターの子デバイス**  
ディスプレイミニポートドライバーが子として列挙するディスプレイアダプター上のデバイス。 ディスプレイアダプターのすべての子デバイスは、ボードデバイスです。ディスプレイアダプターに接続するモニターとその他のデバイスは、子デバイスとは見なされません。

<span id="external_device"></span><span id="EXTERNAL_DEVICE"></span>**外部デバイス**  
ディスプレイアダプターの子デバイスに接続するデバイス。 外部デバイスは、ディスプレイアダプターの子デバイスとは見なされません。

<span id="video_output_device"></span><span id="VIDEO_OUTPUT_DEVICE"></span>**ビデオ出力デバイス**  
外部または組み込みのディスプレイデバイスにビデオ出力信号を提供するディスプレイアダプターの子デバイス。

<span id="video_output_codec"></span><span id="VIDEO_OUTPUT_CODEC"></span>**ビデオ出力コーデック**  
ディスプレイアダプターのハードウェアエンコーダー/デコーダー。ビデオメモリ内のプライマリサーフェイスから読み取り、その表面のビデオ信号表現を1つ以上のディスプレイアダプターのビデオ出力に配置します。

 
<span id="off_screen_memory"></span><span id="OFF_SCREEN_MEMORY"></span>**画面外のメモリ**  
ビデオディスプレイにコンテンツが表示されないビデオメモリ。 画面に表示されないメモリは、大量のグラフィックス操作を必要とする複雑なグラフィックスイメージを表示する前に完全にレンダリングできるようにするための、ダブルバッファリングに使用できます。 各イメージが表示された後、同じ方法で別のイメージを作成し、効果的な方法でアニメーションを実現できます。





