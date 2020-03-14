---
title: ユーザー モード WDM オーディオ コンポーネント
description: ユーザー モード WDM オーディオ コンポーネント
ms.assetid: 067944fb-6854-4ae8-81ca-9b8f2eed939e
keywords:
- ユーザーモードコンポーネント WDK オーディオ
- Winmm.dll システムコンポーネントの WDK オーディオ
- WDMAud システムドライバー WDK オーディオ
- DirectSound システムコンポーネント WDK オーディオ
- DirectMusic システムコンポーネント WDK オーディオ
- Windows Audio Services WDK オーディオ
- waveOut API WDK オーディオ
- オーディオサービス WDK
- WDMAud システムドライバー
- WDMAud システムドライバー、ユーザーモード (WDMAud)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21bdb025f98a292fc81252fb4051d0bbb4492113
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242853"
---
# <a name="user-mode-wdm-audio-components"></a>ユーザー モード WDM オーディオ コンポーネント


## <span id="user_mode_wdm_audio_components"></span><span id="USER_MODE_WDM_AUDIO_COMPONENTS"></span>


ユーザーモードの Microsoft Windows Driver Model (WDM) オーディオコンポーネントは次のとおりです。

-   Winmm.dll システムコンポーネント

-   WDMAud システムドライバー

-   DirectSound システムコンポーネント

-   DirectMusic システムコンポーネント

-   Windows オーディオサービス

### <a name="span-idwinmm_system_componentspanspan-idwinmm_system_componentspanwinmm-system-component"></a><span id="winmm_system_component"></span><span id="WINMM_SYSTEM_COMPONENT"></span>Winmm.dll システムコンポーネント

Winmm.dll システムコンポーネント (Winmm.dll とその16ビット対応の Mmsystem .dll) には、Microsoft Windows マルチメディア Api wave*xxx*、midi*Xxx*、ミキサー*xxx*、および aux*xxx*が実装されています (Microsoft Windows SDK のドキュメントを参照してください)。 Winmm.dll コンポーネントは、WDMAud システムドライバーを使用して、Winmm.dll API 呼び出しをカーネルストリーミング i/o 要求に変換します。

### <a name="span-idwdmaud_system_driverspanspan-idwdmaud_system_driverspanwdmaud-system-driver"></a><span id="wdmaud_system_driver"></span><span id="WDMAUD_SYSTEM_DRIVER"></span>WDMAud システムドライバー

ユーザーモードの WDMAud システムドライバー (Wdmaud) は、カーネルモードの WDMAud システムドライバー (Wdmaud) とペアになっています。 WDMAud システムドライバーは、Winmm.dll API 呼び出しとカーネルストリーミング i/o 要求の間で相互に変換されます。 カーネルモードモードの WDMAud ドライバーは、SysAudio システムドライバーのクライアントです。

### <a name="span-iddirectsound_system_componentspanspan-iddirectsound_system_componentspandirectsound-system-component"></a><span id="directsound_system_component"></span><span id="DIRECTSOUND_SYSTEM_COMPONENT"></span>DirectSound システムコンポーネント

DirectSound システムコンポーネント (Dsound) は DirectSound API をサポートしています (Microsoft Windows SDK のドキュメントを参照してください)。 DirectSound コンポーネントは、SysAudio ドライバーのクライアントです。 ハードウェアミックスが使用可能な場合、SysAudio ドライバーは DirectSound ハードウェアバッファーをレンダリングデバイスに直接接続します。 それ以外の場合、SysAudio ドライバーは DirectSound ソフトウェアバッファーを KMixer システムドライバーに接続します。 詳細については、「 [DirectSound ソフトウェアとハードウェアバッファーを使用した Wave コンテンツのレンダリング](rendering-wave-content-using-directsound-software-and-hardware-buffers.md)」を参照してください。

### <a name="span-iddirectmusic_system_componentspanspan-iddirectmusic_system_componentspandirectmusic-system-component"></a><span id="directmusic_system_component"></span><span id="DIRECTMUSIC_SYSTEM_COMPONENT"></span>DirectMusic システムコンポーネント

DirectMusic システムコンポーネント (DMusic .dll) は、DirectMusic API をサポートしています (Microsoft Windows SDK のドキュメントを参照してください)。 このコンポーネントは、DirectMusic API に対する呼び出しを、WDM オーディオデバイスへの i/o 要求に変換します。 DirectMusic コンポーネントは、SysAudio システムドライバーのクライアントです。

### <a name="span-idwindows_audio_servicesspanspan-idwindows_audio_servicesspanwindows-audio-services"></a><span id="windows_audio_services"></span><span id="WINDOWS_AUDIO_SERVICES"></span>Windows オーディオサービス

Windows XP 以降では、windows オーディオサービスコンポーネント (Audiosrv .dll) が Windows ベースのプログラムのオーディオデバイスを管理します。 Windows オーディオサービスを停止すると、オーディオデバイスと特殊効果が正しく機能しなくなります。 オーディオサービスが無効になっている場合、それらに明示的に依存している他のサービス (WDM オーディオドライバーを含む) は起動に失敗します。 Windows XP 以降の Home Edition、Professional、および Server バージョンでは、オーディオサービスが既定で自動的に開始するように構成されています。 ただし、Advanced Server、Data Center、および Web Server バージョンの Windows Server 2003 以降では、オーディオサービスが既定で無効になっています。 オーディオサービスが無効になっている場合、オーディオデバイスをインストールしても有効になりません。オーディオサービスは、管理者が明示的に構成した場合にのみ自動的に実行されます。 Windows サービスの開始と停止の詳細については、 **[サービス]** ダイアログボックスのヘルプファイルを参照してください ( **[管理ツール]** の下にある windows のコントロールパネルを参照してください)。

 

 




