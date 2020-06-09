---
title: システム クラッシュの強制実行
description: システム クラッシュの強制実行
ms.assetid: db93b032-2ca7-4197-87dd-4ae77c328f60
keywords:
- システムクラッシュ、概要
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7e235df3c63b47efe9629faecb71e69a97d1ce21
ms.sourcegitcommit: 8097a09d2f989a9b3dca250c4e2ffd4cec2172e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84563156"
---
# <a name="forcing-a-system-crash"></a>システム クラッシュの強制実行

カーネルモードのダンプファイルを[有効](enabling-a-kernel-mode-dump-file.md)にすると、ほとんどのシステムクラッシュでクラッシュファイルが書き込まれ、青い画面が表示されます。

ただし、実際にカーネルクラッシュを開始することなくシステムがフリーズすることがあります。 このような凍結には、次のような症状が考えられます。

- マウスポインターは移動しますが、何もすることはできません。

- すべてのビデオは固定されています。マウスポインターは移動しませんが、ページングは続行されます。

- マウスまたはキーボードに対する応答はまったくなく、ディスクは使用されません。

経験豊富なデバッグ技術者が存在する場合は、カーネルデバッガーをアタッチして問題を分析することができます。 このような状況が発生した場合の対処方法に関するヒントについては、「停止した[システムのデバッグ](debugging-a-stalled-system.md)」を参照してください。

ただし、技術者が存在しない場合は、カーネルモードのダンプファイルを作成して、オフサイトの技術者に送信することをお勧めします。 このダンプファイルを使用すると、エラーの原因を分析できます。

システムのクラッシュを意図的に発生させるには、次の2つの方法があります。

[デバッガーからのシステム クラッシュの強制実行](forcing-a-system-crash-from-the-debugger.md)

[キーボードからのシステム クラッシュの強制実行](forcing-a-system-crash-from-the-keyboard.md)
