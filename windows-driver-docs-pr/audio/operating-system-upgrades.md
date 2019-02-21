---
title: オペレーティング システムのアップグレード
description: オペレーティング システムのアップグレード
ms.assetid: f985967e-e6cf-431a-bb7e-7b6d8486709c
keywords:
- WDK オーディオ アダプターは、オペレーティング システムをアップグレードします。
- アダプターのドライバー WDK オーディオでは、オペレーティング システムをアップグレードします。
- ポート クラス オーディオ アダプター WDK、オペレーティング システムのアップグレード
- WDK オーディオのオーディオ設定の維持
- DLL の WDK オーディオの移行
- 移行の設定の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6867e25d64d7e287d66ee04fffd96bc2474cb3ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537797"
---
# <a name="operating-system-upgrades"></a>オペレーティング システムのアップグレード


## <span id="operating_system_upgrades"></span><span id="OPERATING_SYSTEM_UPGRADES"></span>


オーディオ デバイスのドライバーとレジストリの設定は、オペレーティング システムのアップグレードにわたって頻繁に維持されます。 以下の説明では、これを実現するためのガイドラインを示します。

### <a name="span-idpreservingaudiosettingsspanspan-idpreservingaudiosettingsspanspan-idpreservingaudiosettingsspanpreserving-audio-settings"></a><span id="Preserving_Audio_Settings"></span><span id="preserving_audio_settings"></span><span id="PRESERVING_AUDIO_SETTINGS"></span>オーディオの設定を保持

オーディオ ドライバーでは、デバイスの現在の設定 - 主にボリューム レベルの追跡でき、システム レジストリの設定をミュートすることができます。 通常、ドライバーは、「設定」のサブキーの下 (HKR INF キーワードで表される) システムによって提供されるドライバー キーでこれらの設定を格納します。 ユーザーは、コントロール パネルまたは他のオーディオ アプリケーションを介してこれらの設定を変更、ドライバーは、適切なレジストリ エントリを更新します。 システムが起動するたびに、ドライバーは、レジストリからデバイスの設定を復元します。

Me Windows からアップグレードする場合]、[Windows XP または Windows 2000、98、Windows のインストール プログラムは、これらの設定を保存することができます。

ただし、別に (たとえば、Windows XP を Windows 2000) から、または Windows Me、Windows 98 から NT ベースの 1 つのオペレーティング システムからをアップグレードする際、インストール プログラム、ドライバーの既存のレジストリ設定そのまま残されます。 ユーザーは、作成されたシステムに強制することではなく時間の経過と共に、オペレーティング システムをアップグレードするたびに手動での設定を復元しようとしています。 調整を保持するので、この動作をほとんどもいます。

いくつかの独自ドライバーでは、ただし、無条件たびに上書きこれらのレジストリ設定の既定値でインストールされています。 優れたアプローチは、インストール時に決定するためのドライバーによっては特定のドライバー固有のレジストリ エントリが既に存在するかどうかです。 存在、ドライバーはこれらのエントリを上書きせずに含まれている設定を保存する必要があります。

ドライバーの INF ファイルの追加レジストリ セクション ディレクティブでは、既存のレジストリ エントリを上書きするかどうかを指定します。 詳細については、FLG の説明を参照してください。\_ADDREG\_NOCLOBBER フラグ[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。

### <a name="span-idmigrationdllspanspan-idmigrationdllspanspan-idmigrationdllspanmigration-dll"></a><span id="Migration_DLL"></span><span id="migration_dll"></span><span id="MIGRATION_DLL"></span>DLL の移行

Windows からのアップグレード中に私 98 NT ベース オペレーティング システム (Windows 2000 以降)、Windows のインストール プログラムを処理したデバイス ドライバー/Windows Me にインストール/98 を互換性なしとし、ドライバーとそのレジストリ設定の両方を破棄します。

さらに、Windows 2000 のセットアップ プログラムは、デバイスのインボックス ドライバーのサポートを検出されない場合、プログラムはすぐにドライバー ソフトウェアを提供するユーザーに求めます。 Windows XP 以降では、セットアップ プログラムでインボックスまたは Windows Update サイトでは、適切なドライバーを検索することがない場合、待機、不足しているドライバーのユーザーに通知するために、アップグレードが完了するまでします。

ドライバーは、このようなアップグレード時にそのレジストリ設定の損失を回避することはできません、Microsoft では、移行をユーザーに対して透過的に互換性のあるドライバーを再インストールする DLL の使用を推奨します。 この目的では、Microsoft は、Devupgrd 移行、Windows Driver Kit (WDK) のセットアップのプラグ アンド プレイのサンプルに含まれている DLL を提供します。 このサンプルには、DLL、移行を説明するヘルプ ファイルが含まれています。

移行の DLL は、最初にいる WDM ドライバーでのみ使用する必要があります Windows Me にインストール/98 はも、Windows 2000 または Windows XP で実行可能です。 注こと、移行の DLL からアップグレードできませんドライバー Windows Me 98/Windows Server 2003、Windows Vista では、またはそれ以降。 のみアップグレードできるドライバー Windows から Me 98/Windows XP または Windows 2000 にします。

Windows からのアップグレード中に Me]、[Windows XP または Windows 2000 では、移行の DLL には次の処理します。

-   Me、Windows 内の場所から、デバイス ドライバーの移行情報を読み取る/98 レジストリ。

-   Windows XP または Windows 2000 で、デバイスが正常にインストールすることを確認して、ドライバーの INF ファイルに必要な情報を追加します。

インストールするには、Windows XP または Windows 2000 のセットアップ プログラム、INF ファイルを後で移行については、使用可能 の下の Windows Me/98 は、次に行う必要があります。

-   移行の DLL を INF 指定のバックアップ ディレクトリにコピーし、Me、Windows にそのディレクトリのパス名を追加/98 レジストリ。

-   デバイスを移行できるデバイスを識別する Id レジストリに追加します。

-   INF 指定のバックアップ ディレクトリにドライバー ファイル (.sys および .inf)、デバイスのバックアップ コピーを保存し、それらのディレクトリのパス名をレジストリに追加します。

アップグレードの過程では、Windows XP または Windows 2000 のセットアップ プログラムは、登録したデバイス Id の INF 検索パスにバックアップ ディレクトリ名を追加します。

前述のように、セットアップ プログラムを破棄、ドライバーのレジストリ設定 Windows からのアップグレード中に私 98/Windows XP または Windows 2000 にします。 移行の DLL のヘルプに対して実行されるドライバーの再インストールは、ドライバーのボリューム、ミュート、およびその他の設定が、初期既定値を想定「clean install」です。

Ac97 オーディオ アダプター サンプル Windows Driver Kit (WDK) で Windows からのオーディオ ドライバーの移行は Me INF ファイル (Ac97smpl.inf) の例が含まれています/98 Windows XP または Windows 2000 にします。

 

 




