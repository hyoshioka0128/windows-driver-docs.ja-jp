---
title: ネットワーク リダイレクターは
description: ネットワーク リダイレクターは
ms.assetid: 5c966d92-7796-4cba-a90e-8c83240655ce
keywords:
- ネットワーク リダイレクターに関するネットワーク リダイレクター WDK、
- ネットワーク リダイレクターについてリダイレクター ドライバー WDK、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be38f977df4a49dd7ecfcad4aa71472fae169717
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322308"
---
# <a name="what-is-a-network-redirector"></a>ネットワーク リダイレクターについて


## <span id="ddk_what_is_a_network_redirector_if"></span><span id="DDK_WHAT_IS_A_NETWORK_REDIRECTOR_IF"></span>


ネットワーク リダイレクターは、ファイルとリモート システム上の他のリソース (プリンターやプロッターの例では、) にアクセスするために使用するクライアント コンピューターにインストールされているソフトウェア コンポーネントで構成されます。 ネットワーク リダイレクターを送信します (またはリダイレクト)、要求の処理をリモート サーバーにローカル クライアント アプリケーションからのファイル操作の要求。 ネットワーク リダイレクターは、ローカルのアプリケーションに返される、リモート サーバーから応答を受信します。 ネットワーク リダイレクター ソフトウェアは、ローカル ファイルとリソースとしては、同じリモート ファイルとリソース、および使用し、同じ方法で操作することができますにクライアント システム上、外観に作成します。

ネットワーク リダイレクターがリモート リソースにアクセスをローカル クライアント アプリケーションをできるだけ透過的に作成しようとするとします。 ネットワークの問題がある場合は何回か前に、ネットワーク リダイレクターを放棄し、クライアント アプリケーションにエラーが返されますを要求に再試行されます。

このセクションには、次のトピックが含まれます。

[ネットワーク リダイレクターの基本的なアーキテクチャ](basic-architecture-of-a-network-redirector.md)

 

 




