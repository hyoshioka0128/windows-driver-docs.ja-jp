---
title: カーネルセキュリティサポートルーチン
description: カーネルセキュリティサポートルーチン
ms.assetid: d8ee86dc-8327-4c0b-b916-cc6763d87178
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7d5b2240ff0cad8ed5f13beac398525624baa39e
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955778"
---
# <a name="kernel-security-support-routines"></a>カーネルセキュリティサポートルーチン

カーネルセキュリティドライバー (KSECDD) によって提供される、システムによって提供されるカーネルセキュリティサポートルーチンを次に示します。SYS) は、カーネルモードのファイルシステムおよびファイルシステム (ミニフィルターおよびレガシ) フィルタードライバーで使用できます。

**ヘッダーファイル:** *ntifs*

** プレフィックス:秒 @ no__t ~ 0_Xxx_

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **SecLookupAccountName** | アカウントを入力として受け取り、アカウントのセキュリティ識別子 (SID) と、アカウントが見つかったドメインの名前を取得します。 |
| **SecLookupAccountSid** | 入力としてセキュリティ識別子 (SID) を受け取ります。 この SID のアカウント名と、この SID が検出された最初のドメインの名前を取得します。 |
| **SecLookupWellKnownSid** | は、既知のセキュリティ識別子 (SID) の種類を入力として受け取り、この既知の SID のローカルセキュリティ識別子 (SID) を取得します。 |
| **SecMakeSPN** | 特定のセキュリティサービスプロバイダーと通信するときに使用できるサービスプロバイダー名文字列を作成します。 |
| **SecMakeSPNEx** | 特定のセキュリティサービスプロバイダーと通信するときに使用できるサービスプロバイダー名文字列を作成します。 |
| **SecMakeSPNEx2** | 特定のセキュリティサービスプロバイダーと通信するときに使用できるサービスプロバイダー名文字列を作成します。 |
