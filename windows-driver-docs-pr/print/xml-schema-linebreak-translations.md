---
title: XML スキーマ改行変換
description: XML スキーマ改行変換
ms.assetid: c277984f-8e7a-4d17-98ab-66c3f6f80473
keywords:
- linebreak シーケンス WDK GDL
- GDL WDK、スキーマ
- WDK GDL スキーマ
- スナップショット WDK GDL、linebreak
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a7261ee2e7633f55fbfb286b81db1bc1c52ae45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581427"
---
# <a name="xml-schema-linebreak-translations"></a>XML スキーマ改行変換


XML のスナップショットは、次の 2 つの文字シーケンスの改行を表します。&lt;0 d&gt;&lt;0a&gt; (CR LF)。 ただし、内&lt;CDATA&gt;セクションでは、文字列値、およびネイティブ XML データ型の値、GDL ソース ファイルに含まれる生の文字シーケンスを引用符で囲まれたを正確に使用します。 この使用法は、GDL データの作成者を使用する改行シーケンスの選択に含まれる情報の損失を防ぎます。

 

 




