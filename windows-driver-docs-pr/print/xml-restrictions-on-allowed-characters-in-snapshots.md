---
title: スナップショットの許可されている文字の XML 制限
description: スナップショットの許可されている文字の XML 制限
ms.assetid: e90fb0f2-28f7-4264-bd8c-cd5994717bad
keywords:
- スナップショット WDK の GDL が許可される文字
- GDL WDK、ソース ファイル
- GDL WDK、文字列
- ソース ファイル WDK GDL
- 文字列の文字を許可されている、WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a3a152ef4fd6303e7f9991e6f6ea1148949b535
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355248"
---
# <a name="xml-restrictions-on-allowed-characters-in-snapshots"></a>スナップショットの許可されている文字の XML 制限


XML ソース ファイルは、制御文字 (つまり、0x20 16 進数よりも小さい ANSI 値でこれらの文字など) のみを含めることができます。0x09、0x0a、および 0x0d です。 この制限は、GDL ソース ファイルが XML で禁止している制御文字を含めることはできませんを意味します。 GDL 文字列の内容は、(16 進文字列の値が、対応する ANSI または Unicode に変換、) を持つ XML 文字列に直接マップされて、GDL 文字列する必要がありますや、禁止されている制御文字または 16 進文字列形式を使用して表現します。 ただし、コマンド文字列、解釈されないため、引き続きできますを 16 進文字列形式を使用して制御文字を表します。

 

 




