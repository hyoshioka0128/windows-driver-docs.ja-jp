---
title: TWAIN と互換性のあるアプリケーションのサポート
description: TWAIN と互換性のあるアプリケーションのサポート
ms.assetid: 8135178f-a432-4200-81c3-8e12112637f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f85504c59a7a4fec15c56901e971785ce8c582fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536764"
---
# <a name="support-for-twain-compatible-applications"></a>TWAIN と互換性のあるアプリケーションのサポート





プライベートの機能を備えた TWAIN アプリケーションをサポートするために、WIA ドライバーと呼ばれる手法を使用できます*パススルー*機能します。 パススルーのメカニズムは、TWAIN と互換性のあるアプリケーションは、仲介者として、データ ソースのマネージャーと TWAIN 互換性レイヤーを使用して、WIA ドライバーと通信する方法を参照します。 TWAIN 機能パススルーが Windows XP およびそれ以降のオペレーティング システム バージョンでのみサポートされていることに注意してください。 重要です。

データ ソースのマネージャーに TWAIN と互換性のあるアプリケーションと、WIA ドライバーの間のすべての通信は最初 (*twain\_32. dll*)、TWAIN 互換性レイヤーをさらに呼び出し (*wiadss.dll*). TWAIN 互換性レイヤーを呼び出して、 **IWiaItemExtras::Escape**メソッドを呼び出す、 **IStiUSD::Escape**メソッド。 TWAIN 互換レイヤーの呼び出しのみ、 **IWiaItemExtras::Escape**メソッド。 ドライバーの開発者は、デバイスの受信のみを考慮する必要があります、 **IStiUSD::Escape**呼び出します。 詳細については**IWiaItemExtras::Escape**、Microsoft Windows SDK のドキュメントを参照してください。

**注**   TWAIN パススルー機能の目的は、TWAIN ドライバーから WIA ドライバーへの移行を行っているドライバー開発者にサポートを提供します。 WIA ドライバーに TWAIN 機能を追加するためのものではありません。 WIA ドライバーで TWAIN のサポートが必要ない場合は、ドライバーにこの機能を追加する必要がありますできません。

 

このセクションでは、次のトピックがについて説明します。

[WIA ドライバーでは、TWAIN 機能パススルーを有効にします。](enabling-twain-capability-pass-through-in-a-wia-driver.md)

[IStiUSD エスケープ メソッドを使用してください。](using-the-istiusd-escape-method.md)

 

 




