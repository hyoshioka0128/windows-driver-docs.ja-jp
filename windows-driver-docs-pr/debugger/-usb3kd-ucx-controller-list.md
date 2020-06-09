---
title: ucx_controller_list usb3kd
description: Usb3kd コマンドは、コンピューター上のすべての USB 3.0 ホストコントローラーに関する情報を表示します ucx_controller_list。 表示は、UcxVersion. sys によって管理されるデータ構造に基づいています。
ms.assetid: 57565A2A-A409-46CE-B7F9-F1CD521960E5
keywords:
- usb3kd Windows デバッグの ucx_controller_list
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_controller_list
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 213f659f34a08f66eaca27e4bc1f25da1ae164c3
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534171"
---
# <a name="usb3kducx_controller_list"></a>! usb3kd \_ コントローラーの \_ 一覧


[**! Usb3kd \_ controller \_ list**](-usb3kd-device-info.md)コマンドは、コンピューター上のすべての USB 3.0 ホストコントローラーに関する情報を表示します。 この表示は、USB ホストコントローラー拡張機能ドライバー (Ucx*バージョン*.sys) によって管理されるデータ構造に基づいています。

```dbgcmd
!usb3kd.ucx_controller_list
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


次のスクリーンショットは、 [**! ucx \_ コントローラー \_ リスト**](-usb3kd-device-info.md)コマンドの出力を示しています。

![\- \- ucx コントローラーデバイスとエンドポイントを示す! ucx コントローラーリストコマンドの出力](images/ucxcontrollerlist01.png)

出力には、USB 3.0 ホストコントローラーが1つあることが示されています。これは、 [**! ucx \_ コントローラー**](-usb3kd-ucx-controller.md)で始まる行で表されます。 2つのデバイスがコントローラーに接続されており、各デバイスには4つのエンドポイントがあることがわかります。

出力では、[デバッガーマークアップ言語 (DML) を使用して](debugger-markup-language-commands.md)リンクを提供します。 これらのリンクは、個々のデバイスまたはエンドポイントに関する詳細情報を提供するコマンドを実行します。 たとえば、 [**! ucx \_ エンドポイント**](-usb3kd-ucx-endpoint.md)リンクのいずれかをクリックすると、エンドポイントに関する詳細情報を取得できます。 リンクをクリックする代わりに、コマンドを入力することもできます。 たとえば、2番目のデバイスの最初のエンドポイントに関する情報を表示するには、次のコマンドを入力します。 **ucx \_ エンドポイント 0xfffffa8003694860**。

**メモ**   DML 機能は、WinDbg では使用できますが、Visual Studio または KD では使用できません。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

[**! Ucx \_ controller \_ list**](-usb3kd-device-info.md)コマンドは、この一連のコマンドの親コマンドです。

-   [**! ucx \_ コントローラー**](-usb3kd-ucx-controller.md)
-   [**! ucx \_ デバイス**](-usb3kd-ucx-device.md)
-   [**! ucx \_ エンドポイント**](-usb3kd-ucx-endpoint.md)

Usb ホストコントローラー拡張機能ドライバー (Ucx*バージョン*.sys) は、usb 3.0 ハブドライバーと usb 3.0 ホストコントローラードライバーの間に抽象層を提供します。 拡張機能ドライバーは、ホストコントローラー、デバイス、およびエンドポイントを独自に表現したものです。 [**! Ucx \_ コントローラー \_ リスト**](-usb3kd-device-info.md)ファミリのコマンドの出力は、拡張機能ドライバーによって管理されるデータ構造に基づいています。 Usb ホストコントローラー拡張機能ドライバーおよび USB 3.0 ホストコントローラードライバーの詳細については、「 [Usb ドライバースタックアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。 USB 3.0 スタックのドライバーで使用されるデータ構造の詳細については、Windows 8 ビデオの[Usb デバッグイノベーション](https://channel9.msdn.com/Events/BUILD/BUILD2011/HW-258P)のパート2を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






