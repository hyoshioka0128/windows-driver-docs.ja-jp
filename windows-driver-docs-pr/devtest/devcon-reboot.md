---
title: DevCon Reboot
description: 停止し、オペレーティング システムを起動します。 ローカル コンピューターでのみ有効です。
ms.assetid: 4e27c35c-8b98-4edc-98d7-8ba0f96d7a78
keywords:
- DevCon 再起動ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Reboot
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92af29ce5dd13cb84d8eaff0ce5286ff1694d2da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347034"
---
# <a name="devcon-reboot"></a>DevCon Reboot


停止し、オペレーティング システムを起動します。 ローカル コンピューターでのみ有効です。

```
    devcon reboot 
```

## <span id="ddk_devcon_reboot_tools"></span><span id="DDK_DEVCON_REBOOT_TOOLS"></span>


### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

異なり、 **/r**パラメーターで、システムを再起動して変更を有効にするために必要な場合にのみ、 **DevCon 再起動**操作は、再起動が必要かどうかを決定することがなく、システムを再起動します。

DevCon 標準を使用して**ExitWindowsEx**を再起動する関数。 ユーザーがコンピューター上の開いているファイルまたはプログラムが閉じられません、システムが、ユーザーがファイルを閉じるかプロセスを終了するシステムのプロンプトに応答するまで再起動しません。 詳細については**ExitWindowsEx**、Microsoft Windows SDK を参照してください。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon reboot
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

[39 の使用例:ローカル コンピューターを再起動します。](devcon-examples.md#ddk_example_39_reboot_the_local_computer_tools)









