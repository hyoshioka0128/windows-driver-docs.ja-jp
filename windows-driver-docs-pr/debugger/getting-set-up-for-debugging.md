---
title: デバッグの設定 (カーネルモードとユーザーモード)
description: Windows デバッガーを使用してデバッグを設定するには、2つの方法があります。
ms.assetid: 3575B850-A0F9-4AAE-9432-E970D40069D2
keywords:
- デバッグのセットアップ
- デバッグの構成
- デバッガーの構成
- WinDbg
- Visual Studio のデバッグ
- カーネルモードのデバッグ
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2b458ffbd5dba5c45dfa61acd396b836fc555b42
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528962"
---
# <a name="setting-up-debugging-kernel-mode-and-user-mode"></a>デバッグの設定 (カーネルモードとユーザーモード)

カーネルモードのデバッグを設定した後、WinDbg または KD を使用してデバッグセッションを確立できます。 ユーザーモードのデバッグを設定した後、WinDbg、CDB、または NTSD を使用してデバッグセッションを確立できます。

Windows デバッガーは、Windows 用デバッグツールに含まれ**て  ます**。 これらのデバッガーは、visual studio に含まれている Visual Studio デバッガーとは異なります。 詳細については、「 [Windows デバッグ](index.md)」を参照してください。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容

### <a name="configuring-transports"></a>トランスポートの構成

- [カーネルモードデバッグの設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

### <a name="supported-target-pc-nics"></a>サポートされているターゲット PC Nic

- [Windows 10 でのネットワークカーネルデバッグ用にサポートされているイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)
- [Windows 8.1 でのネットワークカーネルデバッグ用にサポートされるイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)
- [Windows 8 でのネットワークカーネルデバッグ用にサポートされているイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

### <a name="additional-configuration-tools"></a>その他の構成ツール

- [ツール .ini を構成しています](configuring-tools-ini.md)
- [KDbgCtrl の使用](using-kdbgctrl.md)
