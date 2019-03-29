---
title: NDIS ライブラリへのリンク
description: NDIS ライブラリへのリンク
ms.assetid: eac33c9e-ff70-4a6c-b391-833a81faa079
keywords:
- NDIS.sys WDK networking
- NDIS ライブラリ WDK ネットワーク
- NDIS ライブラリ WDK ネットワークのリンク
- WDK NDIS ライブラリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e0f8c87319aa9bb25b8428d3fe3349e63740b5a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571531"
---
# <a name="linking-to-the-ndis-library"></a>NDIS ライブラリへのリンク





NDIS ライブラリは、最大のパフォーマンスのマクロに重点を置いて、関数のセットとして Ndis.sys、カーネル モードのエクスポート ライブラリでは、パッケージ化されます。 (エクスポート ライブラリは、ダイナミック リンク ライブラリに同様に機能する .sys ファイルです)。すべての NDIS ドライバーでは、NDIS ライブラリに自体をリンクします。 NDIS ライブラリ関数は、Microsoft Windows Driver Kit (WDK) ドキュメントのネットワーク リファレンスのセクションで説明します。

WDK は、ミニポート ドライバーのメイン ヘッダー ファイルとして Ndis.h を提供します。 このファイルは、ミニポート ドライバーでは、NDIS ライブラリ関数、および一般的なデータ構造のエントリ ポイントを定義します。 ネットワークのリファレンス セクションには、ミニポート ドライバー、プロトコルのドライバーがについて説明しますと**Ndis * Xxx*** 関数と、共通のデータ構造体と Oid。

 

 





