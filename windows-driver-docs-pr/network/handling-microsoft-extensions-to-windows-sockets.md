---
title: Windows ソケットに対する Microsoft 拡張機能の処理
description: Windows ソケットに対する Microsoft 拡張機能の処理
ms.assetid: e5209a63-519b-42bd-882b-a1c3d2074deb
keywords:
- WDK Windows Sockets の拡張機能
- Windows ソケットは、WDK、拡張機能を直接します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0e743ba1a6d6fbae705b5783e491f89a007f6a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379822"
---
# <a name="handling-microsoft-extensions-to-windows-sockets"></a>Windows ソケットに対する Microsoft 拡張機能の処理





Windows Sockets スイッチは、すべての Microsoft 固有の Windows Sockets 拡張関数を内部的に処理します。 Microsoft Windows SDK のドキュメントを公開するメカニズムが高度な拡張機能を定義する Windows Sockets では、アプリケーションのプログラム 機能を転送します。 これらの拡張機能は次のとおりです。**TransmitFile**、 **AcceptEx**、および**GetAcceptExSockAddrs**します。 スイッチは、必要に応じて、これらの呼び出しに変換し、適切な SAN サービス プロバイダー関数に転送します。[**WSPSend**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566316(v=vs.85))、 [ **WSPAccept**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566266(v=vs.85))、 [ **WSPRdmaWrite**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566306(v=vs.85))、または[ **WSPRdmaRead**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566304(v=vs.85))します。

 

 





