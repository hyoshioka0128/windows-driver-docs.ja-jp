---
title: Windows メタデータとインターネット サービス
description: Windows メタデータとインターネット サービス
ms.assetid: 9e814be5-e22a-48d5-b46b-d22baa89e229
keywords:
- WMIS
- WDK のメタデータ情報サーバー
- WDK のメタデータ サーバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e69ca81bdec134728d3dbd31b634ae3cbfb08ffa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531578"
---
# <a name="windows-metadata-and-internet-services"></a>Windows メタデータとインターネット サービス


Windows メタデータとインターネット サービス (WMIS) は、Oem に送信されるデバイス メタデータ パッケージを管理、 [Windows Quality Online Services (Winqual)](https://go.microsoft.com/fwlink/p/?linkid=62651)インターネット経由で web サイト。 Winqual のサイトを使用すると、ハードウェア デバイスと Windows のソフトウェア アプリケーションを証明することができます。

OEM は、デバイス メタデータ パッケージを送信するときに、Winqual は、次のプロセスを実行します。

1.  デバイス メタデータ パッケージ内に含まれる XML ドキュメントを検証し、検証に合格したパッケージにデジタル署名します。

2.  パッケージを利用 WMIS を配布し、リモート コンピューターにインストールできるようにします。

Windows 7 および Windows の以降のバージョンでは、オペレーティング システムは、検出、インデックス、およびコンピューターに接続されている特定のデバイスのデバイス メタデータ パッケージと一致する WMIS を使用します。 このプロセスの詳細については、次を参照してください。 [WMIS からデバイス メタデータ パッケージをインストールする](installing-device-metadata-packages-from-wmis.md)します。

 

 





