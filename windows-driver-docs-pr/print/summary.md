---
title: 概要
description: 概要
ms.assetid: 8ed412b2-1e7c-440f-8949-a3b1fff09b16
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d583201b00164b6082ed5d5a8f5b173838cb806a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538799"
---
# <a name="summary"></a>概要


スキーマのパス:\\Printer.Status.Summary

ノード型: プロパティ

デバイスの現在の状態の説明: A 簡単な説明。 これにより、デバイスの状態の概要を確認します。 最も重要な条件のみが表示されます。

サマリー プロパティには、2 つの子の値が含まれています。**状態**と**StateReason**します。

### <a name="span-idstatespanspan-idstatespanstate"></a><span id="state"></span><span id="STATE"></span>状態

スキーマのパス:\\Printer.Status.Summary:State

ノード型: 値

データ型: BIDI\_文字列

説明: デバイスの処理状態です。

次の値は使用できます。

アイドル

Processing

［停止］

### <a name="span-idstatereasonspanspan-idstatereasonspanstatereason"></a><span id="statereason"></span><span id="STATEREASON"></span>StateReason

スキーマのパス:\\Printer.Status.Summary:StateReason

ノード型: 値

データ型: BIDI\_文字列

説明: 現在のプリンターの状態の最も重要な理由です。 この値は、スペースで区切られた状態の理由の一覧を指定できます。

次の値は使用できます。

AttentionRequired

DoorOpen

MarkerSupplyEmpty

MarkerSupplyLow

MediaEmpty

MediaJam

MediaLow

MediaNeeded

なし

一時停止

OutputAreaAlmostFull

OutputAreaFull

 

 




