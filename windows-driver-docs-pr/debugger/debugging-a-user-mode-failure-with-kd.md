---
title: KD を使用したユーザーモード エラーのデバッグ
description: KD を使用したユーザーモード エラーのデバッグ
ms.assetid: c7ef3c04-45bf-4e7b-bcc6-35fe2ffa43d1
keywords:
- KD、ユーザー モードの KD を使用したデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 541c91a37fc69e98be83c93c20fb7c424e400f59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324589"
---
# <a name="debugging-a-user-mode-failure-with-kd"></a>KD を使用したユーザーモード エラーのデバッグ


## <span id="ddk_debugging_user_mode_failures_with_kd_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_FAILURES_WITH_KD_DBG"></span>


ユーザー モードの失敗を正しくデバッグするには、CDB または WinDbg する必要があります。 ただし、場合がありますユーザー モード例外は分割 KD ユーザー モードのデバッガーが存在しないためです。 特定のユーザー モード プロセスの実行内容を監視すると便利な場合も、カーネル モードの問題のデバッグ中にします。

既定では、指定したアドレスに一致する最初のユーザー モード シンボルを読み込もうとカーネル デバッガー (用、 **k**、 **u**、または**ln**コマンド)。

残念ながら、シンボル パスでは、ユーザー モードのシンボルは指定されていない多くの場合、または最初のシンボルはしいものではありません。 シンボル パスまたは使用にコピーするか、シンボルが登録されていない場合、 [ **.sympath (シンボル パスの設定)** ](-sympath--set-symbol-path-.md)完全なシンボルのツリーで、] をポイントし、使用するコマンド、 [ **.reload(モジュールの再読み込み)** ](-reload--reload-module-.md)コマンド。 これでシンボルを明示的に読み込む、正しくないシンボルが読み込まれている場合、 **.reload &lt;binary.ext&gt;** します。

Windows Dll のほとんどが再配置されるため、別のアドレスに読み込まれるが、例外があります。 ビデオ アダプターは、最も一般的な例外です。 多数の同じベース アドレスは KD は、ほぼ常にすべての負荷が ati.dll (最初のビデオ シンボル アルファベット順) を検索するビデオ アダプターがあります。 ビデオの場合もファイルがある .sys ロードを使用して識別できる、 [ **! ドライバー** ](-drivers.md)拡張機能。 その情報を発行することができます、 **.reload**正しいビデオ Dll を取得します。 ときに、デバッガーに混乱して取得および適切なスタックを提供するヘルプは特定のシンボルを再読み込み時間もあります。 シンボルが正しいかかどうかを確認する関数を逆アセンブルします。

ビデオの Dll と同様に、ほぼすべての実行可能ファイルを読み込む同じアドレスでように KD へのアクセスが報告されます。 アクセスでスタック トレースを表示する場合は、 [ **! プロセス**](-process.md)をクリックし、 **.reload**の指定された実行可能ファイルの名前。 実行可能ファイル、シンボルをシンボル パスではありませんの場合がありますコピーし、実行、 **.reload**もう一度です。

場合によって KD または WinDbg は、完全なシンボルのツリーをシンボル パスが場合でも、適切なユーザー モードのシンボルの読み込みに問題を持っています。 この場合、ntdll.dll と kernel32.dll を 2 つの最も一般的な記号が必要になります。 KD から CSRSS をデバッグするには、場合 winsrv.dll と csrsrv.dll も一般的な Dll を読み込めません。

 

 





