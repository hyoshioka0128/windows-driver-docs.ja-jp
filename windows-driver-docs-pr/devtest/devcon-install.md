---
title: DevCon Install
description: プラグ アンド プレイ デバイスの新しい、ルート列挙 devnode を作成し、そのサポート対象のソフトウェアをインストールします。 ローカル コンピューターでのみ有効です。
ms.assetid: d31007dd-6f20-460d-8561-d1639c69aa09
keywords:
- DevCon インストール ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Install
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 122eab295ea09855ca4c49d77fc1fa899de59adf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347045"
---
# <a name="devcon-install"></a>DevCon Install


プラグ アンド プレイ デバイスの新しい、ルート列挙 devnode を作成し、そのサポート対象のソフトウェアをインストールします。 ローカル コンピューターでのみ有効です。

```
    devcon [/r] install INFfile HardwareID 
```

## <a name="span-idddkdevconinstalltoolsspanspan-idddkdevconinstalltoolsspanparameters"></a><span id="ddk_devcon_install_tools"></span><span id="DDK_DEVCON_INSTALL_TOOLS"></span>パラメーター


<span id="________r______"></span><span id="________R______"></span> **/r**   
条件付き再起動します。 再起動が、変更を有効にする必要な場合は、操作を完了した後、システムを再起動します。 既定では、DevCon では、システムは再起動されません。

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span> *INFfile*   
デバイスの INF ファイルの完全なパスとファイル名を指定します。 パスを省略した場合、DevCon ファイルが現在のディレクトリがある前提としています。

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span> *HardwareID*   
デバイスのハードウェア ID を指定します。

指定されたハードウェア ID では、デバイスのハードウェア ID を完全に一致する必要があります。 パターンが有効ではありません。 単一引用符文字を入力しないでください (**'**) をリテラル値を示します。 詳細については、次を参照してください。[ハードウェア Id](https://msdn.microsoft.com/library/windows/hardware/ff546152)と[識別文字列](https://msdn.microsoft.com/library/windows/hardware/ff541224)します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

システムは、この変更を有効にするを再起動する必要があります。 DevCon システムを再起動するのには、再起動の条件付きパラメーターを追加します (**/r**) コマンド。

使用することはできません、 **DevCon インストール**プラグ アンド プレイ デバイスを操作します。

**DevCon インストール**操作は、プラグ アンド プレイ デバイスの新しいノードを作成します。 次を使用して、 [ **DevCon 更新**](devcon-update.md)を新しく追加されたデバイスのドライバーをインストールする操作。 その結果、メッセージ、成功、 **DevCon インストール**操作は、DevCon のデバイス ノードが作成されていると、デバイスのドライバーを更新したことを報告します。

場合のいずれかの手順、 **DevCon インストール**DevCon 操作が失敗エラー メッセージが表示され、ドライバーのインストールは続行されません。

**DevCon インストール**コマンドが実行するたびに新しいプラグ アンド プレイ デバイス ノードを作成します。 更新またはドライバーを再インストール、使用、 [ **DevCon 更新**](devcon-update.md)コマンド。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon install c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r install c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[33 の使用例:デバイスをインストールします。](devcon-examples.md#ddk_example_33_install_a_device_tools)

[34 の使用例:無人セットアップを使用してデバイスをインストールします。](devcon-examples.md#ddk_example_34_install_a_device_using_unattended_setup_tools)

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ハードウェア Id](https://msdn.microsoft.com/library/windows/hardware/ff546152)

[デバイスの識別文字列](https://msdn.microsoft.com/library/windows/hardware/ff541224)










