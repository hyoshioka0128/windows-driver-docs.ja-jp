---
title: DevCon Rescan
description: コンピューターのデバイスの一覧を更新するのにには、Windows のプラグ アンド プレイの機能を使用します。 ローカルおよびリモート コンピューターで有効です。
ms.assetid: 08762f30-a276-4ef4-8936-dfb1e1f692ca
keywords:
- DevCon は、ドライバー開発ツールを再スキャンします。
topic_type:
- apiref
api_name:
- DevCon Rescan
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d43ef82d23d3efd96486873d83798cce1a4d8274
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347020"
---
# <a name="devcon-rescan"></a>DevCon Rescan


コンピューターのデバイスの一覧を更新するのにには、Windows のプラグ アンド プレイの機能を使用します。 ローカルおよびリモート コンピューターで有効です。

```
    devcon [/m:\\computer] [/r] rescan 
```

## <a name="span-idddkdevconrescantoolsspanspan-idddkdevconrescantoolsspanparameters"></a><span id="ddk_devcon_rescan_tools"></span><span id="DDK_DEVCON_RESCAN_TOOLS"></span>パラメーター


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\**<em>コンピューター</em>   
指定したリモート コンピューター上のコマンドを実行します。 円記号が必要です。

**注**DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista および Windows 7 を実行するコンピューター、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 WDK 8 WDK 8.1 を実行するコンピューターでリモート アクセスでは使用できません。



<span id="________r______"></span><span id="________R______"></span> **/r**   
条件付き再起動します。 再起動が必要な変更を有効にする場合にのみ操作を完了した後、システムを再起動します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/M**パラメーターは、操作名を付ける必要があります (**再スキャン**)。 それ以外の場合、DevCon は無視されます、 **/m**パラメーターと、構文エラーを返さずに、ローカル コンピューターをスキャンします。

再スキャンすると、プラグ アンド プレイ manager を新しいデバイスを検出し、警告なしにデバイス ドライバーをインストールすることがあります。

再スキャン特にパラレル ポートのデバイスとデバイスのシリアル ポートなど、インストールされると、システムに通知することはできませんが、一部のプラグ アンド プレイ デバイスを検出できます。 その結果を実行する管理者特権が必要**DevCon を再スキャン**コマンド。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon rescan
devcon /m:\\Server01 rescan
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

[37 の使用例:新しいデバイスには、コンピューターをスキャンします。](devcon-examples.md#ddk_example_37_scan_the_computer_for_new_devices_tools)









