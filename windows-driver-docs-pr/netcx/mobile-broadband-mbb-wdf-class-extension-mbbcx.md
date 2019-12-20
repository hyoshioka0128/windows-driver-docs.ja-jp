---
title: モバイル ブロードバンド (MBB) WDF クラス拡張機能 (MBBCx) の概要
description: モバイルブロードバンド (MBB) WDF クラス拡張の概要 (MBBCx)。
ms.assetid: FA4D1C2D-270B-40C4-A922-8ABDDE4D8444
keywords:
- モバイルブロードバンド (MBB) WDF クラス拡張、MBBCx、モバイルブロードバンド NetAdapterCx
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: a4b530ebfadb77f929541345a952c52ba08f77fd
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210816"
---
# <a name="introduction-to-the-mobile-broadband-mbb-wdf-class-extension-mbbcx"></a>モバイル ブロードバンド (MBB) WDF クラス拡張機能 (MBBCx) の概要

Windows 10 の次期リリース以降、Windows Driver Kit (WDK) には、NetAdapterCx と連携するモバイルブロードバンド (MBB) WDF クラスの拡張機能が含まれています。 MBB クライアントドライバーは、最初は最も重要な WDF クライアントドライバーであり、他の NIC ドライバーと同様に NetAdapterCx クライアントドライバーであり、最後に、MBBCX メディア固有のドライバーを提供する MBB クラス拡張 (MBB) のクライアントドライバーです。機. 次のブロック図は、MBBCx アーキテクチャを示しています。

![MbbCx アーキテクチャ](images/MbbCx.png)

MBB アダプタークライアントドライバーは、フレームワークとの関係に基づいて、3つのカテゴリのタスクを実行します。

- Pnp や電源管理などの一般的なデバイスタスクには、[標準の WDF api](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)を呼び出します。
- ネットワークパケットの送信や受信など、一般的なネットワークデバイス操作に[NetAdapterCx api](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/#netadaptercx)を呼び出します。
- MBIM メッセージ処理のような MBB 固有のコントロールパス操作に対して[MbbCx api](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/#mbbcx)を呼び出します。

開始する前に、次の概念を理解しておく必要があります。

- [Windows Driver Foundation (WDF)](../wdf/using-the-framework-to-develop-a-driver.md)
- [NetAdapter クラス拡張 (NetAdapterCx)](index.md)

このセクションのトピックでは、基本的な NIC 用に NetAdapterCx クライアントドライバーを記述する方法が既にわかっていることを前提としているため、MBBCx 固有のコードにのみ焦点を当てます。

このセクションでは、次のトピックについて説明します。

- [Writing an MBBCx client driver (MBBCx クライアント ドライバーの作成)](writing-an-mbbcx-client-driver.md)
