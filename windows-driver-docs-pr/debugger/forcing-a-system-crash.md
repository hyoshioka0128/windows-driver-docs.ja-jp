---
title: システム クラッシュの強制実行
description: システム クラッシュの強制実行
ms.assetid: db93b032-2ca7-4197-87dd-4ae77c328f60
keywords:
- システムのクラッシュ、概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa70c7824b0327ecc0cbc01ca47a7bd4b55885a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572602"
---
# <a name="forcing-a-system-crash"></a>システム クラッシュの強制実行


## <span id="ddk_forcing_a_system_crash_dbg"></span><span id="DDK_FORCING_A_SYSTEM_CRASH_DBG"></span>


カーネル モードのダンプ ファイルがされる[有効になっている](enabling-a-kernel-mode-dump-file.md)、クラッシュ ファイルを書き込むと表示されるブルー スクリーンにほとんどのシステムがクラッシュが発生します。

ただし、実際にカーネル クラッシュを開始せず、システムがフリーズする時間があります。 このような凍結の考えられる症状は次のとおりです。

-   マウス ポインターが移動するが何もできません。

-   すべてのビデオを凍結すると、マウス ポインターが移動されないはページングが続行されます。

-   応答がありませんまったくに、マウスまたはキーボード、およびディスクは使用されていません。

経験豊富なデバッグ技術者が存在する場合は、自分カーネル デバッガーをフックでき、問題を分析できます。 このような状況が発生したときに確認する項目のヒントについては、[デバッグを停止しているシステム](debugging-a-stalled-system.md)を参照してください。

ただし、技術者が存在しない場合、カーネル モードのダンプ ファイルを作成し、オフサイトの技術者に送信することがあります。 このダンプ ファイルは、エラーの原因の分析に使用できます。

意図的にシステム クラッシュが発生する 2 つの方法はあります。

[デバッガーから強制的にシステムのクラッシュ](forcing-a-system-crash-from-the-debugger.md)

[キーボードから強制的にシステムのクラッシュ](forcing-a-system-crash-from-the-keyboard.md)

 

 





