---
title: フィルム スキャナー アーキテクチャ
description: フィルム スキャナー アーキテクチャ
ms.assetid: fe3a2c23-a520-4701-8178-02f50ac08767
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f475358de358cdac39d7c8d854eebe67e6e48613
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323453"
---
# <a name="film-scanner-architecture"></a>フィルム スキャナー アーキテクチャ





スライドまたは透明度単位のスキャンをサポートするスキャナー デバイスは、WIA 項目のツリーでフィルム スキャナーの項目を実装する必要があります。 この WIA 項目は、プログラミング可能なデータ ソースを表します。 イメージを生成またはフィルム スキャナーのフィルムのスキャン データの転送時に画面に配置されているからイメージがこの項目から要求します。 フィルム スキャナーの項目は、WIA ルート項目から直接配置して、(フレームと呼ばれる) 1 つまたは複数の子項目を含める必要があります。 *フレーム*フィルム項目個々 の選択範囲と画面をスキャンするフィルムの選択領域の場所です。 WIA ドライバーには、かどうかどのようなことができます追加、削除、サイズ変更、またはエクステントの設定の有効な値を設定しても再配置が決定します。

次のトピックでは、フィルム スキャナーの 2 つの種類について説明します。

[フィルムのスキャンをサポートするためのフラット ベッド スキャナー](flatbed-scanners-that-support-film-scanning.md)

[専用のフィルム スキャナー](dedicated-film-scanners.md)

 

 




