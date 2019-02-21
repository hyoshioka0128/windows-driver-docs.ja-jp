---
title: Orientation
description: Orientation
ms.assetid: a3bd9d67-200f-4739-ad0e-ff7fd2eb20a3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c288d783764876a8c0f1e1fb72af312f9eec7fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560266"
---
# <a name="orientation"></a>Orientation


スキーマのパス:\\Printer.Layout.Orientation

ノード型: プロパティ

説明: ページの向きに関連付けられているプロパティ。 このプロパティの子である値のエントリは、現在のページの向きと、デバイスでサポートされているページの向きの一覧には。

Orientation プロパティには、2 つの子の値が含まれています。**CurrentValue**と**サポート**します。

### <a name="span-idcurrentvaluespanspan-idcurrentvaluespan-currentvalue"></a><span id="currentvalue"></span><span id="CURRENTVALUE"></span> CurrentValue

スキーマのパス:\\Printer.Layout.Orientation:CurrentValue

ノード型: 値

データ型: BIDI\_文字列

説明: 現在のページが印刷されます (既定値) の向き。

次の値のいずれかを指定する必要があります。

縦向き

横向き

ReversePortrait

ReverseLandscape

### <a name="span-idsupportedspanspan-idsupportedspan-supported"></a><span id="supported"></span><span id="SUPPORTED"></span> サポートされています

スキーマのパス:\\Printer.Layout.Orientation:Supported

ノード型: 値

データ型: BIDI\_文字列

説明: A 向きのサポートされているすべての値のコンマ区切り一覧。

 

 




