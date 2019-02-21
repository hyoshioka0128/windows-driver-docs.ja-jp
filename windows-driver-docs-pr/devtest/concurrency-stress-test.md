---
title: Power Framework 遅延ファジー テスト
description: Power Framework 遅延ファジー テスト オプションは、電源管理フレームワーク (PoFx) を使用するドライバーの同時実行のバグを検出するためにスレッド スケジュールをランダム化します。
ms.assetid: A33DEA5B-4758-456A-B4CF-F036CB511A1F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3268173a4500e1111aa08ed4027f5190add8fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560591"
---
# <a name="power-framework-delay-fuzzing"></a>Power Framework 遅延ファジー テスト


Power Framework 遅延ファジー テスト オプションを使用するドライバーの同時実行のバグを検出するためにスレッド スケジュールをランダムに、[電源管理フレームワーク (PoFx)](https://msdn.microsoft.com/library/windows/hardware/hh406637)します。 このオプションは、電源管理フレームワーク (PoFx) を直接利用しないドライバーを使用しないでください。

**注**  このオプションは Windows 8 以降で使用できます。

 

オプションを選択すると、Driver Verifier は、さまざまなポイントのスレッドでランダムな遅延を挿入します。 Power Framework 遅延ファジー テスト オプションは、ドライバーでエラーの検出確率論的保証を提供するアルゴリズムを使用します。 Power Framework 遅延ファジー テストを向上させる従来のストレス テスト、テスト プログラムが実行されるの数日間あるいは数週間をキャッチしようで同時実行で問題が発生します。

ドライバー ルーチンのほとんどは、再入可能および同時実行されます。 同時実行のバグは非常に困難を検索します。 デッドロックや競合状態、同期の問題とスレッド間でタイミングの問題が原因で、バグを含めることができます。 ストレス テストは、従来のテスト手法と、低速であり、高価であることができますが、結果は常に再現できません。 Power Framework 遅延ファジー テスト オプションには、さまざまな電源 API 関数呼び出しでランダムな遅延を挿入することで、実行時に表示される競合状態の確率が高くなります。 たとえば、IRP へのアクセスが取り消されました後、ドライバーの場合、競合状態、Power Framework 遅延ファジー テスト オプションには、Driver Verifier テスト中にエラーが検出するようにこの競合状態の機会が増えます。 Power Framework 遅延ファジー テスト オプションでは、電源とドライバーの検証ツールの有用性を拡張します。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。


ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバー用に Power Framework 遅延ファジー テスト機能をアクティブ化できます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。 Power Framework 遅延ファジー テスト オプションをアクティブ化またはコンピューターを再起動する必要があります。

**注**  The Power Framework 遅延ファジー テスト オプションには、さまざまな電源 API 関数呼び出しでランダムな遅延を挿入することで、実行時に表示される競合状態の確率が高くなります。 これら遅延をより有効にするには、その他のドライバーの検証オプションでは、このオプションを有効にすることができます。 導入できる遅延のためには、コンピューターが、応答が遅くできるが期待できます。

 

-   **コマンドラインで**

    コマンドラインで、Power Framework 遅延ファジー テストで表される**verifier/flags 0x00008000 (ビット 15)** します。 Power Framework 遅延ファジー テストをアクティブ化するには、0x00008000 のフラグの値を使用するか、フラグの値に 0x00008000 を追加します。 次に、例を示します。

    ```
    verifier /flags 0x00008000 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック) Power Framework 遅延ファジー テストします。
    5.  コンピューターを再起動します。

 

 





