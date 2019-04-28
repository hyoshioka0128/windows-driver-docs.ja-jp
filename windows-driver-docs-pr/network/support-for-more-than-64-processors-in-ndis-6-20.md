---
title: NDIS 6.20 の 64 を超えるプロセッサのサポート
description: NDIS 6.20 の 64 を超えるプロセッサのサポート
ms.assetid: 3fb2a09c-e2dd-48b8-a631-3793bd023ef0
keywords:
- NDIS 6.20 WDK、64 を超えるプロセッサのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebeb4656b3ad69370d7da6899d8ac1f113b8a986
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368234"
---
# <a name="support-for-more-than-64-processors-in-ndis-620"></a>NDIS 6.20 の 64 を超えるプロセッサのサポート





NDIS 6.20 インターフェイスには、64 を超えるプロセッサのサポートが導入されています。 以前のバージョンの NDIS は 64 個のプロセッサに制限されます (x86 32 オペレーティング システムのバージョン)。

旧バージョンとのまま、以前の実装と互換性のある NDIS をサポートしていますのプロセッサ グループ。 64 を超えるプロセッサをサポートするために更新されていないソフトウェアの既定のプロセッサ グループ 0 にできます。

64 を超えるプロセッサ、NDIS 6.20 が動作をサポートし、後でこれらのインターフェイスの更新バージョンを指定します。

-   [Receive Side Scaling (RSS)](ndis-receive-side-scaling2.md)

-   プロセッサ情報デバイス ドライバー インターフェイス (を参照してください[NDIS システム情報関数](https://msdn.microsoft.com/library/windows/hardware/ff564816))

-   リソースの割り当て (を参照してください[NDIS メモリ管理インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff564749))

-   読み取り/書き込みロック (を参照してください[NDIS 読み取り書き込みロック参照](https://msdn.microsoft.com/library/windows/hardware/ff564797))

デバイス ドライバーの NDIS インターフェイス要素の一部は、NDIS 6.20 が動作し、以降のドライバーの廃止されています。 古い形式のインターフェイスの詳細については、次を参照してください。 [NDIS 6.20 で古いインターフェイス](obsolete-interfaces-in-ndis-6-20.md)します。

 

 





