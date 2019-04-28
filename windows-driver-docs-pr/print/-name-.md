---
title: '\ 名前 \/'
description: '\ 名前 \/'
ms.assetid: 5259ea1a-a251-479b-88f1-711d5933868a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60ad341ded00ca35003f72d070765794133ffe1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372878"
---
# <a name="name"></a>\[名前\]


スキーマのパス:\\Printer.Consumables\[ 。名\]

ノード型: プロパティ

説明: このプロパティは、仕入先にマップされた使用できる名前。 名前は、この消耗品のベンダー固有の一意の ID に対応します。 この ID は、同じ種類と色の組み合わせで複数の消耗品の可能性をによりします。 \[名前\]プロパティは必須では常に、名前にスペースを含めることはできません。

このプロパティには、次の子の値が含まれています。

種類

色

インストール済み

Level

モーダル

### <a name="span-idtypespanspan-idtypespan-type"></a><span id="type"></span><span id="TYPE"></span> 型

スキーマのパス:\\Printer.Consumables\[ 。名前\]します。型

ノード型: 値

説明: この値は、参照先の消耗品の種類を表します。

次の定義済みの型を使用できます。

インク

トナー残量:

Developer

FuserOil

ワックス

WasteToner

WasteInk

WasteWax

ベンダーは、プロセスの印刷や印刷デバイスに固有の値を追加できます。

### <a name="span-idcolorspanspan-idcolorspan-color"></a><span id="color"></span><span id="COLOR"></span> 色

スキーマのパス:\\Printer.Consumables\[ 。名前\]します。色

ノード型: BIDI\_文字列

説明: この値は、参照先の消耗品の色を表します。 いくつかの種類を使用できるは実際に関連付けられている色があるないために、このデータ値は省略可能でします。

次の色の種類が事前に定義されています。

黒

青

色

シアン

灰色

[緑]

マゼンタ

PhotoBlack

PhotoColor

PhotoCyan

PhotoMagenta

PhotoYellow

[赤]

White

黄

各仕入先は、印刷、プロセスとデバイスに固有の任意の値を追加できます。

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> インストールされています。

スキーマのパス:\\Printer.Consumables\[ 。名前\]します。インストールされています。

ノード型: 値

データ型: BIDI\_BOOL

説明: この値は、デバイス上の種類と色を記述する消耗品がインストールされているかどうかを示します。

### <a name="span-idlevelspanspan-idlevelspan-level"></a><span id="level"></span><span id="LEVEL"></span> レベル

スキーマのパス:\\Printer.Consumables\[ 。名前\]します。レベル

ノード型: 値

データ型: BIDI\_INT

説明:この値は、参照先の消耗品の現在のレベルを表します。 この値の単位は、パーセント ポイントです。 フル レベル 100 の値になり、空のレベルが 0 の値になります。 レベルが測定可能でない場合は-1 (不明) の値が返されます。

### <a name="span-idmodelspanspan-idmodelspan-model"></a><span id="model"></span><span id="MODEL"></span> モデル

スキーマのパス:\\Printer.Consumables\[ 。名前\]します。モデル

ノード型: 値

［データの種類］:BIDI\_文字列

説明: 参照先の消耗品の仕入先のモデルのインジケーターを表すオプションの値。 この値は、正確に使用できるが、デバイスにインストールされている特定の種類と色の組み合わせのバージョンを区別するためにクライアントを有効にします。

 

 




