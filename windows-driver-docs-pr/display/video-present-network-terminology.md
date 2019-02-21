---
title: ビデオの存在するネットワーク用語
description: ビデオの存在するネットワーク用語
ms.assetid: a7a02522-de13-419f-8dc5-065943fd4645
keywords:
- ビデオが存在するネットワーク用語、WDK の表示
- VidPN WDK の表示、用語集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d12c40803419d2f0e39ac3706bb35ecdac9dcf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560046"
---
# <a name="video-present-network-terminology"></a>ビデオの存在するネットワーク用語


VidPN マネージャーでは、ビデオの存在するネットワーク (VidPN) の概念を使用してディスプレイ アダプターに接続されているディスプレイ デバイスのセットを管理します。 詳細については、次を参照してください。[ビデオ存在するネットワークの概要](introduction-to-video-present-networks.md)します。

VidPNs について説明します、アダプター、およびディスプレイ アダプターに接続するデバイスを表示するために使用する主な用語の定義を次に示します。

<span id="display_adapter_s_presentational_subsystem"></span><span id="DISPLAY_ADAPTER_S_PRESENTATIONAL_SUBSYSTEM"></span>**アダプターの表象サブシステムを表示します。**  
スキャンを担当するすべてのハードウェアには、ビデオ メモリとビデオの出力に送ることからコンテンツがレンダリングされます。

<span id="video_present_network"></span><span id="VIDEO_PRESENT_NETWORK"></span>**ビデオの存在するネットワーク**  
このモデルはディスプレイ アダプターに存在するビデオのソースに関連するアダプターのビデオの存在ターゲットし、それらのソースとターゲットを構成する方法を指定します。 ディスプレイ アダプターの表象サブシステムの抽象化することをお勧めします。 VidPN は、以下の構成します。

<span id="video_present_sources"></span><span id="VIDEO_PRESENT_SOURCES"></span>**ビデオの存在するソース**  
独立したビュー (つまり、プライマリ サーフェスのチェーン) ディスプレイ アダプターが同時に提示できます。

<span id="video_present_targets"></span><span id="VIDEO_PRESENT_TARGETS"></span>**ビデオの存在ターゲット**  
独立した物理ビデオ出力、ディスプレイ アダプターでは、それぞれのビューを提供できます。

<span id="topology"></span><span id="TOPOLOGY"></span>**トポロジ**  
コレクション*ビデオの存在するパス*各ビデオの表示パスは存在するビデオ ソースとビデオの存在ターゲット間のアソシエーションです。 ビデオの表示パスでは、特定のソースが特定のターゲットに接続されていることを指定します。 パスには、提示されたコンテンツに適用されるコンテンツの変換も指定します。 ソースをターゲットに接続することを意味ディスプレイ アダプター スキャンの元のプライマリ画面 (チェーン)、ターゲットのビデオ信号形式にスキャンしたコンテンツをエンコードします (たとえば、コントラスト/明るさの向上、コンテンツの変換を適用します。ちらつきのフィルター、色変換) で処理します。

<span id="source_mode_sets"></span><span id="SOURCE_MODE_SETS"></span>**ソース モードの設定**  
各ビデオの存在するソース、VidPN では、VidPN のトポロジで、ソースではサポートされているプライマリ画面形式 (ソース モード) の一覧であるソース モードのセットに関連付けられます。

<span id="target_mode_sets"></span><span id="TARGET_MODE_SETS"></span>**ターゲット モードの設定**  
VidPN 内の各ビデオの存在ターゲットは、VidPN のトポロジ内のターゲットでサポートされているビデオ信号形式 (ターゲット モード) の一覧であるターゲット モードのセットに関連付けられています。

<span id="monitor_source_mode_sets"></span><span id="MONITOR_SOURCE_MODE_SETS"></span>**ソース モード設定を監視します。**  
モニター (またはその他の外部のディスプレイ デバイス) に接続されている VidPN 内の各ターゲットは、接続されているモニターのサポートされているビデオ信号形式の一覧には、モニターのソースのモード セットに関連付けられます。

<span id="active_VidPN"></span><span id="active_vidpn"></span><span id="ACTIVE_VIDPN"></span>**アクティブな VidPN**  
ディスプレイ アダプターで現在設定されている VidPN します。

<span id="pinned_mode"></span><span id="PINNED_MODE"></span>**固定モード**  
特定のビデオの存在するソースまたはターゲットの目的のモードとして指定するモード。 ソース (ターゲット) に固定されているモードとは限りません (ターゲット); のソースで使用されているモード指定した VidPN でソース (ターゲット) のため、目的のモードはではなく (可能性があります [次へ] のアクティブな VidPN として使用する)。 全体にわたって、VidPN に適用される追加の制約を設定モードで使用可能なまま固定モードにする必要があります。 つまり、VidPN への変更は許可されていませんしない限り、変更された VidPN ですべての固定モードは引き続きサポートします。

<span id="functional_VidPN"></span><span id="functional_vidpn"></span><span id="FUNCTIONAL_VIDPN"></span>**機能 VidPN**  
すべての次の条件を満たす VidPN:

-   トポロジでは、少なくとも 1 つのビデオの表示パスがあります。

-   トポロジ内のビデオすべて存在するソースでは、固定モードがあります。

-   トポロジのすべてのビデオの存在ターゲットでは、固定モードがあります。

<span id="modality"></span><span id="MODALITY"></span>**モダリティ**  
モードのコレクションは、すべてのソースとターゲットの VidPN のトポロジで設定します。

<span id="cofunctional_mode_set"></span><span id="COFUNCTIONAL_MODE_SET"></span>**cofunctional モード設定**  
特定のソースまたはターゲット、(たとえば、トポロジ、モードの他のソースとターゲットのピン留め) 制約の使用可能なモードのセットを VidPN の。

<span id="cofunctional_VidPN_modality"></span><span id="cofunctional_vidpn_modality"></span><span id="COFUNCTIONAL_VIDPN_MODALITY"></span>**cofunctional VidPN モダリティ**  
Cofunctional モードのコレクションは、すべてのソースとターゲットの VidPN のトポロジで設定します。

<span id="child_device_of_the_display_adapter"></span><span id="CHILD_DEVICE_OF_THE_DISPLAY_ADAPTER"></span>**ディスプレイ アダプターの子デバイス**  
子として、ディスプレイのミニポート ドライバーを列挙するディスプレイ アダプター上のデバイス。 ディスプレイ アダプターのすべての子デバイスは、オンボード デバイスです。モニターとディスプレイ アダプターに接続するその他のデバイスは、子デバイスは考慮されません。

<span id="external_device"></span><span id="EXTERNAL_DEVICE"></span>**外部のデバイス**  
ディスプレイ アダプターの子デバイスに接続するデバイス。 外部のデバイスでは、ディスプレイ アダプターの子デバイスは考慮されません。

<span id="video_output_device"></span><span id="VIDEO_OUTPUT_DEVICE"></span>**ビデオの出力デバイス**  
外部または組み込みのディスプレイ デバイスにビデオ出力信号を提供するディスプレイ アダプターの子デバイス。

<span id="video_output_codec"></span><span id="VIDEO_OUTPUT_CODEC"></span>**出力ビデオ コーデック**  
ハードウェア エンコーダー/デコーダー ビデオ メモリ内のプライマリ画面から読み取り、1 つ以上のディスプレイ アダプターのビデオ出力にその画面のビデオ信号表現を配置するディスプレイ アダプターでします。

 
<span id="off_screen_memory"></span><span id="OFF_SCREEN_MEMORY"></span>**オフスクリーン メモリ**  
ビデオ メモリの内容はビデオ ディスプレイには表示されません。 オフスクリーン メモリを多数のグラフィックス操作を必要とする複雑なグラフィックス イメージを完全に表示できる表示されるようにする手法のダブル バッファリングに使用できます。 各イメージを表示した後は、アニメーションを実現するために効果的な方法を提供する、同じ方法で別のイメージを構築できます。





