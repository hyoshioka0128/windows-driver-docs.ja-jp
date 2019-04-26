---
title: カーネル同期遅延ファジー テスト
description: オプションをファジー化カーネル同期の遅延には、ドライバーで同時実行のバグを検出するためにスレッド スケジュールはランダム化します。
ms.assetid: B4BB3A75-C458-4718-8BE9-065CFC09E194
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bbbc061191211991fd68db65e2fa4f5da301109
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340454"
---
# <a name="kernel-synchronization-delay-fuzzing"></a>カーネル同期遅延ファジー テスト


オプションをファジー化カーネル同期の遅延には、ドライバーで同時実行のバグを検出するためにスレッド スケジュールはランダム化します。

**注意**  すべてを確認する場合に、このオプションは使用想定していません (または、多数の) コンピューター上のドライバーです。 個々 のドライバーまたは接続されているフィルター ドライバーの対象となるテストを実行する場合にのみ、このオプションを使用する必要があります。 予測の結果になると同時に多数のドライバーでは、このオプションを使用してとをテストするドライバーに関係のないコンポーネントでの force クラッシュの可能性があります。

 

**注**  このオプションは、Windows 8.1 以降から使用できます。

 

オプションを選択すると、Driver Verifier は、さまざまなポイントのスレッドでランダムな遅延を挿入します。 ように、 [Power Framework 遅延ファジー テスト](concurrency-stress-test.md)オプション、オプションの使用をファジー化カーネル同期の遅延のヘルプを提供するアルゴリズム向上のドライバーでエラーの検出可能性があります。 カーネル同期遅延ファジー テストを向上させる従来のストレス テスト、テスト プログラムが実行されるの数日間あるいは数週間をキャッチしようで同時実行で問題が発生します。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。


カーネル同期遅延がドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して 1 つまたは複数のドライバーの機能をファジー化を有効にすることができます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。 Power Framework 遅延ファジー テスト オプションをアクティブ化またはコンピューターを再起動する必要があります。

**注**  カーネル同期の遅延ファジー オプションには、さまざまなカーネル API 関数呼び出しでランダムな遅延を挿入することで、実行時に表示される競合状態の確率が高くなります。 これら遅延をより有効にするには、その他のドライバーの検証オプションでは、このオプションを有効にすることができます。 導入できる遅延のためには、コンピューターが、応答が遅くできるが期待できます。

 

-   **コマンドラインで**

    コマンドラインで、カーネル同期遅延ファジー テストで表される**verifier/flags 0x00800000** (ビット 23)。 Power Framework 遅延ファジー テストをアクティブ化するには、0x00800000 のフラグの値を使用するか、フラグの値に 0x00800000 を追加します。 例:

    ```
    verifier /flags 0x00800000 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック)**カーネル同期遅延ファジー テスト**します。
    5.  コンピューターを再起動します。

## <a name="span-idwhykernelsynchronizationdelayfuzzingspanspan-idwhykernelsynchronizationdelayfuzzingspanspan-idwhykernelsynchronizationdelayfuzzingspanwhy-kernel-synchronization-delay-fuzzing"></a><span id="Why_Kernel_synchronization_delay_fuzzing_"></span><span id="why_kernel_synchronization_delay_fuzzing_"></span><span id="WHY_KERNEL_SYNCHRONIZATION_DELAY_FUZZING_"></span>なぜカーネル同期遅延ファジー テストでしょうか。


ドライバー ルーチンのほとんどは、再入可能および同時実行されます。 同時実行に関連するバグが非常に困難を検索します。 デッドロックや競合状態、同期の問題とスレッド間でタイミングの問題が原因で、バグを含めることができます。 ストレス テストは、これらのバグを検索するための従来のテスト手法と、低速であり、高価であることができますが、結果は常に再現できません。 オプションをファジー化カーネル同期の遅延には、さまざまなカーネル API 関数呼び出しでランダムな遅延を挿入することで、実行時に表示される競合状態の確率が高くなります。 たとえば、IRP へのアクセスが取り消されました後、ドライバーの場合、競合状態、オプションのファジング カーネル同期の遅延には、Driver Verifier テスト中にエラーが検出するようにこの競合状態の機会が増えます。 オプションをファジー化カーネル同期の遅延には、電源と Driver Verifier の有効性が向上します。

 

 





