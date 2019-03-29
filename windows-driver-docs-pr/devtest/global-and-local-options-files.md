---
title: グローバル オプション ファイルとローカル オプション ファイル
description: グローバル オプション ファイルとローカル オプション ファイル
ms.assetid: 9b367e9f-f711-4b76-b331-7563edebb79c
keywords:
- ファイル WDK Static Driver Verifier のオプション
- グローバル オプション ファイル WDK Static Driver Verifier
- ローカル オプション ファイル WDK Static Driver Verifier
ms.date: 04/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9885e409667ee065f8336d3408c3f8286c5fe09b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577977"
---
# <a name="global-and-local-options-files"></a>グローバル オプション ファイルとローカル オプション ファイル


Sdv default.xml ファイル システム上の複数のコピーを持ち、ファイルのコピー内の値を編集することができます。

2 種類のオプションのファイルがあります。

-   *グローバル オプション ファイル*SDV でインストールする sdv default.xml ファイルには、\\ツール\\sdv\\データ\\*&lt;drivermodel&gt;* WDK のサブディレクトリ。 これらのファイル内の値は、ローカル オプション ファイル、ソース ディレクトリがあるドライバーの検証を除く driver model (WDM、WDF、NDIS、または Storport) に従って、SDV の検証にすべてに適用されます。

-   A*ローカル オプション ファイル*ドライバーのソース ディレクトリにある sdv default.xml のコピーです。 コピーは、sdv default.xml ファイル名が必要です。 ローカル オプション ファイルの値は、そのドライバーの検証にのみ適用されます。 SDV には、ドライバーのプロジェクト ディレクトリ内のローカル オプション ファイルが検出されると、そのファイルを使用して、グローバル オプション ファイル内の値は無視されます。

**注意**  移動またはグローバル オプション ファイルから削除、\\ツール\\sdv\\データ\\*&lt;drivermodel&gt;* サブディレクトリとそれらの名前を変更していません。 ローカル オプション ファイルを作成するには、グローバル オプション ファイルのコピーを作成し、ドライバーのプロジェクト ディレクトリ内に配置します。 グローバル オプション ファイルが見つからない場合、\\ツール\\sdv\\データ\\*&lt;drivermodel&gt;* サブディレクトリ、SDV は、検証を終了します。「Sdv default.xml が見つかりませんでした」エラー メッセージが表示されます。

 

 

 





