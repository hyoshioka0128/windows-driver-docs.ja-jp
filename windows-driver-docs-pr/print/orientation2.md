---
title: 方向
description: 方向
ms.assetid: a3bd9d67-200f-4739-ad0e-ff7fd2eb20a3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c288d783764876a8c0f1e1fb72af312f9eec7fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362748"
---
# <a name="orientation"></a>方向


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

 

 




