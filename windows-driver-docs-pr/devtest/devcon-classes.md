---
title: DevCon Classes
description: システム上のデバイスを使用しないクラスを含む、すべてのデバイス セットアップ クラスを一覧表示します。 ローカルおよびリモート コンピューターで有効です。
ms.assetid: 05b9339c-30d1-45df-8f43-20a07e520a42
keywords:
- DevCon クラス ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Classes
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 147a0e029dadaa26f7d8438845ccf5cc2089a62c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371528"
---
# <a name="devcon-classes"></a>DevCon Classes


すべてを一覧表示[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)システム上のデバイスを使用しないクラスを含むです。 ローカルおよびリモート コンピューターで有効です。

```
    devcon [/m:\\computer] classes 
```

## <a name="span-idddkdevconclassestoolsspanspan-idddkdevconclassestoolsspanparameters"></a><span id="ddk_devcon_classes_tools"></span><span id="DDK_DEVCON_CLASSES_TOOLS"></span>パラメーター


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\コンピューター**   
指定したリモート コンピューター上のコマンドを実行します。 円記号が必要です。

**注**DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista および Windows 7 を実行するコンピューター、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 WDK 8 WDK 8.1 を実行するコンピューターでリモート アクセスでは使用できません。



### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/M**パラメーターは、操作名を付ける必要があります (**クラス**)。 それ以外の場合、DevCon は無視されます、 **/m**パラメーター、構文エラーを返さずに、ローカル コンピューター上のクラスが表示されます。

DevCon ディスプレイ クラスは、レジストリ (GUID でアルファベット順) に出現する順序で一覧表示されます。

セットアップ クラスのデバイスを見つけ、使用、 [ **DevCon ListClass** ](devcon-listclass.md)操作。 特定のデバイスのセットアップ クラスを検索するには、使用、 [ **DevCon スタック**](devcon-stack.md)操作。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon classes
devcon classes > setupclasses.txt
devcon /m:\\Server01 classes
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 4:ローカル コンピューターのリスト クラス](devcon-examples.md#ddk_example_4_list_classes_on_the_local_computer_tools)

[例 5:リモート コンピューター上のリスト クラス](devcon-examples.md#ddk_example_5_list_classes_on_the_remote_computer_tools)









