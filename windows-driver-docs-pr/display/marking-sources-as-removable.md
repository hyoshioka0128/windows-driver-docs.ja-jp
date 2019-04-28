---
title: リムーバブルとしてのソースのマーキング
description: リムーバブルとしてのソースのマーキング
ms.assetid: 7fe48a4b-25d2-4e2c-9c26-a425928947ce
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6e645c8f2454b9afe5190806172a5f1c8ac01db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370742"
---
# <a name="marking-sources-as-removable"></a>リムーバブルとしてのソースのマーキング


ビデオの存在するソースをプライマリ ビュー表示のアプリケーションを防ぐためには、リムーバブルとソースをマークする必要があります。 リムーバブルどのソースを示す、という名前のレジストリの DWORD のプラグ アンド プレイ (PnP) の値を指定できます**RemovableSources**します。

**注**  ソース 0 リムーバブルとして DWORD 値のビット フィールドをマークすることはできません。

 

N<sup>th</sup>ビット フィールドの値のビットは、ソース n-1 が取り外し可能かどうかを指定します。 たとえば、リムーバブルとしてソース 1 をマークするには、ディスプレイ ミニポート ドライバーの INF ファイルに次の行を追加できます。

```inf
HKR,, RemovableSources, %REG_DWORD%, 2
...
```

ディスプレイ ドライバーのインストールの詳細については、次を参照してください。[ミニポートの表示と表示のユーザー モード ドライバーのインストール要件](installing-display-miniport-and-user-mode-display-drivers.md)します。

 

 





