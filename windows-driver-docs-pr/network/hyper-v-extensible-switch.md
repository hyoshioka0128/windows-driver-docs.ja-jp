---
title: Hyper-v 拡張可能スイッチの概要
description: Hyper-v 拡張可能スイッチでは、NDIS フィルタードライバー (拡張可能スイッチ拡張機能と呼ばれます) のインスタンスが拡張可能なスイッチドライバースタック内でバインドできるインターフェイスがサポートされています。
ms.assetid: FB6AA190-0DB1-441E-9BC6-2FD3A6D88114
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb0144903b92991bf75a0fa9b015f382a86f069e
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565754"
---
# <a name="introduction-to-hyper-v-extensible-switch"></a>Hyper-v 拡張可能スイッチの概要

Hyper-v 拡張可能スイッチでは、NDIS フィルタードライバー (*拡張可能スイッチ拡張機能*と呼ばれます) のインスタンスが拡張可能なスイッチドライバースタック内でバインドできるインターフェイスがサポートされています。 バインドして有効にすると、拡張機能はパケットを監視、変更、および拡張可能なスイッチポートに転送できます。 これにより、拡張機能は、Hyper-v パーティションによって使用されるポートに対して、パケットの拒否、リダイレクト、または発信を行うことができます。

Hyper-v 拡張可能スイッチは、Windows Server 2012 の NDIS 6.30 以降でサポートされています。

ここでは、Hyper-v 拡張可能スイッチとそのインターフェイスについて説明する次のトピックについて説明します。

-   [Hyper-v 拡張可能スイッチ拡張機能の作成はじめに](getting-started-writing-a-hyper-v-extensible-switch-extension.md)
-   [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)
-   [Hyper-v 拡張可能スイッチのアーキテクチャ](hyper-v-extensible-switch-architecture.md)
-   [Hyper-v 拡張可能スイッチ拡張機能の記述](writing-hyper-v-extensible-switch-extensions.md)
-   [Hyper-v 拡張可能スイッチ拡張機能のインストール](installing-hyper-v-extensible-switch-extensions.md)
-   [Hyper-v 拡張可能スイッチ Oid](hyper-v-extensible-switch-oids.md)

 

 





