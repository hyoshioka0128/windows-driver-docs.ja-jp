---
title: Static Driver Verifier をについてください。
description: Static Driver Verifier をについてください。
ms.assetid: 519e3314-2fea-4acd-8c0d-954a57e257ba
keywords:
- Static Driver Verifier WDK、Static Driver Verifier について
- StaticDV WDK、Static Driver Verifier について
- SDV の WDK、Static Driver Verifier について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c95e67345779c9b5e003319e50cd8b2b4e79cec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558392"
---
# <a name="understanding-static-driver-verifier"></a>Static Driver Verifier をについてください。


Windows Driver Model (WDM) またはカーネル モード ドライバー フレームワーク (KMDF)、NDIS、または Storport に準拠している堅牢なドライバーを作成するには、専門知識があるし、ドライバーが I/O マネージャーと対話する方法を理解する必要があります。 これらのドライバーをテストすることは、同じように注意が必要です。

Solid のドライバーの開発は、次の理由により困難となります。

-   ドライバーは、シングル プロセッサ マシン上であっても、非同期です。

-   ドライバーは、超再入可能です。

-   ドライバーは、多くのあいまいなルールを使用します。

-   ドライバー モデルは、革新的な時間の経過と共に有効期間します。

デバイス ドライバーのテストは、次の理由によって制限されます。

-   *監視*します。 ドライバーとオペレーティング システム間のやり取りでエラーを確認することはできません。 ドライバー クラッシュまたは不適切な動作は、その結果の暗黙の型の使用に関する規則に違反することができますが、開発とドライバーをテストする場合はエラーの根本原因を検出することは困難です。

-   *コントロール*します。 通常の状況で正しく動作するドライバーには、微妙なエラーなど、スタック内の下にあるドライバーは IRP に失敗すると、例外的な状況でのみ発生することができます。 このような状況は従来のテストも、ドライバーのコードによってエラー パスは適切に検出しませんのでを実行するため困難です。

SDV は、監視とドライバーをテストするときに必要のあるコントロールの両方を強化します。 WDM、KMDF、NDIS、および Storport の関数の適切な使用規則を定義し、これらの規則、ドライバーのコンプライアンスを監視、SDV はエラーを確認する機能が向上します。 WDM ルールなど[LowerDriverReturn](https://msdn.microsoft.com/library/windows/hardware/ff548273)特定の状況で、ドライバーのディスパッチ ルーチン返す必要があります常にスタックの下位のドライバーによって返された値を指定します。

SDV は、提供することで、コントロールも増加します。

-   ドライバーの環境では、継続的に失敗しているオペレーティング システムの呼び出し) (最悪のシナリオをいくつかが起こるの悪意のあるモデル。

-   強力な静的分析 (と呼ばれる*モデル チェック*)、ドライバーのすべての可能な実行パスを体系的に説明します。

SDV は、デバイス ドライバーの重要な単体テスト ツールです。 悪意のある環境でドライバーを配置し、体系的にテストがドライバー モデルの使用に関する規則の違反を探すことによって、ドライバーを経由するパスをコードします。

 

 





