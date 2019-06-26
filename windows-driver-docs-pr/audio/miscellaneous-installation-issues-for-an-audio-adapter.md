---
title: オーディオ アダプターためのインストールに関するその他の問題
description: オーディオ アダプターためのインストールに関するその他の問題
ms.assetid: fcfa9c41-7fad-4b22-9054-a1debb972580
keywords:
- オーディオ アダプター、WDK をインストールします。
- アダプターのドライバー WDK オーディオをインストールします。
- ポート クラス オーディオ アダプター、WDK をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 484c26d67c15a042090d999423c15adc8f4e3f2c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355347"
---
# <a name="miscellaneous-installation-issues-for-an-audio-adapter"></a>オーディオ アダプターためのインストールに関するその他の問題


## <span id="miscellaneous_installation_issues_for_an_audio_adapter"></span><span id="MISCELLANEOUS_INSTALLATION_ISSUES_FOR_AN_AUDIO_ADAPTER"></span>


オーディオのアダプターのインストールの最も一般的な問題には表示されています。

-   オーディオ デバイスまたは既存のオーディオ設定を破壊するオペレーティング システムのアップグレードの実行時の初期インストール中に、ドライバーは、設定が適切な既定値に初期化される確認してください。 詳細については、次を参照してください。[オーディオの音量設定の既定の](default-audio-volume-settings.md)します。

-   インストールの実行中に、OEM は既定のオーディオ音量レベル、またはハードコーディング オーディオ クラス ドライバーによっては、マイク ブーストの既定のレベルをオーバーライドする思います。 これは Windows 7 までの Windows の以前のバージョンでは不可能でした。 Windows 8 以降では、これらの設定の既定値をカスタマイズできます。 これを行う方法の詳細については、次を参照してください。[既定のオーディオのボリューム設定のカスタマイズ](customizing-default-audio-volume-settings.md)します。

-   Windows Vista およびそれ以降のオペレーティング システムでは、オーディオ デバイスのマスター ボリューム レベルの既定の設定は、の減衰の 6 つデシベル単位と、インストール時に設定されます。 この既定マスター ボリューム レベルの設定、またはインストール後に、選択したその他の任意のレベルは、コンピューターを再起動するどのくらいの頻度に関係なく維持されます。 ボリューム レベルの持続性をオプトアウトすることができますディレクティブを使用する、AddProperty レジストリ、INF ファイルを使用して、鍵の値を設定する\_AudioDevice\_DontPersistControls レジストリ キー。 これを行う方法の詳細については、次を参照してください。[ボリューム レベル永続化のオプトイン](opting-out-of-volume-level-persistence.md)します。

-   オペレーティング システムのアップグレード中にオーディオ デバイスのインストールされているドライバとレジストリ設定を頻繁に保持されます。 このプロセスをユーザーが透明にする方法のガイドラインについては、次を参照してください。[オペレーティング システムのアップグレード](operating-system-upgrades.md)します。

-   オーディオ ドライバーはオーディオ アダプター カードを同じシステムに接続の複数の同じインスタンスに簡単に設計されています。 詳細については、次を参照してください。[システム全体の一意のデバイス Id](system-wide-unique-device-ids.md)します。

-   すべてのデバイス クラスに共通する INF ファイルのキーワードの一覧は、次を参照してください。 [INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)します。 ただし、この一覧は、メディアに固有のいくつかのキーワードは含まれません。 詳細については、次を参照してください。 [INF ファイルのメディアに固有のキーワード](media-specific-inf-file-keywords.md)します。

-   方法、アダプタのドライバまたはミニポート ドライバーできますセットアップ情報をレジストリから取得方法の詳細については、次を参照してください。[デバイスのセットアップ情報を取得する](retrieving-device-setup-information.md)します。

-   物理ボリューム コントロール ノブがないオーディオのアダプター用の Windows Vista のサポートについては、次を参照してください。、 [Windows Vista ソフトウェア ボリューム コントロール サポート](https://docs.microsoft.com/windows-hardware/drivers/audio/software-volume-control-support)トピック。

 

 




