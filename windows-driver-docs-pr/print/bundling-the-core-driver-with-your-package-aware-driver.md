---
title: パッケージ対応ドライバーでコア ドライバーをバンドルする
description: パッケージ対応ドライバーでコア ドライバーをバンドルする
ms.assetid: 72e29f79-4e71-4aa8-929f-eefdebfe4835
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9de28136f4b3baa54cc479d36417c35ba8d23aa3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582103"
---
# <a name="bundling-the-core-driver-with-your-package-aware-driver"></a>パッケージ対応ドライバーでコア ドライバーをバンドルする


したら[展開](getting-the-updated-core-driver-package.md)core のドライバー パッケージを含む Microsoft のスタンドアロン更新プログラム (MSU) ファイルの内容は、[次へ] の手順では、パッケージに対応したドライバーを使用したコア ドライバーをバンドルします。

パッケージに対応したドライバーのファイルが含まれているディレクトリに変更し、コアのドライバー パッケージにサブディレクトリを作成します。 これらのパッケージはアーキテクチャに固有であり、アーキテクチャごとに適切なコアのドライバー パッケージを含めるし、これらのコア ドライバー パッケージが含まれているサブディレクトリに適切な名前を割り当てる必要がありますマルチ アーキテクチャのドライバーを配布する場合。 新しいサブディレクトリに MSU ファイルが含まれるコアが更新されたドライバー パッケージ サブディレクトリの内容をコピーします。 その他の変更は必要ありません。 改ざんしたり、デジタル署名は、コア ドライバー パッケージを変更しないでください。 パッケージの内容を変更しない限り、署名が有効な残ります。

 

 




