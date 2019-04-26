---
title: 検証ツールの調査
description: 検証ツールの調査
ms.assetid: d36e041f-efa5-450f-b4de-c84c4880e44d
keywords:
- WDK の動的検証ツール
- WDK の静的検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feeee25ed8dd8687a68f75c730e6e86a27a3542a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347604"
---
# <a name="survey-of-verification-tools"></a>検証ツールの調査


次の検証ツールは、WDK で説明されているし、ドライバー開発者およびテスト担当者による使用は推奨します。 これらは、その通常使用する順序に表示されます。

### <a name="span-idassoonasthecodecompilesspanspan-idassoonasthecodecompilesspanas-soon-as-the-code-compiles"></a><span id="as_soon_as_the_code_compiles"></span><span id="AS_SOON_AS_THE_CODE_COMPILES"></span>コードをコンパイルするようになります

-   [Code Analysis for Drivers](code-analysis-for-drivers.md)はコンパイル時に実行する静的検証ツールです。 Windows Driver Kit にドライバー固有の拡張機能を提供する、[コード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)Microsoft Visual Studio Ultimate 2012。

    [Code Analysis for Drivers](code-analysis-for-drivers.md) C/C++ で記述され、管理されているドライバーを確認できますコード。 調査いないドライバーの各関数のコード、独立して、ドライバーをビルドすると、すぐに実行できるようにします。 比較的短時間で実行し、いくつかのリソースを使用します。

    基本的な機能、[コード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)戻り値をオンにしないなどの一般的なコーディング エラーを検出します。 ドライバー固有の機能は、コーディング エラーのコピーの IRP で初期化されていないフィールドをルーチンの終わりまでに変更された IRQL が復元に失敗するより微妙なドライバーを検出します。

<!-- -->

-   [Static Driver Verifier](static-driver-verifier.md) (SDV) はコンパイル時に実行され、C と C++ で記述されたカーネル モード ドライバーのコードを確認する静的検証ツールです。 WDK に含まれているし、Visual Studio Ultimate 2012 から、または MSBuild を使用して、Visual Studio コマンド プロンプト ウィンドウから開始できます。

    一連のインターフェイスの規則とオペレーティング システムのモデルに基づいて、Static Driver Verifier は、Windows オペレーティング システムのカーネルのドライバーが正しく対話するかどうかを決定します。 Static Driver Verifier は非常に詳細な--ドライバーのソース コード内のすべての到達可能なパスをについて説明し、シンボリックに実行します。 そのため、ドライバーのテストの他の従来のメソッドを使用して検出されないバグを検索します。

### <a name="span-idwhenthedriverrunsspanspan-idwhenthedriverrunsspanwhen-the-driver-runs"></a><span id="when_the_driver_runs"></span><span id="WHEN_THE_DRIVER_RUNS"></span>ドライバーを実行すると

ドライバーは組み込まれており、明らかなエラーなしで実行するいるとすぐには、次の動的検証ツールを使用します。

-   [チェック済みの Windows ビルド](checked-build-of-windows.md)します。 検証ツールでは技術的には、Windows のチェック ビルドでは、ドライバーを実行する際に役立つ他のツールとテストではないエラーを検出します。 ドライバーの開発とテストでは、カーネル デバッガーと共にチェック ビルドを使った実行を標準の手法として含める必要があります。

-   [Driver Verifier](driver-verifier.md)は特に Windows ドライバー用に記述された、動的検証ツールです。 これには、いくつかのドライバーで同時に実行できる複数のテストが含まれます。 Driver Verifier は非常に効率的でドライバー開発者が発生したドライバーで重大なバグを見つけ出すためにし、テスト担当者は、ドライバーは、開発またはテスト環境で実行されるたびに実行する Driver Verifier を構成します。 Driver Verifier は、Windows 2000 および以降のバージョンの Windows に含まれます。 ドライバーのドライバーの検証を有効にすると、ドライバーでも複数のテストを実行する必要があります。 Driver Verifier は、単独での静的検証ツールを使用して検出しにくい特定のドライバーのバグを検出できます。 これらの種類のバグの例については、次のとおりです。
    -   **カーネル プールのバッファー オーバーランです。** 検証済みのドライバーは、メモリ バッファーをプールに割り当て、Driver Verifier はそれらにアクセス可能なメモリのページに保護します。 ドライバーが、バッファーの末尾のメモリを使用しようとすると、ドライバーの検証ツールにバグ チェックが発行されます。
    -   **メモリを使用して、それを解放した後。** 特別なプールのメモリ ブロックは、独自のメモリ ページを使用してし、他の割り当てメモリ ページを共有しないでください。 ドライバーはプールのメモリ ブロックを解放して、すると、対応するメモリ ページからアクセス可能なようになります。 ドライバーがそれを解放した後、そのメモリを使用しようとすると、すぐに、ドライバーがクラッシュします。
    -   **管理者特権での IRQL での実行中にページング可能なメモリを使用します。** 検証済みのドライバーがディスパッチで IRQL を発生させる\_レベル、または以降では、Driver Verifier トリム、システムのワーキング セットからすべてのページング可能なメモリをシステム メモリ負荷をシミュレートします。 ページング可能な仮想アドレスのいずれかを使用すると、ドライバーがクラッシュします。
    -   **低リソース シミュレーション。** リソース不足の条件下でシステムをシミュレートするには、Driver Verifier はドライバーによって Api が呼び出されるさまざまなオペレーティング システムのカーネルにフェールバックできます。
    -   **メモリ リークが発生します。** Driver Verifier は、ドライバーによって行われるメモリ割り当てを追跡し、アンロードされたドライバーを取得する前に、メモリが解放されるようにします。
    -   **I/O 操作を完了するか取り消される時間がかかりすぎています。** Driver Verifier の状態に対応するため、ドライバーのロジックをテストできます\_PENDING から値を返す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。
    -   **DDI 準拠の確認。** (Windows 8 以降で使用可能)Driver Verifier には、一連のドライバーとオペレーティング システムのカーネル インターフェイスの適切な相互作用をチェックするデバイス ドライバー インターフェイス (DDI) ルールが適用されます。 これらの規則は、Static Driver Verifier は、ドライバーのソース コードの分析に使用されるルールに対応します。 Driver Verifier には、DDI 準拠の検査が有効になっているときにエラーが検出されると、実行[Static Driver Verifier](static-driver-verifier.md)エラーの原因となった同じ規則を選択します。 Static Driver Verifier は、ドライバーのソース コードの不具合の原因を見つけるのに役立ちます。
-   [Application Verifier](application-verifier.md)はユーザー モード アプリケーションと C と C++ で記述されたドライバーの動的検証ツールです。 マネージ コードは検証されません。 Application Verifier は、WDK に含まれていませんが、ダウンロードしてインストールしてから、 [Microsoft ダウンロード センター web サイト](https://go.microsoft.com/fwlink/p/?linkid=11573)します。

 

 





