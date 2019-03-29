---
title: シェル コマンドの使用
description: シェル コマンドの使用
ms.assetid: 16df2592-0e7d-4cd3-bc35-5323578cf555
keywords:
- シェル コマンド
- シェル コマンド, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 021c12590d078be1cf898afa1b62e475ecf7960d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581184"
---
# <a name="using-shell-commands"></a>シェル コマンドの使用


## <span id="ddk_using_shell_commands_dbg"></span><span id="DDK_USING_SHELL_COMMANDS_DBG"></span>


デバッガーでは、デバッガーが実行されている Microsoft Windows 環境に特定のコマンドを送信できます。

使用することができます、 [ **.shell (コマンド シェル)** ](-shell--command-shell-.md)任意の Windows のデバッガー コマンド。 次のコマンドでは、デバッガーから直接アプリケーションまたは Microsoft MS-DOS のコマンドを実行できます。 実行している場合[リモート デバッグ](remote-debugging.md)サーバーのシェル コマンドを実行します。

[ **.Noshell (シェルのコマンドを禁止)** ](-noshell--prohibit-shell-commands-.md)コマンドまたは **- noshell** [コマンド ライン オプション](command-line-options.md)シェル コマンドをすべて無効にします。 コマンドを無効に、デバッガーが実行されている場合でも、新しいデバッグ セッションを開始します。 コマンドを発行する場合でも無効のまま、 [ **.restart (再起動カーネル接続)** ](-restart--restart-kernel-connection-.md) KD コマンド。

デバッグ サーバーを実行している場合は、シェル コマンドを無効にすることがあります。 リモート接続で使用できる、シェルを使用できる場合、 **.shell**コンピューターを変更するコマンド。

### <a name="span-idnetworkdrivecontrolspanspan-idnetworkdrivecontrolspannetwork-drive-control"></a><span id="network_drive_control"></span><span id="NETWORK_DRIVE_CONTROL"></span>ネットワーク ドライブの制御

使用することができます、WinDbg で、[ファイル |ネットワーク ドライブのマップ](file---map-network-drive.md)と[ファイル |ネットワーク ドライブの切断](file---disconnect-network-drive.md)ドライブ マッピングのコマンドは、ネットワークを管理します。 これらの変更は、常に、WinDbg は WinDbg にリモートで接続されている任意のコンピューターではなくで実行されているコンピューターで発生します。

 

 





