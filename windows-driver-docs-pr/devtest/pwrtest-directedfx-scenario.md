---
title: PwrTest DirectedFx シナリオ
description: PwrTest Directed Power Framework シナリオは PoFx v3 機能をテストする設計されています。
ms.assetid: edf70fce-4c2a-4747-854f-feb919e01324
ms.date: 03/27/2019
ms.custom: 19H1
ms.openlocfilehash: 24716ed7cc721c67340843f37d1285ddae9b6a7b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345754"
---
# <a name="pwrtest-directedfx-scenario"></a>PwrTest DirectedFx シナリオ

PwrTest DirectedFx シナリオが使用するドライバーを使用してデバイスをテストするように設計、 [Directed 電源管理フレームワーク (DFx)](../kernel/introduction-to-the-directed-power-management-framework.md)します。

ユーザーは、テストするデバイスと、必要に応じてデバイスの電源状態を確認するのインスタンスのパスを提供します。

D 状態が指定されていない場合、テストは、デバイスの維持が D0 でしませんでしたを確認します。  インスタンスのパスを検索するには、デバイス マネージャーで、デバイスのプロパティを確認します。  または、システム上のすべての DFx 対応デバイスのインスタンス パスの一覧を取得するオプションなしで、テストを実行します。

このテストは、いずれかで実行できる[最新スタンバイ](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)スタンバイ状態または AC または DC 電源で実行されるかどうか、ネットワーク接続の設定に関係なくシステム。

指定したデバイスの場合、テストを確認します。

- デバイスと、親の前にする必要がありますの電源を任意の子デバイス DFx をサポートします。
- デバイスでは、少なくとも 1 つの有向電源ダウン/アップが正常に完了します。
- デバイスはダウン有向の電源を割り当てた D の適切な状態になります。 (オプション)

サイクルごとに、テストを示しています。

- システムがアイドル状態の回復性にしていた時間
- 時間の指示に従って[深いランタイム アイドル プラットフォームの状態 (DRIPS)](https://docs.microsoft.com/windows-hardware/design/device-experiences/prepare-hardware-for-modern-standby)作動されました
    - 個々 の動機ごとにアクティブだった時刻
- 個々 の統計情報と、省略可能なすべてのテスト デバイスの理由が失敗します。
    - `Device {Test Device} failed because device {Failed Device} {Failed Reason}` の順にクリックします。
        - ページング デバイスまたはデバッグ デバイスのいずれかには
        - DFx をサポートしていません
        - コンポーネントを制約します。
        - その DFx の電源の呼び出しに失敗しました
- 各ブロードキャストのツリーと参加要素のすべてのデバイス

デバイスに複数の有向 power 遷移を実行できることを確認する、3 つのサイクルのテストを実行することをお勧めします。  すべてのサイクルが完了したら、テスト サイクルの成功/失敗の合計数を出力します。

テストを返すかどうか、システム上のデバイスの DFx サポートなし、`Error retrieving list of available Directed Fx devices`します。

## <a name="syntax"></a>構文

```
pwrtest /directedfx [/c:n] [/d:n] [/p:n] [/device(:n):path] [/?] 
```

**/c:**<em>n</em>  
実行するには、(1 は、既定値) のサイクル数を指定します。

**/d:**<em>n</em>  
サイクル間の遅延時間を指定します (秒単位。 60 は既定値)。

**/p:**<em>n</em>  
コネクト スタンバイ内に存続する時間を指定します (秒単位。 300 は既定値)。

**/device:**<em>n</em>  
パスは、テストするデバイスのインスタンスのパスを提供します。  
N は、[fx] の指示の遷移のため、デバイスを入力する必要があります、省略可能なデバイスの電源状態を提供します。

**使用例**

```
pwrtest /directedfx
```

## <a name="related-topics"></a>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

