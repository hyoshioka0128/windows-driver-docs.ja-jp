---
title: 複数ページのスキャンと TWAIN
description: 複数ページのスキャンと TWAIN
ms.assetid: 02b5ef48-413d-403b-8c42-caecd9521067
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 921006eaed7cc236ddfc30f4fee701745478c260
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571184"
---
# <a name="multipage-scanning-and-twain"></a>複数ページのスキャンと TWAIN





Windows XP 以降、TWAIN 互換性レイヤー スキャンをサポート マルチページ スクロール フィードのデバイスからスキャンしたすべてのページが同じ長さを指定します。 その理由は、その TWAIN は、最初のページでのみページの長さの詳細については、呼び出し元のアプリケーションから情報を取得します。 TWAIN はページ間でのイメージ情報を要求する呼び出し元のアプリケーションは必要ありません。 さらに、TWAIN 後続のすべてのページに最初のページについて、アプリケーションから受信した情報を適用します。

 

 




