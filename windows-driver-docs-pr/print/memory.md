---
title: メモリ (印刷)
description: 印刷デバイスにインストールされているメモリの値のエントリ
ms.assetid: 9e1ad59f-9a97-49d7-b749-14380067cf64
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 45d7702b716f4a7a188d6170e181aecf40d90310
ms.sourcegitcommit: ff2f72fe98f6ba559c1c01b17d25c773df7337c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86060802"
---
# <a name="memory-print"></a>メモリ (印刷)

スキーマパス: \\Printer.Configuration。量

ノードの種類: プロパティ

説明: デバイスにインストールされているメモリの値のエントリ

Memory プロパティには、**サイズ**と**PS**という2つの子値が含まれています。

## <a name="size"></a>サイズ

スキーマパス: \\Printer.Configuration。メモリ: サイズ

ノードの種類: 値

データ型: BIDI \_ INT

説明: デバイスにインストールされている物理メモリの量 (KB 単位)。

## <a name="ps"></a>PS

スキーマパス: \\Printer.Configuration。メモリ: PS

ノードの種類: 値

データ型: BIDI \_ INT

説明: デバイスの Postscript インタープリターで使用可能なメモリの量 (kb 単位)。 この値は、インストールされている物理メモリの量よりも少なくする必要があります。
