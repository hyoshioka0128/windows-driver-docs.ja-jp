---
title: Windows ソケットに対する Microsoft 拡張機能の処理
description: Windows ソケットに対する Microsoft 拡張機能の処理
ms.assetid: e5209a63-519b-42bd-882b-a1c3d2074deb
keywords:
- WDK Windows Sockets の拡張機能
- Windows ソケットは、WDK、拡張機能を直接します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 791e61956ea3374e2acf6dfba727263bcf926835
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559548"
---
# <a name="handling-microsoft-extensions-to-windows-sockets"></a>Windows ソケットに対する Microsoft 拡張機能の処理





Windows Sockets スイッチは、すべての Microsoft 固有の Windows Sockets 拡張関数を内部的に処理します。 Microsoft Windows SDK のドキュメントを公開するメカニズムが高度な拡張機能を定義する Windows Sockets では、アプリケーションのプログラム 機能を転送します。 これらの拡張機能は次のとおりです。**TransmitFile**、 **AcceptEx**、および**GetAcceptExSockAddrs**します。 スイッチは、必要に応じて、これらの呼び出しに変換し、適切な SAN サービス プロバイダー関数に転送します。[**WSPSend**](https://msdn.microsoft.com/library/windows/hardware/ff566316)、 [ **WSPAccept**](https://msdn.microsoft.com/library/windows/hardware/ff566266)、 [ **WSPRdmaWrite**](https://msdn.microsoft.com/library/windows/hardware/ff566306)、または[ **WSPRdmaRead**](https://msdn.microsoft.com/library/windows/hardware/ff566304)します。

 

 




