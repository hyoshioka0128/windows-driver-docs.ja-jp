---
title: usb3kd.ucx_controller_list
description: Usb3kd.ucx_controller_list コマンドでは、コンピューターのすべての USB 3.0 ホスト コント ローラーに関する情報が表示されます。 表示は、UcxVersion.sys によって管理されるデータ構造に基づいています。
ms.assetid: 57565A2A-A409-46CE-B7F9-F1CD521960E5
keywords:
- デバッグ usb3kd.ucx_controller_list Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_controller_list
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 40beff4b1785125f3cf95ca80639b8b7bd2ea60e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560582"
---
# <a name="usb3kducxcontrollerlist"></a>!usb3kd.ucx\_controller\_list


[ **! Usb3kd.ucx\_コント ローラー\_一覧**](-usb3kd-device-info.md)コマンドは、コンピューターのすべての USB 3.0 ホスト コント ローラーに関する情報を表示します。 USB ホスト コント ローラーの拡張機能ドライバーによって管理されるデータ構造に基づいて表示 (Ucx*バージョン*.sys)。

```dbgcmd
!usb3kd.ucx_controller_list
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


次のスクリーン ショットの出力を表示する、 [ **! ucx\_コント ローラー\_一覧**](-usb3kd-device-info.md)コマンド。

![出力、! ucx\-コント ローラー\-コマンドが表示された ucx コント ローラー デバイスとエンドポイントを一覧表示](images/ucxcontrollerlist01.png)

出力で始まる行で表される 1 つの USB 3.0 ホスト コントがあることを示しています。 [ **! ucx\_コント ローラー**](-usb3kd-ucx-controller.md)します。 コント ローラーに、2 つのデバイスが接続されていることと、各デバイスが 4 つのエンドポイントを持つことを確認できます。

出力を使用して[を使用してデバッガー マークアップ言語 (DML)](debugger-markup-language-commands.md)リンクを提供します。 リンクは、個々 のデバイスまたはエンドポイントに関する詳細な情報を提供するコマンドを実行します。 たとえばのいずれかをクリックしてエンドポイントに関する詳細な情報を取得できます、 [ **! ucx\_エンドポイント**](-usb3kd-ucx-endpoint.md)リンク。 リンクをクリックする代わりに、コマンドを入力することができます。 たとえば、2 つ目のデバイスの最初のエンドポイントに関する情報を表示する可能性がありますコマンドを入力する **! ucx\_エンドポイント 0xfffffa8003694860**します。

**注**  DML の機能は、WinDbg がではなく Visual Studio または KD で使用できます。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

[ **! Ucx\_コント ローラー\_一覧**](-usb3kd-device-info.md)コマンドは、このコマンドのセットの親コマンド。

-   [**! ucx\_コント ローラー**](-usb3kd-ucx-controller.md)
-   [**! ucx\_デバイス**](-usb3kd-ucx-device.md)
-   [**! ucx\_エンドポイント**](-usb3kd-ucx-endpoint.md)

USB ホスト コント ローラーの拡張機能ドライバー (Ucx*バージョン*.sys) コント ローラーのドライバーの USB 3.0 ハブのドライバーと USB 3.0 ホスト間の抽象化レイヤーを提供します。 拡張機能ドライバーが、ホスト コント ローラー、デバイス、およびエンドポイントの独自の表現。 内のコマンドの出力、 [ **! ucx\_コント ローラー\_一覧**](-usb3kd-device-info.md)ファミリが拡張機能ドライバーによって管理されるデータ構造に基づきます。 USB ホスト コント ローラーの拡張機能ドライバーと USB 3.0 ホスト コント ローラーのドライバーの詳細については、[USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)を参照してください。 USB 3.0 スタック内のドライバーで使用されるデータ構造の詳細については、第 2 部を参照してください、 [Windows 8 の USB デバッグ イノベーション](https://go.microsoft.com/fwlink/p/?LinkID=249153)ビデオ。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






