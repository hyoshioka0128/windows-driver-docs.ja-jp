---
title: ミラー ドライバーのインストール
description: ミラー ドライバーのインストール
ms.assetid: 13b0ce22-f833-482c-815b-a596098ee6bc
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、ミラー ドライバー
- ミラー ドライバー WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed4b2b1df3a82f7bf2f5bab0061159ca5d32f0a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385593"
---
# <a name="mirror-driver-installation"></a>ミラー ドライバーのインストール


## <span id="ddk_mirror_driver_installation_gg"></span><span id="DDK_MIRROR_DRIVER_INSTALLATION_GG"></span>


システムでは、ミラー ドライバーをインストール、Win32 への応答で**ChangeDisplaySettings**または**ChangeDisplaySettingsEx**呼び出します。 これらの呼び出しには、ミラー ドライバーをインストールおよびその設定を管理するを行うユーザー モード サービスを実装する必要があります。 このアプリケーションを使用します。

-   ミラー ドライバーがブート時に正しく読み込まれたことを確認します。 アプリケーションは、CD を指定する必要があります\_それ以降の起動と同じでは、ドライバーが自動的に読み込まれるように、レジストリ設定を保存する updateregistry にフラグ[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)について以下で説明します。

-   デスクトップの変更は表示を取得することによって、WM 経由で通知を変更するには適切に応答\_DISPLAYCHANGE メッセージ。

サンプル*Mirror.exe*付属の Windows Driver Kit (WDK) でのファイル、ソース コードからビルドすることができる実装にミラー ドライバーの読み込み操作ユーザー モード サービスのサブセットを提供する必要があります。

ユーザー モード アプリケーションを入力する必要があります、ミラー ドライバーをインストールすると、前に、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造を次の表示属性を指定します。

-   位置 (**dmPosition**)

-   サイズ (**dmPelsWidth**と**調べます**)

-   ミラー化された表示形式 (**dmBitsPerPel**)

ユーザー モード アプリケーションを設定する必要がありますも**dmFields**変更するには、この構造体メンバーのそれぞれに使用するフラグを含めることによって、適切にします。 デスクトップ座標でミラー化された表示の位置座標を指定する必要があります。そのため、1 つ以上のデバイスに分散していることができます。 プライマリ ディスプレイを直接反映するには、ミラー ドライバーはプライマリ ディスプレイのデスクトップ座標と一致するには、その場所を指定する必要があります。

DEVMODEW 構造体のメンバーが設定された後は、Win32 への呼び出しでこの構造体を渡すことによってミラー化された表示設定を変更**ChangeDisplaySettingsEx**関数。

ミラー ドライバーがインストールされた後は呼び出すことが GDI でドライバーの表示領域と交差するすべてのレンダリング操作。 ミラー ドライバーでは、マルチ モニター システムでプライマリ ディスプレイのみが重なっている場合、GDI が、ミラー ドライバーをすべての描画操作を送信しません。

に関する詳細については、Microsoft Windows SDK ドキュメントを参照してください、 **ChangeDisplaySettings**と**ChangeDisplaySettingsEx**関数、および変更デスクトップの通知を表示します。

**注**  以降 Windows 8 では、ミラー ドライバーがインストールされないシステムにします。 詳細については、次を参照してください。[ミラー ドライバー](mirror-drivers.md)します。

 

 

 





