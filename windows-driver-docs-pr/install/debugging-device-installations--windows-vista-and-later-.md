---
title: デバイスのインストールのデバッグ
description: デバイスのインストールのデバッグ
ms.assetid: bc7105f6-8ba7-49da-8c02-ceda69066daa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 087ddb8305f6c2592ea086d5fda3c32040b07338
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577810"
---
# <a name="debugging-device-installations"></a>デバイスのインストールのデバッグ


デバイスのインストールの主要な段階を常と呼ばれる非対話型のコンテキストで実行では、Windows Vista および Windows の以降のバージョンでは、*サーバー側インストール*します。 デバイスのインストールのホスト プロセス (*DrvInst.exe*) は、LocalSystem アカウントのセキュリティ コンテキストで実行されます。

サーバー側のインストールでは、非対話的に実行し、すべてのユーザー入力なしで完了する必要があります、ためのアクションをデバッグするドライバー パッケージの開発者にいくつかの課題を提供、[ドライバー パッケージの](driver-packages.md)クラスのインストーラーと共同インストーラー Dll。 ドライバー パッケージの開発者は、通常はデバイスのインストール中に共同インストーラー DLL のアクションをデバッグする最も望ましくなります。

ここでは、次のトピックは、デバイスのインストールの主要な段階で co-installer をデバッグするために使用する方法について説明します。

[デバイスのインストールのデバッグのサポートを有効にします。](enabling-support-for-debugging-device-installations.md)

[ユーザー モード デバッガーによるデバッグ デバイスのインストール](debugging-device-installations-with-a-user-mode-debugger.md)

[カーネル デバッガー (KD) を使用したデバイスのインストールのデバッグ](debugging-device-installations-with-the-kernel-debugger--kd-.md)

共同インストーラーの詳細については、次を参照してください。[共同インストーラーの作成](writing-a-co-installer.md)です。

 

 





