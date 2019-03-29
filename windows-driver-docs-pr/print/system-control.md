---
title: システム コントロール
description: システム コントロール
ms.assetid: 3ac58d53-daa7-4f50-a512-05325b95a17d
keywords:
- WDK の印刷の色のシステム管理の対象の管理
- 既定の印刷時の色の管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11b4d2db6950f4089a4182af17289b40cf391212
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580617"
---
# <a name="system-control"></a>システム コントロール





色のシステム管理の対象の管理は、既定の色の管理の種類です。 プリンターの推奨される種類もです。 色の管理が有効になっている場合、GDI すべて Dib、ペンの色を修正して、入力と出力に基づいて、ドライバーのプリンター グラフィックス、DLL に送信する前にブラシのカラー スペースと ICC プロファイルがインストールされています。

ICM 固有のコードをサポート システム コントロールの色の管理、CYMK 色空間 (該当する場合)、「」のサポートを示す以外のプリンター ドライバーを追加する必要はありません[CMYK カラー領域をサポートしている](supporting-cmyk-color-space.md)します。

 

 




