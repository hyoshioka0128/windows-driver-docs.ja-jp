---
title: 共同インストーラーの記述
description: 共同インストーラーの記述
ms.assetid: d5637321-9cff-4b24-8941-d3ca16b0d8c1
keywords:
- デバイス セットアップ WDK デバイスのインストール、共同インストーラー
- デバイスのインストール co-installer を WDK
- デバイス co-installer を WDK をインストールします。
- 共同インストーラーについて、co-installer WDK デバイスのインストール
- WDK 共同インストーラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 812c7d40cf4da3d6c323f92fd934faea7c8ecf24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339259"
---
# <a name="writing-a-co-installer"></a>共同インストーラーの記述





**注**  ユニバーサルまたはモバイルのドライバー パッケージでは、このセクションで説明する機能はサポートされていません。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

共同インストーラーは、デバイスのインストールに役立つ Microsoft Win32 DLL です。 共同インストーラーは、クラスのインストーラーの「ヘルパー」として SetupAPI によって呼び出されます。 たとえば、仕入先は、デバイスに固有の情報を INF ファイルで処理できません。 レジストリに書き込むの共同インストーラーを提供できます。

ここでは、次のトピックについて説明します。

[共同インストーラー操作](co-installer-operation.md)

[共同インストーラー インターフェイス](co-installer-interface.md)

[共同インストーラーの機能](co-installer-functionality.md)

[差分のコードの処理](handling-dif-codes.md)

[共同インストーラーを登録します。](registering-a-co-installer.md)

 

 





