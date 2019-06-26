---
title: VM スイッチ検証
description: VM のスイッチの確認オプションは、HYPER-V 拡張可能スイッチ内で実行されるフィルター ドライバー (拡張可能スイッチの拡張機能) を監視します。 または、送信で発生し、拡張可能スイッチ内の操作を受信するエラーをキャッチするのにには、このオプションを使用します。
ms.assetid: 629C0C70-D6C6-4977-A36B-6BD6EEC14FE8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc4e109ef2cc85619259c4ff02f0c7073a45e4c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381785"
---
# <a name="vm-switch-verification"></a>VM スイッチ検証


VM のスイッチの確認オプションは、フィルター ドライバーを監視します。 (*拡張可能スイッチの拡張機能*) 内で実行される、 [Hyper-v 拡張可能スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch)します。 または、送信で発生し、拡張可能スイッチ内の操作を受信するエラーをキャッチするのにには、このオプションを使用します。

**注**  このオプションは、Windows 8.1 以降から使用できます。

 

Driver Verifier を発行するときに、このオプションがアクティブで[**バグ チェック 0xC4** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (ドライバー\_VERIFIER\_検出\_違反) 場合、拡張可能スイッチの拡張機能HYPER-V 拡張可能スイッチ ハンドラー関数を正しく呼び出すには失敗します。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。


ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して VM スイッチの検証機能の 1 つまたは複数のドライバーをアクティブ化することができます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。 Power Framework 遅延ファジー テスト オプションをアクティブ化またはコンピューターを再起動する必要があります。

-   **コマンドラインで**

    によって表される VM スイッチの確認、コマンドラインで**verifier/flags 0x01000000** (ビット 24)。 Power Framework 遅延ファジー テストをアクティブ化するには、0x01000000 のフラグの値を使用するか、フラグの値に 0x01000000 を追加します。 次に、例を示します。

    ```
    verifier /flags 0x01000000  /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック) **VM switch 検証**です。
    5.  コンピューターを再起動します。

 

 





