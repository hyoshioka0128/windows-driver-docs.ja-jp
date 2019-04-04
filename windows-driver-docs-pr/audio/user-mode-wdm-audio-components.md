---
title: ユーザー モード WDM オーディオ コンポーネント
description: ユーザー モード WDM オーディオ コンポーネント
ms.assetid: 067944fb-6854-4ae8-81ca-9b8f2eed939e
keywords:
- ユーザー モード コンポーネント WDK オーディオ
- WinMM システム コンポーネントの WDK オーディオ
- WDMAud システム ドライバー WDK オーディオ
- DirectSound システム コンポーネントの WDK オーディオ
- DirectMusic システム コンポーネントの WDK オーディオ
- Windows オーディオ Services WDK オーディオ
- waveOut API WDK オーディオ
- WDK の音声サービス
- WDMAud システム ドライバー
- WDMAud システム ドライバー、ユーザー モード (wdmaud.drv)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21bdb025f98a292fc81252fb4051d0bbb4492113
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537799"
---
# <a name="user-mode-wdm-audio-components"></a>ユーザー モード WDM オーディオ コンポーネント


## <span id="user_mode_wdm_audio_components"></span><span id="USER_MODE_WDM_AUDIO_COMPONENTS"></span>


ユーザー モードの Microsoft Windows Driver Model (WDM) オーディオ コンポーネントは次のとおりです。

-   WinMM システム コンポーネント

-   WDMAud システム ドライバー

-   DirectSound システム コンポーネント

-   DirectMusic システム コンポーネント

-   Windows の音声サービス

### <a name="span-idwinmmsystemcomponentspanspan-idwinmmsystemcomponentspanwinmm-system-component"></a><span id="winmm_system_component"></span><span id="WINMM_SYSTEM_COMPONENT"></span>WinMM システム コンポーネント

WinMM システム コンポーネント (Winmm.dll と 16 ビットの対応する、Mmsystem.dll) 実装の Microsoft Windows のマルチ メディア Api wave*Xxx*、midi*Xxx*、ミキサー*Xxx*、aux*Xxx* (Microsoft Windows SDK のドキュメントを参照してください)。 WinMM コンポーネントでは、WDMAud システム ドライバーを使用して、I/O 要求のカーネル ストリーミングに WinMM API 呼び出しを変換します。

### <a name="span-idwdmaudsystemdriverspanspan-idwdmaudsystemdriverspanwdmaud-system-driver"></a><span id="wdmaud_system_driver"></span><span id="WDMAUD_SYSTEM_DRIVER"></span>WDMAud システム ドライバー

ユーザー モード WDMAud システム ドライバー (Wdmaud.drv) は、カーネル モード WDMAud システム ドライバー (Wdmaud.sys) と組み合わせて使用します。 同時に、WDMAud システム ドライバーは WinMM API 呼び出しとカーネル ストリーミング I/O 要求間で変換します。 詳細については、カーネル モードの WDMAud ドライバーのモードは、SysAudio システム ドライバーのクライアントです。

### <a name="span-iddirectsoundsystemcomponentspanspan-iddirectsoundsystemcomponentspandirectsound-system-component"></a><span id="directsound_system_component"></span><span id="DIRECTSOUND_SYSTEM_COMPONENT"></span>DirectSound システム コンポーネント

DirectSound システム コンポーネント (Dsound.dll) サポート、DirectSound API (Microsoft Windows SDK のドキュメントを参照してください)。 DirectSound コンポーネントは、SysAudio ドライバーのクライアントです。 ハードウェアの混在が使用可能な場合は、SysAudio ドライバーは、レンダリング デバイスに直接 DirectSound ハードウェア バッファーを接続します。 それ以外の場合、SysAudio ドライバーは DirectSound ソフトウェア バッファーを KMixer システムのドライバーに接続します。 詳細については、[レンダリング Wave コンテンツを使用して DirectSound ソフトウェアおよびハードウェア バッファー](rendering-wave-content-using-directsound-software-and-hardware-buffers.md)を参照してください。

### <a name="span-iddirectmusicsystemcomponentspanspan-iddirectmusicsystemcomponentspandirectmusic-system-component"></a><span id="directmusic_system_component"></span><span id="DIRECTMUSIC_SYSTEM_COMPONENT"></span>DirectMusic システム コンポーネント

DirectMusic システム コンポーネント (DMusic.dll) サポート、DirectMusic API (Microsoft Windows SDK のドキュメントを参照してください)。 このコンポーネントには、WDM オーディオ デバイスへの I/O 要求に DirectMusic API への呼び出しに変換します。 DirectMusic コンポーネントは、SysAudio システム ドライバーのクライアントです。

### <a name="span-idwindowsaudioservicesspanspan-idwindowsaudioservicesspanwindows-audio-services"></a><span id="windows_audio_services"></span><span id="WINDOWS_AUDIO_SERVICES"></span>Windows の音声サービス

Windows XP 以降では、Windows オーディオ サービス コンポーネント (Audiosrv.dll) は、Windows ベースのプログラムのオーディオ デバイスを管理します。 Windows オーディオ サービスを停止できないようにオーディオ デバイスと効果が適切に機能します。 オーディオのサービスが無効な場合を開始に明示的に依存している他のサービスの (WDM オーディオ ドライバーを含む) は失敗します。 Home Edition、Professional、およびサーバー バージョンの Windows XP 以降、オーディオのサービスが既定では自動的に開始するように構成されます。 ただし、Advanced Server、データ センター、および Web サーバーのバージョンの Windows Server 2003 以降では、オーディオのサービスは既定で無効にします。 オーディオのサービスを無効にすると、オーディオ デバイスのインストールも、そのできません--にこれを行うには、管理者が明示的に設定する場合にのみ、自動的に実行するオーディオ サービスが有効になっています。 開始して、Windows サービスの停止については、のヘルプ ファイルを参照してください、**サービス**] ダイアログ ボックス (Windows コントロール パネルの [検索対象**管理ツール**)。

 

 




