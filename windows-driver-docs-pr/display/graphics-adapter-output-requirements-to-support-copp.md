---
title: COPP をサポートするためのグラフィックス アダプター出力の要件
description: COPP をサポートするためのグラフィックス アダプター出力の要件
ms.assetid: e557487d-dba5-4185-9c35-da3185c291f6
keywords:
- コピー防止 WDK COPP、グラフィック アダプター要件の出力
- ビデオのコピー防止 WDK COPP、グラフィック アダプター要件の出力
- COPP WDK DirectX va なので、グラフィック アダプター要件の出力
- ビデオの WDK COPP 保護されているグラフィック アダプター要件の出力
- グラフィック アダプター要件 WDK COPP の出力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b440160a9fa2af80796c0b0db8b777b3db862ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374608"
---
# <a name="graphics-adapter-output-requirements-to-support-copp"></a>COPP をサポートするためのグラフィックス アダプター出力の要件


## <span id="ddk_display_adapter_output_requirements_to_support_copp_gg"></span><span id="DDK_DISPLAY_ADAPTER_OUTPUT_REQUIREMENTS_TO_SUPPORT_COPP_GG"></span>


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

COPP をサポートするには、グラフィックス アダプターの物理出力コネクタは、次のタスクを実行する必要があります。

<span id="Protect_key_information"></span><span id="protect_key_information"></span><span id="PROTECT_KEY_INFORMATION"></span>重要な情報を保護します。  
認定済みの出力には、認定をもって出力に発行された重要な情報を保護する必要があります。

<span id="Restrict_unauthorized_components_from_accessing_secure_content"></span><span id="restrict_unauthorized_components_from_accessing_secure_content"></span><span id="RESTRICT_UNAUTHORIZED_COMPONENTS_FROM_ACCESSING_SECURE_CONTENT"></span>セキュリティで保護されたコンテンツへのアクセスを承認されていないコンポーネントを制限します。  
認定済みの出力では、COPP セキュリティで保護されたチャネルを介して送信されたコンテンツへのアクセスを承認されていないソフトウェアやハードウェア コンポーネントを防ぐ必要があります。 認定済みの出力には、COPP セキュリティで保護されたチャネル経由で受信したデータを操作する COPP コマンドのみを許可する必要があります。

<span id="Switch_to_a_failure_mode_if_the_output_fails"></span><span id="switch_to_a_failure_mode_if_the_output_fails"></span><span id="SWITCH_TO_A_FAILURE_MODE_IF_THE_OUTPUT_FAILS"></span>出力に失敗した場合、障害モードに切り替える  
認定済みの出力は、構成時に指定した構成プロファイルを適用不要になったことができます、出力は受信したコンテンツを復号化を停止し、アプリケーションにステータス メッセージを送信する必要があります。 ステータス メッセージは、出力では構成されているを実行できる不要になったことを示す必要があります。

 

 





