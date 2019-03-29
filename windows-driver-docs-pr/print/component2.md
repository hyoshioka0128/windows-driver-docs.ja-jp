---
title: コンポーネント
description: コンポーネント
ms.assetid: 15cc741e-5919-4d71-802b-519494827722
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4481b65a74fa282f69a39f3b4bec63945111490b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571975"
---
# <a name="component"></a>コンポーネント


スキーマのパス:\\Printer.Status.Summary:Detailed します。イベント\#\#\#します。コンポーネント

データ型: プロパティ

説明: このプロパティには、現在のイベントによって影響を受ける印刷デバイスの一部を記述する値のエントリが含まれています。

コンポーネントのプロパティには、2 つの子の値が含まれています。グループと名前です。

### <a name="span-idgroupspanspan-idgroupspan-group"></a><span id="group"></span><span id="GROUP"></span> グループ

スキーマのパス:\\Printer.Status.Summary:Detailed します。イベント\#\#\#します。コンポーネント グループ:

ノード型: 値

データ型: BIDI\_文字列

説明: 現在のイベントによって影響を受けるコンポーネント グループ。 コンポーネント グループとコンポーネントの名前 (次の説明) は、問題の正確な場所を特定する結合されます。 次の一覧には、グループの一般的な値が含まれています。

InputBin

MediaPath

OutputBins

コンシューマブル

### <a name="span-idnamespanspan-idnamespan-name"></a><span id="name"></span><span id="NAME"></span> 名

スキーマのパス:\\Printer.Status.Detailed.Event\#\#\#します。コンポーネント名:

ノード型: 値

データ型: BIDI\_文字列

説明: 現在のイベントによって影響を受ける個々 のコンポーネントの名前。 コンポーネント名と (上) のコンポーネント グループは、問題の正確な場所を特定する結合されます。

標準値*名前*次に示します。

トレイ 1

TopBin

LargeCapacityBin

OutputBin1

Toner.Black

Ink.Cyan

 

 




