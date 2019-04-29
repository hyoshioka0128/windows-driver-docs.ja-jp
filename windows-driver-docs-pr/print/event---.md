---
title: Event\ \ \
description: Event\ \ \
ms.assetid: a3b0b3f1-03d6-4309-9efe-d2588c7240cb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8a68c1b668ad98fe333b55db5bb21726f67dc33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324238"
---
# <a name="event"></a>イベント\#\#\#


スキーマのパス:\\Printer.Status.Detailed.Event\#\#\#

ノード型: プロパティ

説明: A には、デバイスのイベント Id に基づくイベント名が生成されます。 各数値のサフィックスは、特定のイベントに対して一意である必要があります。 場合は、デバイスでは、特定の数値のサフィックスが再利用は、アプリケーション数値のサフィックスに以前関連付けられているイベントの有効期限が切れているかどうかを判断するための十分な時間を許可する必要があります。 このプロパティには、すべての対象となるイベントを記述する値のエントリが含まれています。

イベント\#\# \#プロパティ名と重要度、2 つの子値が含まれますの親である、[コンポーネント](component2.md)プロパティ。

### <a name="span-idnamespanspan-idnamespan-name"></a><span id="name"></span><span id="NAME"></span> 名

スキーマのパス:\\Printer.Status.Detailed.Event\#\#\#: 名前

ノード型: 値

データ型: BIDI\_文字列

現在のエラー状態の説明: A 簡単な説明。 各コンポーネントの異なるイベント名があります。

名前の一般的な値は次のとおりです。

CoverOpen

紙詰まり

DoorOpen

InputTrayMissing

InputTrayMediaSizeChange

InputTrayMediaTypeChange

InputTraySupplyLow

InputTraySupplyEmpty

OutputTrayMissing

OutputTrayAlmostFull

OutputTrayFull

FuserUnderTemperature

FuserOverTemperature

ConsumableLow

ConsumableEmpty

WasteReceptacleAlmostFull

WasteReceptacleFull

### <a name="span-idseverityspanspan-idseverityspan-severity"></a><span id="severity"></span><span id="SEVERITY"></span> 重要度

スキーマのパス:\\Printer.Status.Summary:Detailed します。イベント\#\#\#: 重大度

ノード型: 値

データ型: BIDI\_文字列

説明: 現在のイベントの重大度レベル。 プリンターは、エラー状態に割り当てられた重大度レベルを決定します。

次の値は使用できます。

情報

警告

重大

 

 




