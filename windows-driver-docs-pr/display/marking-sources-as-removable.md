---
title: リムーバブルとしてソースをマークします。
description: リムーバブルとしてソースをマークします。
ms.assetid: 7fe48a4b-25d2-4e2c-9c26-a425928947ce
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6e645c8f2454b9afe5190806172a5f1c8ac01db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558014"
---
# <a name="marking-sources-as-removable"></a>リムーバブルとしてソースをマークします。


ビデオの存在するソースをプライマリ ビュー表示のアプリケーションを防ぐためには、リムーバブルとソースをマークする必要があります。 リムーバブルどのソースを示す、という名前のレジストリの DWORD のプラグ アンド プレイ (PnP) の値を指定できます**RemovableSources**します。

**注**  ソース 0 リムーバブルとして DWORD 値のビット フィールドをマークすることはできません。

 

N<sup>th</sup>ビット フィールドの値のビットは、ソース n-1 が取り外し可能かどうかを指定します。 たとえば、リムーバブルとしてソース 1 をマークするには、ディスプレイ ミニポート ドライバーの INF ファイルに次の行を追加できます。

```inf
HKR,, RemovableSources, %REG_DWORD%, 2
...
```

ディスプレイ ドライバーのインストールの詳細については、[ミニポートの表示と表示のユーザー モード ドライバーのインストール要件](installing-display-miniport-and-user-mode-display-drivers.md)を参照してください。

 

 





