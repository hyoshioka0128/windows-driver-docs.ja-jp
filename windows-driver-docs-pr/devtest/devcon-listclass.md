---
title: DevCon ListClass
description: 指定されたデバイス セットアップ クラスのすべてのデバイスの一覧を表示します。 ローカルおよびリモート コンピューターで有効です。
ms.assetid: b642ca5e-5ef1-499f-b8c5-96583a4bd411
keywords:
- DevCon ListClass ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon ListClass
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f1e54a08ff250f896e401ac5b0f9743ac618e19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551349"
---
# <a name="devcon-listclass"></a>DevCon ListClass


指定されたデバイス セットアップ クラスのすべてのデバイスの一覧を表示します。 ローカルおよびリモート コンピューターで有効です。

```
    devcon [/m:\\computer] listclass class [class...] 
```

## <a name="span-idddkdevconlistclasstoolsspanspan-idddkdevconlistclasstoolsspanparameters"></a><span id="ddk_devcon_listclass_tools"></span><span id="DDK_DEVCON_LISTCLASS_TOOLS"></span>パラメーター


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\**<em>コンピューター</em>   
指定したリモート コンピューター上のコマンドを実行します。 円記号が必要です。

**注**DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista および Windows 7 を実行するコンピューター、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 WDK 8 WDK 8.1 を実行するコンピューターでリモート アクセスでは使用できません。



<span id="_______class______"></span><span id="_______CLASS______"></span> *class*   
デバイス セットアップ クラスを指定します。 等号 (=) は必要ありません。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/M**パラメーターは、操作名を付ける必要があります (**listclass**)。 それ以外の場合、DevCon は無視されます、 **/m**パラメーター、構文エラーを返さずに、ローカル コンピューター上のデバイスが表示されます。

セットアップ クラスの表示の各エントリは、1 つのデバイスを表します。 一意のインスタンス名と、デバイスの説明のエントリで構成されます*インスタンス* **:** *説明*形式。

特定のデバイスのセットアップ クラスを検索するには、使用、 [ **DevCon スタック**](devcon-stack.md)操作。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon listclass printers ports
devcon /m:\\Server01 listclass SmartCardReader
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 6:デバイス セットアップ クラスでデバイスを一覧表示します。](devcon-examples.md#ddk_example_6_list_the_devices_in_a_device_setup_class_tools)

[例 7:リモート コンピューター上の複数のクラス内のデバイスを一覧表示します。](devcon-examples.md#ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute)









