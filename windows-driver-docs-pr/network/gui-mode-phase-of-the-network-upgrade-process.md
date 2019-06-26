---
title: ネットワーク アップグレード プロセスの GUI モード フェーズ
description: ネットワーク アップグレード プロセスの GUI モード フェーズ
ms.assetid: 35c382aa-5905-4a22-b9fa-b876d1373b94
keywords:
- ネットワーク コンポーネントをアップグレード WDK、フェーズ
- WDK のネットワーク コンポーネントのアップグレード フェーズします。
- GUI モード フェーズ WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1f6d62756c2b5d4f2a302684d2cfbcd387b5355
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382749"
---
# <a name="gui-mode-phase-of-the-network-upgrade-process"></a>ネットワーク アップグレード プロセスの GUI モード フェーズ





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

Windows 2000 またはそれ以降のオペレーティング システムは、システムにインストールする前に、NetSetup は Winnt32 フェーズ中に、応答ファイルに書き込まれたネットワークに固有の情報を読み取ります。

ネットワーク移行 DLL を作成した場合、 [ **InfToRunBeforeInstall** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559059(v=vs.85))キー コンポーネントを*OEM セクション*NetSetup、応答ファイルでは、INF ファイルおよび指定したセクションの操作を検索しますキーとプロセスのこのセクションでは、INF ディレクティブ。 このセクションでには、通常が含まれています、 **AddReg**、**して**、 **AddService**、または**DelService**ディレクティブ。

Windows 2000 またはそれ以降のオペレーティング システムをインストールした後 NetSetup はコンポーネントをコンポーネントの Windows 2000 またはそれ以降の INF ファイルに指定された既定のパラメーター値を使用して、システムで検出された各ネットワーク コンポーネントをインストールします。 NetSetup は、応答ファイルに表示されているネットワーク コンポーネントをインストールします。

ネットワーク コンポーネントの*OEM セクション*、応答ファイルが含まれています、 [OemDllToLoad](examining-the-answerfile.md)キー、NetSetup 読み込みますネットワーク移行 DLL、DLL が既に読み込まれていないと、呼び出して、DLL の場合[**PostUpgradeInitialize** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff562410(v=vs.85))関数。 **PostUpgradeInitialize**関数は、DLL 自体を初期化するために、DLL を使用する情報を提供します。 NetSetup を呼び出して、DLL の[**発生**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545629(v=vs.85)) DLL によってアップグレードするには、各ネットワーク コンポーネントに対して 1 回の関数。 **発生**ユーザーがコンポーネントのパラメーター値を指定できるユーザー インターフェイスを表示できます。 **発生**ユーザーが指定したパラメーターの値をレジストリに書き込みます。

ネットワーク アダプターのミニポート ドライバーにアップグレードする前に、アダプターのインスタンス ID が必要な場合、アップグレード後に、アダプターのインスタンス ID が必要ことがあります。 DLL を呼び出すことができますのネットワーク移行[ **HrGetInstanceGuidOfPreNT5NetCardInstance** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546613(v=vs.85))からその**発生**Windows 2000 以降を取得する関数ネットワーク アダプターのインスタンス GUID。

NetSetup では、インストールされているネットワーク プロトコル、クライアント、およびサービスを開始します。

NetSetup 内のエントリの処理、**識別**セクションの応答ファイルと、システムには、ワークグループまたはドメインのセクションで指定された接続を試みます。

システムのアップグレード中に、非同期のアダプターが含まれている場合、セットアップは、次のように各非同期アダプターをアップグレードする非同期のクラス インストーラーを呼び出します。

-   非同期クラスのインストーラーは、応答ファイル内の非同期アダプターは、OEM のセクションを検索します。

-   非同期アダプターの OEM セクションでは、非同期クラスのインストーラーは、アダプターのアップグレード前のパラメーター値を読み取ります。 これらのパラメーター値は、アップグレードの Winnt32 フェーズ中に、アダプターのネットワーク移行 DLL によって書き込まれました。

-   非同期クラスのインストーラーは、アダプターのアップグレード前のパラメーターの値を Windows 2000 またはそれ以降のレジストリに書き込みます。

 

 





